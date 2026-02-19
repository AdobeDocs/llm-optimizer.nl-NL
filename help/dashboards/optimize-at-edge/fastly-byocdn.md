---
title: Optimaliseren bij Edge, snel (BYOCDN)
description: Leer hoe u snel BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---


# Snel (BYOCDN)

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de Fastly VCL-regels instelt, moet u controleren of u:

* Toegang tot Fastly voor uw domein.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Configuratie**

Voeg de volgende drie fragmenten VCL aan uw Snelle dienst toe. Deze fragmenten behandelen het verpletteren van agentische verzoeken aan Edge Optimize, geheim voorgeheugenzeer belangrijke scheiding, en failover aan uw standaardoorsprong.

![&#x200B; VCL van de Fastly &#x200B;](/help/assets/optimize-at-edge/fastly-vcl.png)

![&#x200B; voeg VCL fragmenten &#x200B;](/help/assets/optimize-at-edge/add-vcl-snippets.png) toe

**vcl_recv fragment**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-forwarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=TRUE;"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**vcl_hash fragment**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_delivery fragment**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

**Failover**

Het fragment `vcl_deliver` handelt failover automatisch af. Als Edge Optimize een `4XX` - of `5XX` -fout retourneert, wordt de aanvraag opnieuw gestart en teruggestuurd naar de standaardoorsprong, zodat de eindgebruiker nog steeds een antwoord ontvangt. Tot de failover-reacties behoort ook de header `x-edgeoptimize-fo: 1` .

| Scenario | Gedrag |
| --- | --- |
| Edge Optimize geeft als resultaat `2XX` | De geoptimaliseerde reactie wordt aan de cliënt gediend. |
| Edge Optimize geeft `4XX` of `5XX` | Het verzoek wordt opnieuw gestart en vanuit de standaardoorsprong verzonden. |
| Failoverreactie | Bevat de koptekst `x-edgeoptimize-fo: 1` . |

**verifieer de opstelling**

Na de voltooiing van de opstelling, verifieer dat beide verkeer aan Edge Optimize wordt verpletterd en dat het menselijke verkeer onaangetast blijft.

**1. Het verkeer van de Bot van de test (zou moeten worden geoptimaliseerd)**

Simuleer een AI bot request using an agentic user-agent:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Een succesvol antwoord bevat de header `x-edgeoptimize-request-id` , waarmee wordt bevestigd dat het verzoek is gerouteerd via Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Het menselijke verkeer van de test (zou NIET moeten worden beïnvloed)**

Simuleer een regelmatig verzoek van een menselijke browser:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

De reactie zou **&#x200B;**&#x200B;niet `x-edgeoptimize-request-id` kopbal moeten bevatten. De pagina-inhoud en de reactietijd moeten gelijk blijven aan voordat u Optimaliseren in Edge inschakelt.

**3. Hoe te tussen de twee scenario&#39;s te onderscheiden**

| Koptekst | Bot-verkeer (geoptimaliseerd) | Menselijk verkeer (niet beïnvloed) |
|---|---|---|
| `x-edgeoptimize-request-id` | Huidig — bevat een unieke aanvraag-id | Afwezig |
| `x-edgeoptimize-fo` | Alleen aanwezig als failover is opgetreden (waarde: `1`) | Afwezig |

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

{{return-to-overview}}
