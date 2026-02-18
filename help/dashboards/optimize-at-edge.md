---
title: Optimaliseren bij Edge
description: Leer hoe u optimalisaties in LLM Optimizer kunt leveren aan de CDN-rand zonder dat er ontwerpwijzigingen nodig zijn.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '2172'
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

Om het opstellingsproces te begeleiden, selecteer hieronder uw leverancier CDN en volg de overeenkomstige configuratiegids. Houd er rekening mee dat deze voorbeelden moeten worden aangepast aan de werkelijke live configuratie. We raden u aan eerst wijzigingen toe te passen in de lagere omgevingen.

### CDN-configuratiehulplijnen

| CDN-provider | Type | Hulplijn |
|---|---|---|
| AEM Cloud Service Managed CDN (snel) | Beheerd door Adobe | [&#x200B; de opstellingsgids van de Mening &#x200B;](/help/dashboards/optimize-at-edge-aem-managed-cdn.md) |
| Snel (BYOCDN) | Uw eigen CDN ophalen | [&#x200B; de opstellingsgids van de Mening &#x200B;](/help/dashboards/optimize-at-edge-fastly-byocdn.md) |
| Akamai (BYOCDN) | Uw eigen CDN ophalen | [&#x200B; de opstellingsgids van de Mening &#x200B;](/help/dashboards/optimize-at-edge-akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Uw eigen CDN ophalen | [&#x200B; de opstellingsgids van de Mening &#x200B;](/help/dashboards/optimize-at-edge-cloudflare-byocdn.md) |

>[!NOTE]
>Als uw CDN-provider hierboven niet wordt vermeld of als u uw domein of e-mail niet in de gebruikersinterface van LLM Optimizer vindt, bereikt u `llmo-at-edge@adobe.com` voor assistentie aan boord. Zodra de installatieconfiguraties zijn voltooid, kunt u suggesties voor Optimize bij de kansen van Edge in LLM Optimizer opstellen.

Elke CDN opstellingsgids hierboven omvat gedetailleerde verificatiestappen aan het eind om te bevestigen dat het agentische verkeer correct wordt verpletterd en dat het menselijke verkeer onaangetast blijft.

## Kansen

Deze tabel vindt u in de volgende tabel met mogelijkheden die de taalkundige webervaring kunnen verbeteren en die worden ondersteund met Optimaliseren in Edge.

| Opportunity | Type | Automatisch identificeren | Automatisch voorstellen | Automatisch optimaliseren |
|---------|----------|----------|----------|----------|
| Zichtbaarheid van inhoud herstellen | Technische GEO | Detecteert pagina&#39;s waarop kritieke inhoud van AI-agents wordt verborgen. Hiermee worden beïnvloede URL&#39;s en verwachte inhoud weergegeven die kunnen worden hersteld. | Hiermee wordt de inhoud gemarkeerd die beschikbaar kan worden gemaakt voor AI-agents en wordt aangeraden om pre-rendering voor deze pagina&#39;s in te schakelen. | Serveert een volledig teruggegeven, AI-vriendschappelijke momentopname van HTML aan zinloos verkeer dat de eerder verborgen inhoud terugkrijgt. |
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

We leveren de geoptimaliseerde versie van uw pagina vanuit cache zolang de onderliggende bronpagina niet is gewijzigd. Nochtans, wanneer de bron voor **verandert herstelt Zichtbaarheid van de Inhoud**, verandert ons systeem automatisch zodat ontvangen de AI agenten altijd de meest bijgewerkte inhoud. Dit komt doordat we de FLV-instellingen (in volgorde van minuten) gebruiken om een lage cache op te slaan, zodat bij elke update van de inhoud op uw site een nieuwe optimalisatie binnen dat venster wordt geactiveerd. Voor inhoudskansen zoals **voegt LLM-Vriendelijke Samenvattingen** toe, controleert LLM Optimizer de bronpagina voor veranderingen. Als een verandering wordt ontdekt, pauzeren wij de optimalisering en markeren het voor menselijk overzicht om inhoudsverschuiving tussen de agent-zichtbare pagina en mens-zichtbare pagina te verhinderen.
<!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

V. Is Optimize bij Edge alleen voor sites die gebruikmaken van Adobe Edge Delivery Service (EDS)?

Nee. Optimaliseren in Edge is niet alleen CDN-agnostisch en werkt met elke front-end architectuur, maar ook met de architectuur die op Adobe EDS Stack wordt geïmplementeerd.

V. Hoe wordt Optimaliseren bij Edge-pre-rendering anders dan bij traditionele rendering op de server?

Beide problemen lossen verschillende problemen op en kunnen samenwerken. Traditionele SSR rendert inhoud aan serverzijde maar omvat geen inhoud die later in browser wordt geladen. Optimaliseren bij voorrendering van Edge legt de pagina vast nadat JavaScript en client-side gegevens zijn geladen, waardoor de volledig geassembleerde versie aan de CDN-rand wordt geproduceerd. SSR richt zich op het verbeteren van de menselijke ervaring en Optimize in Edge verbetert de webervaring voor LLMs.

Q. wat gebeurt als ik optimalisaties voor sommige URLs in mijn domein maar niet allen opstel?

Alleen de URL&#39;s die u expliciet optimaliseert, worden gewijzigd. Voor URLs met opgestelde kansen, ontvangen de agenten AI de geoptimaliseerde versie. Voor URLs zonder opgezette kansen, onze dienst stelt eenvoudig de originele pagina voor zoals-is zonder veranderingen toe te passen of het op te slaan in onze laag van het optimalisatiecache. Op deze manier kunt u optimalisaties selectief implementeren zonder dat dit van invloed is op de rest van uw site.
