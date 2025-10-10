---
title: Optimalisatiemogelijkheden
description: Dit is het artikeloverzicht.
source-git-commit: 8c38027e46b53d85776fffe17597883c742235d6
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# Optimalisatiemogelijkheden

Optimalisatiemogelijkheden zijn automatisch gedetecteerde inzichten die laten zien waar uw site en externe aanwezigheid kunnen worden verbeterd om de zichtbaarheid van uw merk in AI-zoekopdrachten te vergroten. Deze optimalisaties omvatten correcties op pagina&#39;s (het toevoegen van gestructureerde inhoud, chemicaliën, of samenvattingen), technische aanpassingen (het ontgrendelen van AI-crawlers of het oplossen van fouten) en het beïnvloeden van inhoud op gezaghebbende plaatsen van derden. Door deze optimalisatiemogelijkheden aan te pakken, kan uw merk nauwkeurig worden weergegeven en kan het waarschijnlijker worden genoemd in generatieve reacties.

![ de kansen van de Optimalisering ](/help/dashboards/assets/oport.png)

## Opportunity-dashboard

De optimalisatiemogelijkheden die op het dashboard worden voorgesteld worden voorrang gegeven gebaseerd op spelerhiaten, trending onderwerpen, en prestatiesgegevens en voorgesteld als lijst. U kunt naar een bepaalde kans zoeken door het onderzoeksgebied te gebruiken. Bovendien worden de kansen gegroepeerd op labels en kunt u rechtstreeks op een tag klikken om alle kansen weer te geven die onder die tag zijn gegroepeerd.

Het klikken **Details** zal een afzonderlijk venster openen waar meer informatie en extra begeleiding wordt verstrekt.

## Ondersteunde mogelijkheden

Hieronder ziet u een tabel met momenteel ondersteunde mogelijkheden:

| Opportunity | Type | Geïdentificeerde problemen | Suggesties corrigeren |
|---------|----------|----------|----------|
| Lange alinea&#39;s weergeven | Inhoud (onsite) | Detecteert alinea&#39;s die de aanbevolen lengtedrempels overschrijden. Hiermee worden beïnvloede URL&#39;s en grote tekstfragmenten weergegeven. | Maak abstracts of deel lange tekst op in kortere, scannbare gedeelten. |
| Gestructureerde inhoud (veelgestelde vragen) aanbevelen | Inhoud (onsite) | Detecteert prompt met hoge populariteit zonder overeenkomende FAQ-items. Toont verwante herinneringen, categorieën, en beïnvloede URLs. | Voeg de schemablokken van FAQ met beknopte antwoorden toe om gemeenschappelijke vragen aan te passen. |
| Ontbrekende Hreflang detecteren | Inhoud (onsite) | Op pagina&#39;s met markeringen ontbreken hreflang-kenmerken. Verstrekt beïnvloede URLs en verwachte dekking door taal/regio. | Voer hreflang-tags uit om de juiste gelokaliseerde versies aan te geven. |
| Ontbrekende chemische stoffen detecteren | Inhoud (onsite) | Scant naar pagina&#39;s zonder canonieke tags of met conflicterende tags. Hiermee geeft u gewijzigde URL&#39;s en duplicaten weer. | Voeg canonieke tags toe die naar de voorkeursversie van elke pagina verwijzen. Zorg voor consistent gebruik tussen verschillende varianten. |
| Lege koppen detecteren | Inhoud (onsite) | Hiermee markeert u pagina&#39;s met kopcodes, maar zonder tekst. Hiermee geeft u URL en locatie van lege tags weer. | Voeg beschrijvende tekst toe aan koppen die de onderliggende inhoud weerspiegelen. |
| Dubbele koppen zoeken | Inhoud (onsite) | Scant koptags van HTML en markeert herhaalde koppen. Hiermee worden beïnvloede URL&#39;s en gedupliceerde tekstfragmenten weergegeven. | Herzie rubrieken om uniek te zijn en hiërarchie te handhaven (H1 → H2 → H3). Dubbele secties samenvoegen of hernoemen. |
| Geblokkeerd agentschapsverkeer detecteren | Technische GEO | Analyseert CDN-logboeken voor geblokkeerde aanvragen van bekende AI-agents (bijvoorbeeld GPTBot, PerplexityBot). Rapporten beïnvloedden URLs en agenten. | Werk robots.txt bij of server vormt om toegang voor gesteunde AI kruiplers toe te staan waar aangewezen. |
| 404s / 403s / 5xx problemen detecteren | Technische GEO | Controleert CDN-logboeken op foutreacties. Meldt frequentie, beïnvloedde URLs, en geschatte verloren treffers. | Los verbroken koppelingen op, werk machtigingen bij en los problemen op de server op, zodat met de belangrijkste inhoud 200 reacties worden geretourneerd. |

### Zichtbaarheid van inhoud herstellen {#recover-contet}

Zoals hierboven vermeld, markeert de zichtbaarheid van de inhoud pagina&#39;s waar belangrijke inhoud voor AI-agents verloren gaat door weergave op de client. Voor elke geïdentificeerde pagina wordt precies aangegeven welke inhoud ontbreekt in de AI-agentweergave, zodat u de zichtbaarheidsverschillen kunt vaststellen. Het wordt ook ondersteund door een &#39;edge-based&#39; pre-rendering functie die meer HTML-inhoud kan leveren aan mobiel verkeer zonder dat wijzigingen in het Content Management System (CMS) vereist zijn. Gelieve te merken op dat dit vermogen momenteel in **Vroege Toegang** is en ook opstelling van het team vereist LLMO om geoptimaliseerde inhoudslevering toe te laten.

### Extra gereedschappen

De [ LLM zichtcontrole ](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) is een uitbreiding van Chrome die u precies laat zien hoeveel van uw inhoud LLMs van de webpagina kan toegang hebben en ook wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie. Met een enkele klik kunnen gebruikers de gereedschapsleesbaarheid van elke site evalueren, een vergelijking naast elkaar weergeven van wat AI-agents zien in vergelijking met wat menselijke gebruikers zien. Bovendien wordt geschat hoeveel inhoud kan worden hersteld door LLM Optimizer te gebruiken.
