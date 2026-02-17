---
title: Optimaliseren bij Edge
description: Leer hoe u optimalisaties in LLM Optimizer kunt leveren aan de CDN-rand zonder dat er ontwerpwijzigingen nodig zijn.
feature: Opportunities
source-git-commit: ae37ef578f279eae6ea51fd8aed5c6b91c8e1088
workflow-type: tm+mt
source-wordcount: '4843'
ht-degree: 0%

---


# Optimaliseren bij Edge

Deze pagina biedt een gedetailleerd overzicht van hoe u optimalisaties aan de CDN-rand kunt leveren zonder dat er ontwerpwijzigingen nodig zijn. Het behandelt het aan boord gaan proces, de beschikbare optimaliseringsmogelijkheden en hoe te om aan rand automatisch te optimaliseren.

>[!NOTE]
>Deze functionaliteit is momenteel in Vroege Toegang. U kunt meer over de vroege programma&#39;s van de Toegang [&#x200B; hier &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs) leren.

## Wat is Optimize in Edge?

Optimaliseren bij Edge is een op randen gebaseerde implementatiefunctie in LLM Optimizer die voor AI vriendelijke wijzigingen zorgt voor LLM-gebruikersagents. In de huidige context betekent &quot;Edge&quot; dat de optimalisatie wordt toegepast op de CDN-laag. Omdat het optimalisaties bij de laag CDN levert, worden geen auteursveranderingen in het Systeem van het Beheer van de Inhoud (CMS) vereist zodat uw oorsprong CMS onveranderd blijft. Met deze scheiding kunt u de zichtbaarheid van LLM verbeteren zonder de bestaande publicatieworkflows te wijzigen. Het is alleen gericht op agentisch verkeer en heeft geen invloed op menselijke gebruikers of SEO-bots. Wanneer LLM Optimizer mogelijkheden detecteert om een pagina te optimaliseren, kunnen gebruikers correcties direct bij de CDN-rand implementeren.

Optimaliseren in Edge is een sneller en leener alternatief voor traditionele oplossingen die complexe technische inspanningen vereisen. Zoals vermeld, zodra u eenmalig opstelling voltooit, worden geen platformveranderingen of lange ontwikkelingscycli vereist om de veranderingen toe te passen. U kunt verbeteringen binnen enkele minuten publiceren zonder dat u hiervoor de betrokkenheid van de ontwikkelaar nodig hebt. U kunt uw website op deze manier zonder code optimaliseren voor AI-agents.

Optimaliseren in Edge is ontworpen voor zakelijke gebruikers in marketing-, SEO-, content- en digitale strategische teams. Zo kunnen zakelijke gebruikers de volledige reis in LLM Optimizer voltooien: mogelijkheden identificeren, suggesties begrijpen en de oplossingen eenvoudig implementeren. Met Optimaliseren bij Edge kunnen gebruikers de wijzigingen voorvertonen, deze snel implementeren aan de CDN-rand en controleren of de optimalisaties live zijn. Prestaties kunnen worden bijgehouden in het ecosysteem van LLM Optimizer.

### Belangrijkste voordelen

* **AI-slechts levering:** serveert geoptimaliseerde HTML slechts aan AI agenten zonder invloed op of menselijke bezoekers of OSEO bots.
* **Snellere cycli:** publiceer veranderingen in notulen niet weken. Er zijn geen platformwijzigingen of lange technische cycli vereist.
* **Omkeerbaar:** gesteund met één-klik het terugschroeven van prijzen vermogen dat de pagina in notulen kan terugkeren.
* **geen prestatieseffect:** Op Edge gebaseerde optimalisaties en caching houden de plaatslatentie onaangetast.
* **CDN en CMS-agnostic:** werkt met om het even welke configuratie CDN en front-end opstelling ongeacht het Systeem van het Beheer van de Inhoud.

### Welke mogelijkheden worden gesteund met Optimize in Edge?

