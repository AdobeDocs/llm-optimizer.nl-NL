---
title: Optimalisatiemogelijkheden
description: Leer hoe u het opportuniteitsdashboard kunt gebruiken om automatisch te bepalen hoe uw site kan worden verbeterd om de zichtbaarheid van uw merk te verhogen.
feature: Opportunities
source-git-commit: 33196139fef1cebd47b15aa964df2bac366ea12a
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Optimalisatiemogelijkheden

Optimalisatiemogelijkheden zijn automatisch gedetecteerde inzichten die laten zien waar uw site en externe aanwezigheid kunnen worden verbeterd om de zichtbaarheid van uw merk in AI-zoekopdrachten te vergroten.

Deze optimalisaties omvatten correcties op pagina&#39;s (het toevoegen van gestructureerde inhoud, chemicaliën, of samenvattingen), technische aanpassingen (het ontgrendelen van AI-crawlers of het oplossen van fouten) en het beïnvloeden van inhoud op gezaghebbende plaatsen van derden. Door deze optimalisatiemogelijkheden aan te pakken, kan uw merk nauwkeurig worden weergegeven en kan het waarschijnlijker worden genoemd in generatieve reacties.

![&#x200B; de kansen van de Optimalisering &#x200B;](/help/dashboards/assets/oport.png)

## Opportunity-dashboard

De optimalisatiemogelijkheden die op het dashboard worden voorgesteld worden voorrang gegeven gebaseerd op spelerhiaten, trending onderwerpen, en prestatiesgegevens en voorgesteld als lijst. U kunt naar een bepaalde kans zoeken door het onderzoeksgebied te gebruiken. Bovendien worden de kansen gegroepeerd op labels en kunt u rechtstreeks op een tag klikken om alle kansen weer te geven die onder die tag zijn gegroepeerd.

Het klikken **Details** zal een afzonderlijk venster openen waar meer informatie en extra begeleiding wordt verstrekt.

## Ondersteunde mogelijkheden

Hieronder ziet u een tabel met momenteel ondersteunde mogelijkheden:

| Opportunity | Type | Geïdentificeerde problemen | Suggesties corrigeren |
|---------|----------|----------|----------|
| Lange alinea&#39;s weergeven | Inhoud (onsite) | Detecteert alinea&#39;s die de aanbevolen lengtedrempels overschrijden. Hiermee worden beïnvloede URL&#39;s en grote tekstfragmenten weergegeven. | Maak abstracts of deel lange tekst op in kortere, scannbare gedeelten. |
| Gestructureerde inhoud (veelgestelde vragen) aanbevelen | Inhoud (onsite) | Detecteert prompt met hoge populariteit zonder overeenkomende FAQ-items. Toont verwante herinneringen, categorieën, en beïnvloede URLs. | Voeg de schemablokken van FAQ met beknopte antwoorden toe om gemeenschappelijke vragen aan te passen. |
| Geblokkeerd agentschapsverkeer detecteren | Technische GEO | Analyseert CDN-logboeken voor geblokkeerde aanvragen van bekende AI-agents (bijvoorbeeld GPTBot, PerplexityBot). Rapporten beïnvloedden URLs en agenten. | Werk robots.txt bij of server vormt om toegang voor gesteunde AI kruiplers toe te staan waar aangewezen. |
| 404s / 403s / 5xx problemen detecteren | Technische GEO | Controleert CDN-logboeken op foutreacties. Meldt frequentie, beïnvloedde URLs, en geschatte verloren treffers. | Los verbroken koppelingen op, werk machtigingen bij en los problemen op de server op, zodat met de belangrijkste inhoud 200 reacties worden geretourneerd. |
| Zichtbaarheid van inhoud herstellen (vroege toegang) | Technische GEO | Hiermee markeert u pagina&#39;s waar kritieke inhoud wordt verborgen voor AI-agents. Hiermee worden beïnvloede URL&#39;s en verwachte inhoud weergegeven die kunnen worden hersteld. | Geef de pagina&#39;s vooraf weer, zodat er meer inhoud beschikbaar is voor AI-agents zonder JavaScript-uitvoering. |

## Automatische optimalisatie {#auto-optimization}

Dankzij automatische optimalisatie kunt u met één muisklik aanbevolen optimalisaties implementeren, waardoor de handmatige inspanning en de tijd tot waarde worden beperkt. Optimalisaties kunnen worden toegepast bij de inhoudsbron of bij de CDN-rand. Op Edge gebaseerde automatische optimalisatie is momenteel beschikbaar in Vroege Toegang voor bepaalde mogelijkheden. Voor meer details, zie [&#x200B; optimaliseren bij Edge &#x200B;](/help/dashboards/optimize-at-edge/overview.md) pagina.

<!--### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.-->

### Extra gereedschappen

De [&#x200B; LLM zichtcontrole &#x200B;](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) is een uitbreiding van Chrome die u precies laat zien hoeveel van uw inhoud LLMs van de webpagina kan toegang hebben en ook wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie. Met een enkele klik kunnen gebruikers de gereedschapsleesbaarheid van elke site evalueren, een vergelijking naast elkaar weergeven van wat AI-agents zien in vergelijking met wat menselijke gebruikers zien. Bovendien wordt geschat hoeveel inhoud kan worden hersteld door LLM Optimizer te gebruiken.

<!--| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |-->
