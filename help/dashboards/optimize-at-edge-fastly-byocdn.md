---
title: Optimaliseren bij Edge, snel (BYOCDN)
description: Leer hoe u snel BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '217'
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

![ VCL van de Fastly ](/help/assets/optimize-at-edge/fastly-vcl.png)

![ voeg VCL fragmenten ](/help/assets/optimize-at-edge/add-vcl-snippets.png) toe

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

{{verify-setup-byocdn}}

{{return-to-overview}}