De kansen die de agentische Webervaring kunnen verbeteren worden gesteund met Optimize in Edge. Leer meer over elke kans zowel in de [&#x200B; pagina van het Dashboard van Kansen &#x200B;](/help/dashboards/opportunities.md) als de opportuniteitssectie in de huidige pagina.

## Onboarding

Neem contact op met uw Adobe-accountteam of het FDE-team om het instapproces te starten. Uw IT- of CDN-team is ook vereist om de voorwaarden en het installatieproces te voltooien. Daarnaast kunt u contact opnemen met `llmo-at-edge@adobe.com` voor verdere assistentie bij het instappen.

Voorwaarden voor optimalisatie aan boord in Edge:

* Voltooi het instapproces naar LLM Optimizer.
* Voltooi het logboek door:sturen proces voor uw CDN logboeken.

Vereisten voor uw IT/CDN-team:
* Voeg `*AdobeEdgeOptimize/1.0*` user-agent aan de Lijst van gewenste personen in het robots.txt- dossier of allebei-verkeersbeheerregels van uw plaats toe.
* Zorg ervoor dat de pagina&#39;s niet op het domein of CDN niveau worden geblokkeerd.
* Voeg Optimize bij Edge toe die regels in CDN verplettert.
* Bevestig Optimaliseren bij Edge-routering in de LLM Optimizer-interface.

Om het installatieproces te begeleiden, hieronder voorgesteld, zijn steekproefconfiguraties voor een aantal CDN montages. Houd er rekening mee dat deze voorbeelden moeten worden aangepast aan de werkelijke live configuratie. We raden u aan eerst wijzigingen toe te passen in de lagere omgevingen.

>[!BEGINTABS]

>[!TAB  de Dienst van de Wolk AEM beheerde CDN (snelst) ]

**Edge optimaliseert - de Dienst van de Wolk AEM beheerde CDN (snel)**

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

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

>[!TAB  Fastly (BYOCDN) ]

**Edge optimaliseert - snel (BYOCDN)**

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de Fastly VCL-regels instelt, moet u controleren of u:

* Toegang tot Fastly voor uw domein.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

**Stappen om uw API sleutel terug te winnen:**

1. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Onder **AI Verkeer dat verplettert om Optimalisaties** op te stellen, tik **optimalisaties aan AI Agenten** checkbox opstelt.

   ![&#x200B; Tik stel Optimalisaties aan AI Agenten &#x200B;](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png) op

3. Kopieer de API sleutel en ga met de verpletterende configuratiestappen hieronder te werk.

   ![&#x200B; Kopieer de API sleutel &#x200B;](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >In dit stadium, kan de status een rood kruis tonen die erop wijst dat de opstelling nog niet voltooid is. Dit wordt verwacht — zodra u de verpletterende configuratie hieronder voltooit en AI bot het verkeer begint te stromen, zal de status aan een groen controleteken bijwerken bevestigend dat het verpletteren met succes wordt toegelaten.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

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

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB  Akamai (BYOCDN) ]

**Edge optimaliseren - Akamai (BYOCDN)**

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de regels voor Akamai Property Manager instelt, moet u controleren of u:

* Toegang tot Akamai Property Manager voor uw domein.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

**Stappen om uw API sleutel terug te winnen:**

1. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Onder **AI Verkeer dat verplettert om Optimalisaties** op te stellen, tik **optimalisaties aan AI Agenten** checkbox opstelt.

   ![&#x200B; Tik stel Optimalisaties aan AI Agenten &#x200B;](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png) op

3. Kopieer de API sleutel en ga met de verpletterende configuratiestappen hieronder te werk.

   ![&#x200B; Kopieer de API sleutel &#x200B;](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >In dit stadium, kan de status een rood kruis tonen die erop wijst dat de opstelling nog niet voltooid is. Dit wordt verwacht — zodra u de verpletterende configuratie hieronder voltooit en AI bot het verkeer begint te stromen, zal de status aan een groen controleteken bijwerken bevestigend dat het verpletteren met succes wordt toegelaten.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

**Configuratie**

De volgende regel van de Manager van het Bezit van Akamai leidt gebruikersagenten LLM aan Edge Optimize. De configuratie bevat de volgende stappen:

**1. Plaats verpletterend criteria (gebruiker-Agent aanpassing)**

Plaats het verpletteren voor de volgende gebruiker-agenten:

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![&#x200B; plaats verpletterend criteria &#x200B;](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Oorsprong en SSL-gedrag instellen**

Oorsprong instellen als `live.edgeoptimize.net` en SAN afstemmen op `*.edgeoptimize.net`

![&#x200B; Vastgestelde Oorsprong en SSL gedrag &#x200B;](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Cachetoets instellen**

De toetsvariabele voor de cache `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` instellen op `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![&#x200B; vastgestelde Zeer belangrijke Variabele van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Caching Rules**

![&#x200B; Caching Regels &#x200B;](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Binnenkomende aanvraagheaders wijzigen**

Stel de volgende binnenkomende aanvraagheaders in:
`x-edgeoptimize-api-key` naar de API-sleutel die is opgehaald uit LLMO
`x-edgeoptimize-config` to `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` t/m `{{builtin.AK_URL}}`

![&#x200B; wijzigt Binnenkomende Kopballen van het Verzoek &#x200B;](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Binnenkomende antwoordheaders wijzigen**

![&#x200B; wijzigt Inkomende Kopballen van de Reactie &#x200B;](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Wijziging van cache-id**

![&#x200B; Verandering van identiteitskaart van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Uitgaande verzoekkopballen wijzigen**

`x-forwarded-host` header instellen op `{{builtin.AK_HOST}}`

![&#x200B; wijzigt Uitgaande Kopballen van het Verzoek &#x200B;](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Site-failover**

![&#x200B; Failover van de Plaats &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![&#x200B; Gedrag Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![&#x200B; Regels Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

Site-failover zorgt ervoor dat als bij Edge Optimize een `4XX` - of `5XX` -fout wordt geretourneerd, de aanvraag automatisch wordt teruggestuurd naar de standaardoorsprong, zodat de eindgebruiker nog steeds een antwoord ontvangt.

| Scenario | Gedrag |
| --- | --- |
| Edge Optimize geeft als resultaat `2XX` | De geoptimaliseerde reactie wordt aan de cliënt gediend. |
| Edge Optimize geeft `4XX` of `5XX` | Het verzoek wordt verpletterd terug naar de standaardoorsprong. |

**verifieer de opstelling**

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

>[!TAB  Cloudflare (BYOCDN) ]

**Edge optimaliseert - Cloudflare (BYOCDN)**

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de Cloudflare Worker instelt die regels routeert, moet u ervoor zorgen dat:

* Een Cloudflare-account met workers die op uw domein zijn ingeschakeld.
* Toegang tot DNS-instellingen van uw domein in Cloudflare.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

**Stappen om uw API sleutel terug te winnen:**

1. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Onder **AI Verkeer dat verplettert om Optimalisaties** op te stellen, tik **optimalisaties aan AI Agenten** checkbox opstelt.

   ![&#x200B; Tik stel Optimalisaties aan AI Agenten &#x200B;](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png) op

3. Kopieer de API sleutel en ga met de verpletterende configuratiestappen hieronder te werk.

   ![&#x200B; Kopieer de API sleutel &#x200B;](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >In dit stadium, kan de status een rood kruis tonen die erop wijst dat de opstelling nog niet voltooid is. Dit wordt verwacht — zodra u de verpletterende configuratie hieronder voltooit en AI bot het verkeer begint te stromen, zal de status aan een groen controleteken bijwerken bevestigend dat het verpletteren met succes wordt toegelaten.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

**hoe het verpletteren van werken**

Wanneer correct gevormd, wordt een verzoek aan uw domein (bijvoorbeeld, `www.example.com/page.html`) van een agentische gebruikersagent onderschept door de Arbeider van de Vormgeving van de Wolk en verpletterd aan het Edge Optimize achtereind. Het achterste verzoek omvat de vereiste kopballen.

**het Testen van het achterste eindverzoek**

U kunt het verpletteren verifiëren door een direct verzoek aan Edge te richten optimaliseert achtereind.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Vereiste Kopballen**

Bij aanvragen naar de Edge Optimize-backend moeten de volgende headers worden ingesteld:

| Koptekst | Beschrijving | Voorbeeld |
|--------|-------------|---------|
| `x-forwarded-host` | De oorspronkelijke host van de aanvraag. Vereist voor identificatie van het sitedomein. | `www.example.com` |
| `x-edgeoptimize-url` | Het oorspronkelijke URL-pad en de queryreeks van de aanvraag. | `/page.html` of `/products?id=123` |
| `x-edgeoptimize-api-key` | De API-sleutel die Adobe voor uw domein biedt. | `your-api-key-here` |
| `x-edgeoptimize-config` | De koord van de configuratie voor geheim voorgeheugenzeer belangrijke differentiatie. | `LLMCLIENT=TRUE;` |

**Stap 1: Creeer de Worker van de Veldarm**

1. Meld u aan bij het dashboard Cloudflare.
2. Navigeer aan **Arbeiders &amp; Pagina&#39;s** in sidebar.
3. Klik **creëren toepassing** en dan **creëren de Arbeider**.
4. Geef de worker een naam (bijvoorbeeld `edge-optimize-router` ).
5. Klik **opstellen** om de worker met de standaardcode tot stand te brengen.

![&#x200B; dashboard van de Werknemers van de Wolk &#x200B;](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Stap 2: Voeg de code van de Arbeider** toe

Na het creëren van de arbeider, geeft de klik **code** uit en vervangt de standaardcode met het volgende:

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Klik **sparen en stel** op om de worker te publiceren.

![&#x200B; de coderedacteur van de Arbeider van de Wolk &#x200B;](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Stap 3: Vorm omgevingsvariabelen**

Omgevingsvariabelen slaan gevoelige configuratie als de API-sleutel veilig op.

1. In de montages van uw worker, navigeer aan **Montages** > **Variabelen**.
2. Onder **Variabelen van het Milieu**, klik **veranderlijke** toevoegen.
3. Voeg de volgende variabelen toe:

   | Naam variabele | Beschrijving | Vereist |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | De door Adobe verschafte Edge Optimize API-sleutel. | Ja |
   | `EDGE_OPTIMIZE_TARGET_HOST` | De doelhost voor Edge Optimize-aanvragen (verzonden als `x-forwarded-host` header) en het oorspronkelijke domein voor failover. Dit moet alleen het domein zijn zonder protocol (bijvoorbeeld `www.example.com` , niet `https://www.example.com` ). | Ja |

4. Voor de API sleutel, klik **Coderen** om het veilig op te slaan.
5. Klik **sparen en stel** op.

![&#x200B; Cloudflare milieu variabelen &#x200B;](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Stap 4: Voeg een route aan uw domein** toe

De worker op uw domein activeren:

1. Ga naar de Montages van uw arbeider **&#x200B;**&#x200B;> **Trekkers**.
2. Onder **Routes**, klik **route** toevoegen.
3. Voer uw domeinpatroon in (bijvoorbeeld `www.example.com/*` of `example.com/*` ).
4. Selecteer de zone in het vervolgkeuzemenu.
5. Klik **sparen**.

Alternatief, kunt u routes op het streekniveau vormen:

1. Navigeer naar uw domein in Cloudflare.
2. Ga naar **Routes van de Arbeiders**.
3. Klik **toevoegen route** en specificeer het patroon en de arbeider.

![&#x200B; de routes van de Arbeider van de Wolk &#x200B;](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**Stap 5: Verifieer de opstelling**

Na het opstellen, test de configuratie door een verzoek met een agentic gebruikersagent te doen.

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

De header `x-edgeoptimize-request-id` is een succesvol antwoord:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

U kunt ook verifiëren dat het normale verkeer blijft werken:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0"
```

Dit verzoek moet vanaf uw oorsprong worden verzonden zonder de header `x-edgeoptimize-request-id` .

**het verifiëren van failovergedrag**

Als Edge Optimize niet beschikbaar is of een fout retourneert, mislukt de worker automatisch naar de oorsprong. Voorbeelden van failover-reacties zijn de header `x-edgeoptimize-fo` :

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

U kunt de gebeurtenissen van failover in de logboeken van de Werknemers van de Wolk controleren om kwesties problemen op te lossen.

**Begrijpend de logica van de Arbeider**

De Cloudflare Worker implementeert de volgende logica:

1. {de opsporing van de Agent van 0} Gebruiker:**controleert als de de gebruikersagent van het inkomende verzoek om het even welke bepaalde agentic bots (case-insensitive) aanpast.**

2. **Weg richtend:** naar keuze filters verzoeken die op gerichte wegen worden gebaseerd. Standaard worden alle HTML-pagina&#39;s (URL&#39;s die eindigen met `/` , geen extensie of `.html` ) gerouteerd. U kunt specifieke paden opgeven met de array `TARGETED_PATHS` .

3. **bescherming van de Lijn:** de `x-edgeoptimize-request` kopbal verhindert oneindige lijnen. Wanneer Edge Optimize aanvragen terugstuurt naar uw oorsprong, wordt deze header ingesteld op `"1"` en geeft de worker de aanvraag door zonder deze terug te sturen naar Edge Optimize.

4. **veiligheid van de Kopbal:** alvorens Edge te plaatsen optimaliseert kopballen, verwijdert de worker om het even welke bestaande `x-edgeoptimize-*` kopballen van het inkomende verzoek om de aanvallen van de kopbalinjectie te verhinderen.

5. **afbeelding van de Kopbal:** de arbeider plaatst de vereiste kopballen voor Edge optimaliseren:
   * `x-forwarded-host` - Identificeert het oorspronkelijke sitedomein.
   * `x-edgeoptimize-url` - Behoudt het oorspronkelijke aanvraagpad en de oorspronkelijke queryreeks.
   * `x-edgeoptimize-api-key` - Hiermee wordt de aanvraag geverifieerd met Edge Optimize.
   * `x-edgeoptimize-config` - Biedt een configuratie voor de cachemleutel.

6. **logica Failover:** als Edge optimaliseert om het even welke code van de foutenstatus terugkeert (4XX cliëntfouten of 5XX serverfouten) of het verzoek wegens een netwerkfout ontbreekt, ontbreekt de worker automatisch over aan uw oorsprong gebruikend `EDGE_OPTIMIZE_TARGET_HOST`. De failoverreactie omvat `x-edgeoptimize-fo: 1` kopbal om erop te wijzen dat failover voorkwam.

7. **Redirect behandeling:** de `redirect: "manual"` optie zorgt ervoor dat de omleidingsreacties van Edge optimaliseren door aan de cliënt zonder de worker worden overgegaan die hen volgt.

**het Aanpassen van de configuratie**

U kunt het arbeidersgedrag aanpassen door de configuratieconstanten bij de bovenkant van de code te wijzigen:

**Agentic bot list**

Wijzig de array `AGENTIC_BOTS` om gebruikersagents toe te voegen of te verwijderen:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**gerichte wegen**

Standaard worden alle HTML-pagina&#39;s gerouteerd naar Edge Optimize. Als u het routeren wilt beperken tot specifieke paden, wijzigt u de array `TARGETED_PATHS` :

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**configuratie Failover**

Standaard mislukt de worker op een 4XX- of 5XX-fout in Edge Optimize. Pas dit gedrag aan:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Belangrijke overwegingen**

* **gedrag Failover:** De worker ontbreekt automatisch over aan uw oorsprong als Edge optimaliseert om het even welke fout (4XX of 5XX statuscodes) terugkeert of als het verzoek wegens een netwerkfout ontbreekt. Failover gebruikt `EDGE_OPTIMIZE_TARGET_HOST` als het oorspronkelijke domein (vergelijkbaar met het `F_Default_Origin` of CloudFront `Default_Origin` van Fastly). De antwoorden van Failover omvatten de `x-edgeoptimize-fo: 1` kopbal, die u voor controle en het zuiveren kunt gebruiken.

* **Caching:** de geheime voorgeheugenreacties van de Wolk die op URL door gebrek worden gebaseerd. Omdat het agentische verkeer verschillende inhoud dan menselijk verkeer ontvangt, zorg uw rekeningen van de geheim voorgeheugenconfiguratie voor dit voor. U kunt de cache-API of cachekoppen gebruiken om de cacheinhoud te onderscheiden. De header `x-edgeoptimize-config` moet in de cachemoets worden opgenomen.

* **het Beperken van het Tarief:** monitor uw Edge optimaliseert gebruik en overweegt het uitvoeren van tarief dat voor agentic verkeer indien nodig beperkt.

* **het Testen:** test altijd de configuratie in een het opvoeren milieu alvorens aan productie op te stellen. Verifieer dat zowel agentisch als menselijk verkeer zich zoals verwacht gedragen. Het gedrag van de failover van de test door Edge te simuleren optimaliseert fouten.

* **Logging:** laat het registreren van de Werknemers van de Wolk toe Cloudflare om verzoeken te controleren en kwesties problemen op te lossen. Navigeer aan **Arbeiders** > **uw arbeider** > **Logboeken** om logboeken in real time te bekijken. De worker registreert failover-gebeurtenissen voor foutopsporingsdoeleinden.

**Problemen oplossen**

| Probleem | Mogelijke oorzaak | Oplossing |
|-------|----------------|----------|
| Geen `x-edgeoptimize-request-id` header in reactie | De route van de arbeider niet, of gebruikersagent niet in de agentic bots lijst. | Verifieer uw routepatroon de verzoek URL aanpast. Controleer of de gebruikersagent zich in de array `AGENTIC_BOTS` bevindt. |
| 401 of 403 fouten van Edge Optimize | Ongeldige of ontbrekende API-sleutel. | Controleer of `EDGE_OPTIMIZE_API_KEY` correct is ingesteld in omgevingsvariabelen. Neem contact op met Adobe om te bevestigen dat uw API-sleutel actief is. |
| Oneindige omleidingen of lussen | Koptekst voor lusbeveiliging wordt niet op de juiste wijze ingesteld of gecontroleerd. | Controleer of de `x-edgeoptimize-request` -headercontrole is uitgevoerd. |
| Beïnvloed menselijk verkeer | Worker die logica verplettert is te breed. | Verifieer de gebruikersagent passende logica correct en case-insensitive is. Controleer of `TARGETED_PATHS` correct is geconfigureerd. |
| Trage responstijden | Netwerkvertraging naar Edge Optimize backend. | Dit wordt verwacht voor het eerste verzoek; volgende aanvragen worden in de cache geplaatst bij Edge Optimize. |
| `x-edgeoptimize-fo: 1` header in reactie | Edge Optimize heeft een fout en failover naar de oorsprong geretourneerd. | Controleer de logboeken van de Werknemers van de Wolk voor de specifieke foutencode. Controleer de servicestatus Edge Optimize met Adobe. |
| Failover werkt niet | De vlaggen van Failover gehandicapt, of fout in failoverlogica. | Verifiëren `FAILOVER_ON_4XX` en `FAILOVER_ON_5XX` worden ingesteld op `true` . Controleren of workers zich aanmelden voor foutberichten. |
| Bepaalde paden zijn niet geoptimaliseerd | Pad komt niet overeen met het doelpad of het HTML-paginapatroon. | Controleer of het pad zich in `TARGETED_PATHS` (indien opgegeven) bevindt en of het overeenkomt met het HTML-pagina regex-patroon. |
| Verzoeken mislukken met ongeldige host | `EDGE_OPTIMIZE_TARGET_HOST` bevat een protocol (bijvoorbeeld `https://` ). | Gebruik alleen de domeinnaam zonder protocol (bijvoorbeeld `example.com` en niet `https://example.com` ). |
| 530-fout tijdens failover | Cloudflare kan geen verbinding maken met de oorsprong of failover-aanvraag heeft ongeldige headers. | Controleer of de functie failover de koppen voor Edge Optimize verwijdert. Verifieer uw oorsprong toegankelijk is en DNS correct wordt gevormd. |

>[!ENDTABS]

>[!NOTE]
>Neem voor andere CDN-providers contact op met `llmo-at-edge@adobe.com` om uw IT/CDN-teams te helpen bij het instappen. Zodra de installatieconfiguraties zijn voltooid, kunt u suggesties voor Optimize bij de kansen van Edge in LLM Optimizer opstellen.

## Kansen

Deze tabel vindt u in de volgende tabel met mogelijkheden die de taalkundige webervaring kunnen verbeteren en die worden ondersteund met Optimaliseren in Edge.

| Opportunity | Type | Automatisch identificeren | Automatisch voorstellen | Automatisch optimaliseren |
|---------|----------|----------|----------|----------|
| Zichtbaarheid van inhoud herstellen | Technische GEO | Detecteert pagina&#39;s waarop kritieke inhoud van AI-agents wordt verborgen. Hiermee worden beïnvloede URL&#39;s en verwachte inhoud weergegeven die kunnen worden hersteld. | Hiermee wordt de inhoud gemarkeerd die beschikbaar kan worden gemaakt voor AI-agents en wordt aangeraden om pre-rendering voor deze pagina&#39;s in te schakelen. | Serveert een volledig teruggegeven, AI-vriendschappelijke momentopname van HTML aan zinloos verkeer dat de eerder verborgen inhoud terugkrijgt. |
| Koppen voor LLM&#39;s optimaliseren | Inhoud optimaliseren | Scant koppen om lege, dubbele, ontbrekende of dubbelzinnige koppen te detecteren die de leesbaarheid van de machine kunnen verminderen. | Stelt een duidelijkere koptekshiërarchie en verbeterde labels voor en toont een voorvertoning van de bijgewerkte structuur voor elke pagina. | Hiermee wordt de verbeterde kopstructuur voor AI-agents geïnjecteerd, zodat uw visuele ontwerp behouden blijft en de pagina beter leesbaar wordt voor LLM&#39;s. |
| LLM-vriendelijke samenvattingen toevoegen | Inhoud optimaliseren | Hiermee worden lange of complexe pagina&#39;s aangegeven waarvoor geen beknopte overzichten op pagina- of sectieniveau beschikbaar zijn, waardoor het voor AI moeilijker wordt om snel te scannen en te begrijpen. | Hiermee raadt u korte, door AI gegenereerde samenvattingen op pagina- en sectieniveau aan die de belangrijkste inhoud vastleggen. | Hiermee voegt u de samenvattingen in de desbetreffende HTML-secties in, waardoor modellen de pagina-inhoud beter kunnen interpreteren en beschrijven. |
| Relevante veelgestelde vragen toevoegen | Inhoud optimaliseren | Hiermee worden gaten in de intentie in de bestaande pagina-inhoud gedetecteerd die baat kunnen hebben bij veelgestelde vragen. | Stelt door AI gegenereerde veelgestelde vragen-inhoud voor die is uitgelijnd op de gebruikersinstelling en bestaande onderwerpen. | Hiermee wordt veelgestelde vragen-inhoud in de HTML geïnjecteerd, waardoor pagina&#39;s beter te ontdekken en relevanter worden in door AI gestuurde antwoorden. |
| Complexe inhoud vereenvoudigen | Inhoud optimaliseren | Hiermee markeert u pagina&#39;s met complexe tekst die AI-begrip kan belemmeren. | Biedt door AI gegenereerde vereenvoudigde versies van complexe tekst met behoud van de oorspronkelijke betekenis. | Hiermee herschrijft u complexe secties op de pagina en verbetert u de leesbaarheid van AI. |

### Extra gereedschappen

[&#x200B; Adobe LLM Optimizer: Is uw webpage citabel?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome-extensie laat zien hoeveel van uw webpagina-inhoud LLM&#39;s kunnen openen en wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie.

Met één klik kunt u de gereedschapsleesbaarheid van elke site evalueren. U kunt een vergelijking naast elkaar bekijken van wat AI agenten tegenover zien wat menselijke gebruikers zien, en schatten hoeveel inhoud door LLM Optimizer kon worden teruggekregen. Zie [&#x200B; AI uw website lezen?](https://business.adobe.com/nl/blog/introducing-the-llm-optimizer-chrome-extension) voor meer informatie.

## Gedetailleerde mogelijkheden

In de volgende secties kunt u aanvullende details bekijken voor elke opportuniteit die wordt ondersteund bij Optimaliseren in Edge.

### Zichtbaarheid van inhoud herstellen

Deze kans geeft pagina&#39;s weer waar de belangrijkste inhoud verborgen is voor AI-agents vanwege renderen op de client. Voor elke geïdentificeerde pagina wordt precies weergegeven welke inhoud ontbreekt in de AI-agentweergave, worden de zichtbaarheidsverschillen gemarkeerd en kunt u direct wijzigingen toepassen om de verborgen inhoud te herstellen. Wanneer u deze kans met Optimize in Edge opstelt, wordt een pre-teruggegeven, AI-geoptimaliseerde versie van de pagina aan gebruikersagenten LLM getoond zodat kunnen zij tot de volledige context toegang hebben zonder JavaScript uit te voeren.
Dit zorgt ervoor dat de pagina voor het eerst volledig zichtbaar is voor AI-agents. Er worden aanvullende verbeteringen toegepast op die vooraf gerenderde HTML.

>[!IMPORTANT]
>Deze pre-renderfunctie is automatisch van toepassing op alle hieronder weergegeven mogelijkheden bij Optimaliseren in Edge om ervoor te zorgen dat de pagina volledig zichtbaar is voor AI-agents.

### Koppen voor LLM&#39;s optimaliseren

Deze kans detecteert pagina&#39;s waar de kopstructuur het voor AI-agents moeilijk maakt de pagina te begrijpen vanwege lege, dubbele, ontbrekende of dubbelzinnige koppen. Voor elke betrokken pagina wordt met deze optie de suboptimale koppen weergegeven en wordt een duidelijkere hiërarchie aanbevolen. Wanneer opgesteld met Optimize in Edge, worden de betere rubrieken toegepast in HTML die aan agentic verkeer wordt gediend. Hierdoor is de machine beter leesbaar en blijft de persoonlijke lay-out ongewijzigd.

### LLM-vriendelijke samenvattingen toevoegen

Deze kans identificeert pagina&#39;s die van beknopte samenvattingen kunnen profiteren om LLM&#39;s te helpen snel begrijpen waar de pagina-inhoud over gaat. Voor elke pagina, ontdekt de kans waar een samenvatting het meest nodig is en leidt tot AI-geproduceerde samenvattingen of op paginaniveau of sectieniveau. Wanneer u met Optimize bij Edge opstelt worden deze samenvattingen opgenomen in de HTML die AI agenten terugwinnen, verbeterend de kansen om uw inhoud te hebben nauwkeuriger worden beschreven.

### Relevante veelgestelde vragen toevoegen

Met deze mogelijkheid worden pagina&#39;s gemarkeerd waar extra inhoud van Vragen en antwoorden beter kan overeenkomen met de gebruikerintentie en aanwijzingen voor detectie met een AI-basis. Voor elke pagina worden door AI gegenereerde blokken FAQ voorgesteld die zijn gekoppeld aan de gebruikersinhoud en -inhoud op de pagina. Met Optimize in Edge worden deze veelgestelde vragen in de HTML geïnjecteerd, waardoor uw pagina AI-vriendelijker wordt en de kans groter wordt dat de AI-antwoorden direct uw richtlijnen weerspiegelen.

### Complexe inhoud vereenvoudigen

Deze kans vindt pagina&#39;s met lange, complexe alinea&#39;s die AI-begrip kunnen verminderen. Voor elke pagina die de leesbaarheidsdrempels overschrijdt, wordt door AI gegenereerde inhoud gemaakt die eenvoudiger en gemakkelijker te scannen is, terwijl de oorspronkelijke betekenis behouden blijft. Wanneer opgesteld bij de rand, de vereenvoudigde inhoud die aan agentic verkeer wordt geleverd helpt LLMs uw inhoud interpreteren en nauwkeuriger samenvatten.

## Automatisch optimaliseren bij Edge

Voor elke gelegenheid, kunt u voorproef, uitgeven, opstellen, levende bekijken, en de optimalisaties bij de rand terugdraaien.

>[!VIDEO](https://video.tv.adobe.com/v/3477990/?captions=dut&learn=on&enablevpops)

### Voorvertoning

**Voorproef** laat u het effect van een suggestie zien alvorens het live gaat. Er wordt een verschil tussen de huidige pagina en de voor AI geoptimaliseerde versie verwacht na het toepassen van de suggestie. In deze weergave wordt dezelfde functie Optimaliseren bij Edge gebruikt die live verkeer, maar in een geïsoleerde voorvertoningsmodus, mogelijk maakt. Dit beïnvloedt levend verkeer niet aangezien het een read-only simulatie voor overzicht is.

![&#x200B; Voorproef &#x200B;](/help/assets/optimize-at-edge/preview.png)

### Bewerken

**geeft** uit staat u toe om de auto-geproduceerde suggestie te verfijnen of geheel te herschrijven alvorens het op te stellen. In plaats van de suggestie te accepteren, kunt u de volledige controle behouden via de bewerkingsworkflow. In de weergave worden voorgestelde wijzigingen weergegeven in een gestructureerde editor, waar u de tekst kunt wijzigen zodat deze beter aansluit bij uw oorspronkelijke intentie. De bewerkte versie wordt vervolgens aan AI-agents geleverd zodra deze zijn geïmplementeerd.

![&#x200B; geeft &#x200B;](/help/assets/optimize-at-edge/edit.png) uit

### Implementeren

**stelt** op publiceert de geselecteerde suggesties zodat kunnen de geoptimaliseerde ervaringen van de rand aan AI agenten worden gediend. Als CDN volledig wordt verpletterd, gaan alle pagina&#39;s in het domein gewoonlijk met de nieuwe veranderingen binnen notulen. Als het verpletteren voor uitgezochte wegen slechts is gevormd, slechts gaan de gevoegde op lijst van gewenste personen pagina&#39;s met de optimalisaties.

![&#x200B; opstellen &#x200B;](/help/assets/optimize-at-edge/deploy.png)

### Live weergeven

**Levende Mening** laat u verifiëren dat de optimalisering levend is en zich zoals verwacht voor agentisch verkeer gedraagt, een mening die anders moeilijk zou zijn om toegang te hebben. U kunt de actieve pagina weergeven onder Vaste suggesties, waardoor de pagina wordt weergegeven zoals deze wordt weergegeven bij AI-agents.

![&#x200B; Levende Mening &#x200B;](/help/assets/optimize-at-edge/view-live.png)

### Terugdraaien

Met Terugdraaien wordt een eerder geïmplementeerde optimalisatie veilig hersteld. De alleen-AI versie van de pagina wordt doorgaans binnen enkele minuten teruggezet naar de vorige staat, zodat u indien nodig veilig met optimalisaties kunt experimenteren.

![&#x200B; Terugkeer &#x200B;](/help/assets/optimize-at-edge/rollback.png)

## Veelgestelde vragen

V. Welk soort LLMs richt u met Optimize bij Edge?

De lijst van gebruikersagenten aan doel wordt bepaald door u tijdens het aan boord gaan proces.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

V. Wat gebeurt er als ik nog niet aan boord ben om te optimaliseren in Edge?

Als u **klikt stel optimalisaties** op alvorens de vereiste opstelling te voltooien, zal niets op uw plaats worden toegepast. In plaats daarvan wordt u in een pop-updialoogvenster gevraagd contact op te nemen met ons team op `llmo-at-edge@adobe.com` voor hulp bij het instappen. Totdat het instappen volledig is, kunt u nog de ontdekte kansen en de suggesties onderzoeken, maar de één-klik plaatsingswerkschema zal inactief blijven.

V: Wat gebeurt er als de inhoud bij de bron wordt bijgewerkt?

We leveren de geoptimaliseerde versie van uw pagina vanuit cache zolang de onderliggende bronpagina niet is gewijzigd. Nochtans, wanneer de bron voor **verandert herstelt Zichtbaarheid van de Inhoud**, verandert ons systeem automatisch zodat ontvangen de AI agenten altijd de meest bijgewerkte inhoud. Dit komt doordat we de FLV-instellingen (in volgorde van minuten) gebruiken om een lage cache op te slaan, zodat bij elke update van de inhoud op uw site een nieuwe optimalisatie binnen dat venster wordt geactiveerd. Voor inhoudskansen zoals **voegt LLM-Vriendelijke Samenvattingen** toe, controleert LLM Optimizer de bronpagina voor veranderingen. Als een verandering wordt ontdekt, pauzeren wij de optimalisering en markeren het voor menselijk overzicht om inhoudsverschuiving tussen de agent-zichtbare pagina en mens-zichtbare pagina te verhinderen.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

V. Is Optimize bij Edge alleen voor sites die gebruikmaken van Adobe Edge Delivery Service (EDS)?

Nee. Optimaliseren in Edge is niet alleen CDN-agnostisch en werkt met elke front-end architectuur, maar ook met de architectuur die op Adobe EDS Stack wordt geïmplementeerd.

V. Hoe wordt Optimaliseren bij Edge-pre-rendering anders dan bij traditionele rendering op de server?

Beide problemen lossen verschillende problemen op en kunnen samenwerken. Traditionele SSR rendert inhoud aan serverzijde maar omvat geen inhoud die later in browser wordt geladen. Optimaliseren bij voorrendering van Edge legt de pagina vast nadat JavaScript en client-side gegevens zijn geladen, waardoor de volledig geassembleerde versie aan de CDN-rand wordt geproduceerd. SSR richt zich op het verbeteren van de menselijke ervaring en Optimize in Edge verbetert de webervaring voor LLMs.

Q. wat gebeurt als ik optimalisaties voor sommige URLs in mijn domein maar niet allen opstel?

Alleen de URL&#39;s die u expliciet optimaliseert, worden gewijzigd. Voor URLs met opgestelde kansen, ontvangen de agenten AI de geoptimaliseerde versie. Voor URLs zonder opgezette kansen, onze dienst stelt eenvoudig de originele pagina voor zoals-is zonder veranderingen toe te passen of het op te slaan in onze laag van het optimalisatiecache. Op deze manier kunt u optimalisaties selectief implementeren zonder dat dit van invloed is op de rest van uw site.
