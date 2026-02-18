---
title: Optimaliseren bij Edge - AEM Cloud Service Managed CDN (snel)
description: Leer hoe u de CDN (Fastly) voor beheer van de AEM Cloud Service configureert voor optimalisatie bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 8cdd15413555057165f69ea4d5a15b243ab9098d
workflow-type: tm+mt
source-wordcount: '329'
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

Als u verkiest om het verpletteren door de Pijpleiding van Cloud Manager te vormen, volg de hieronder stappen. De verpletterende configuratie wordt gedaan door een [&#x200B; originSelector CDN regel &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors) te gebruiken. De voorwaarden zijn als volgt:

* Bepaal het domein dat moet worden verpletterd.
* Bepaal de paden die u wilt routeren.
* Beslis de gebruikersagenten die (geadviseerde regex) moeten worden verpletterd.

Om de regel op te stellen, moet u:

* Creeer de pijpleiding van de a [&#x200B; configuratie &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline).
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

{{verify-setup-adobe-aem-cs-cdn}}

{{return-to-overview}}
