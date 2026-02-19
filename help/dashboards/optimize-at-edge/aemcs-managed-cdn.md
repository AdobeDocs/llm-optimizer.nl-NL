---
title: Optimaliseren bij Edge - AEM Cloud Service Managed CDN (snel)
description: Leer hoe u de CDN (Fastly) voor beheer van de AEM Cloud Service configureert voor optimalisatie bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---


# AEM Cloud Service Managed CDN (snel)

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Ga als volgt te werk om het routeren van hoekig verkeer naar Edge Optimize:

1. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Onder **AI Verkeer dat verplettert om Optimalisaties** op te stellen, tik **optimalisaties aan AI Agenten** checkbox opstelt. Het team van Adobe zal de verpletterende configuratie namens u behandelen.

   ![&#x200B; Tik stel Optimalisaties aan AI Agenten &#x200B;](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png) op

3. Nadat u het selectievakje hebt ingeschakeld, geeft de status aan dat de installatie wordt uitgevoerd. Het team van Adobe zal de verpletterende configuratie voor u voltooien.

   ![&#x200B; AI Verkeer die opstelling verplettert momenteel &#x200B;](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   Zodra het verpletteren en actief wordt gevormd, zal de status bijwerken om een groen controleteken te tonen die erop wijzen dat het verpletteren met succes wordt toegelaten. U hoeft geen verdere actie te ondernemen.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

**Zelfbediening verpletterend via de Pijpleiding van Cloud Manager**

Als u verkiest om het verpletteren door de Pijpleiding van Cloud Manager te vormen, volg de hieronder stappen. De verpletterende configuratie wordt gedaan door een [&#x200B; originSelector CDN regel &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors) te gebruiken. De voorwaarden zijn als volgt:

* Bepaal het domein dat moet worden verpletterd.
* Bepaal de paden die u wilt routeren.
* Beslis de gebruikersagenten die (geadviseerde regex) moeten worden verpletterd.

Om de regel op te stellen, moet u:

* Creeer de pijpleiding van de a [&#x200B; configuratie &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-manager-cloud-service/content/operations/config-pipeline).
* Leg het configuratiebestand van `cdn.yaml` vast in uw opslagplaats.
* Voer de configuratiepijplijn uit.

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"
```

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

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

{{return-to-overview}}
