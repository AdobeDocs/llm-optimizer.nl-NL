---
title: Optimaliseren bij Edge
description: Leer hoe u optimalisaties in LLM Optimizer kunt leveren aan de CDN-rand zonder dat er ontwerpwijzigingen nodig zijn.
feature: Opportunities
source-git-commit: eb8bdf9144aebb85171a529a3cc25034be5b076e
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 0%

---


# Optimaliseren bij Edge

Deze pagina biedt een gedetailleerd overzicht van hoe u optimalisaties aan de CDN-rand kunt leveren zonder dat er ontwerpwijzigingen nodig zijn. Het behandelt het aan boord gaan proces, de beschikbare optimaliseringsmogelijkheden en hoe te om aan rand automatisch te optimaliseren.

>[!NOTE]
>Deze functionaliteit is momenteel in Vroege Toegang. U kunt meer over de vroege programma&#39;s van de Toegang [&#x200B; hier &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs) leren.

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

* Een API-sleutel genereren.
* Voeg Optimize bij Edge toe die regels in CDN verplettert.
* Door de gebruiker gedefinieerde paden of het hele domein Lijsten van gewenste personen.
* Voeg een user-defined lijst van gebruikersagenten LLM aan doel toe.
* Zorg ervoor dat `robots.txt` geen gebruikersagents blokkeert die zijn bedoeld als doel.
* Bevestig Optimaliseren bij Edge-routering in de LLM Optimizer-interface.

Om het installatieproces te begeleiden, hieronder voorgesteld, zijn steekproefconfiguraties voor een aantal CDN montages. Houd er rekening mee dat deze voorbeelden moeten worden aangepast aan de werkelijke live configuratie. We raden u aan eerst wijzigingen toe te passen in de lagere omgevingen.

>[!BEGINTABS]

>[!TAB  Adobe beheerde CDN ]

**Adobe beheerde CDN**

Het doel van deze configuratie is verzoeken met agentische gebruikersagenten te vormen die aan de Optimizer dienst (`live.edgeoptimize.net` backend) zullen worden verpletterd. Als u de configuratie wilt testen, zoekt u na de installatie naar de header `x-edgeoptimize-request-id` in de reactie.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De verpletterende configuratie wordt gedaan door een [&#x200B; originSelector CDN regel &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors) te gebruiken. De voorwaarden zijn als volgt:

* beslissen welk domein moet worden verpletterd
* bepalen welke paden moeten worden gerouteerd
* beslissen de gebruikersagenten om worden verpletterd (geadviseerde regex)

Om de regel op te stellen, moet u:

* creeer de pijpleiding van de a [&#x200B; configuratie &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* het configuratiebestand van `cdn.yaml` toewijzen in uw opslagplaats
* de configuratiepijplijn uitvoeren


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

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

>[!TAB  Fastly (BYOCDN) ]

**Edge optimaliseert BYOCDN - snel - VCL**

![&#x200B; VCL van de Fastly &#x200B;](/help/assets/optimize-at-edge/fastly-vcl.png)

![&#x200B; voeg VCL fragmenten &#x200B;](/help/assets/optimize-at-edge/add-vcl-snippets.png) toe

**vcl_recv fragment**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=true"; # required for cache key
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

>[!TAB  Akamai (BYOCDN) ]

**Edge optimaliseert BYOCDN - Akamai**

Het doel van deze configuratie is verzoeken van agentic gebruikersagenten aan de Edge te leiden optimaliseert dienst (`live.edgeoptimize.net` backend). Als u de configuratie wilt testen, zoekt u na de installatie naar de header `x-edgeoptimize-request-id` in de reactie.


**de volgende JSON-regel van de Manager JSON van het Bezit van Akamai leidt gebruikersagenten LLM naar Edge Optimize:**

De configuratie bevat de volgende stappen:

**1. Plaats verpletterend criteria (gebruiker-Agent aanpassing)**

![&#x200B; plaats verpletterend criteria &#x200B;](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Oorsprong en SSL-gedrag instellen**

![&#x200B; Vastgestelde Oorsprong en SSL gedrag &#x200B;](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Cachetoets instellen**

![&#x200B; vastgestelde Zeer belangrijke Variabele van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Caching Rules**

![&#x200B; Caching Regels &#x200B;](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Binnenkomende aanvraagheaders wijzigen**

![&#x200B; wijzigt Binnenkomende Kopballen van het Verzoek &#x200B;](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Binnenkomende antwoordheaders wijzigen**

![&#x200B; wijzigt Inkomende Kopballen van de Reactie &#x200B;](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Wijziging van cache-id**

![&#x200B; Verandering van identiteitskaart van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Site-failover**

![&#x200B; Failover van de Plaats &#x200B;](/help/assets/optimize-at-edge/akamai-step8-failover.png)

![&#x200B; Gedrag Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step8-failover-behaviors.png)

![&#x200B; Regels Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step8-failover-rules.png)

![&#x200B; Reactie van het Gedrag &#x200B;](/help/assets/optimize-at-edge/akamai-step8-behaviors-response.png)

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

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

De [&#x200B; Adobe LLM Optimizer: Is uw webpagina citeerbaar?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) De Chrome-extensie toont hoeveel van uw webpagina-inhoud LLM&#39;s kunnen benaderen en wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie.

Met één klik kunt u de gereedschapsleesbaarheid van elke site evalueren. U kunt een vergelijking naast elkaar bekijken van wat AI agenten tegenover zien wat menselijke gebruikers zien, en schatten hoeveel inhoud door LLM Optimizer kon worden teruggekregen. Zie [&#x200B; AI uw website lezen?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) voor meer informatie.

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

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

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

Wij dienen de geoptimaliseerde versie van de pagina van geheim voorgeheugen zolang de onderliggende bronpagina niet is veranderd. Wanneer de bron echter wel verandert, wordt ons systeem automatisch vernieuwd, zodat AI-agents altijd de meest actuele inhoud ontvangen. Dit komt doordat we de FLV-instellingen (in volgorde van minuten) gebruiken om een lage cache op te slaan, zodat bij elke update van de inhoud op uw site een nieuwe optimalisatie binnen dat venster wordt geactiveerd. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

V. Is Optimize bij Edge alleen voor sites die gebruikmaken van Adobe Edge Delivery Service (EDS)?

Nee. Optimaliseren in Edge is niet alleen CDN-agnostisch en werkt met elke front-end architectuur, maar ook met de architectuur die op Adobe EDS Stack wordt geïmplementeerd.

V. Hoe wordt Optimaliseren bij Edge-pre-rendering anders dan bij traditionele rendering op de server?

Beide problemen lossen verschillende problemen op en kunnen samenwerken. Traditionele SSR rendert inhoud aan serverzijde maar omvat geen inhoud die later in browser wordt geladen. Optimaliseren bij voorrendering van Edge legt de pagina vast nadat JavaScript en client-side gegevens zijn geladen, waardoor de volledig geassembleerde versie aan de CDN-rand wordt geproduceerd. SSR richt zich op het verbeteren van de menselijke ervaring en Optimize in Edge verbetert de webervaring voor LLMs.
