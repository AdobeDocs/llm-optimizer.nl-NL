---
title: Agentic Traffic
description: Dit is het artikeloverzicht.
source-git-commit: f92ca3eaa81d05135c65df60267280314c6e2d6f
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# Agentic Traffic {#agentic-traffic}

Het dashboard van het Verkeer van de Agent toont u hoe de agenten van AI (kruipende agenten en praatbots) met uw plaats in wisselwerking staan. Met deze weergave kunt u het totale aantal aanvragen en algemene prestatiegerelateerde gegevens bijhouden. U kunt de distributie van verkeer over markten, categorieën, pagina&#39;s, en agenten ook bekijken. De gegevens die door dit dashboard worden gebruikt zijn afkomstig van de CDN- logboeken zodat moet u **CDN logboek vormen door:sturen** om metriek te tonen. Er zijn ook aanpasbare filters waarmee u de weergegeven gegevens kunt verfijnen.

Op deze pagina vindt u het volgende:

* [Filters](#filters)
* [CDN instellen](#cdn-setup)
* [Verkeersdistributie](#traffic-distribution)
* [Kantoorverkeer](#agentic-trends)
* [Boven- en onderomslagen](#top-bottom-movers)
* [Gebruikersagent en URL-prestatieanalyse](#user-url-performance)

## CDN instellen {#cdn-setup}

Bij de eerste aanmelding is het dashboard voor het verkeer voor de Agentic Traffic leeg. Om agentische interactie te bekijken, moet u **het logboek vormen CDN door:sturen**. **TBD punt aan CDN opstelling in snel begin/onboarding?**

![&#x200B; CDN Opstelling &#x200B;](/help/dashboards/assets/ag-log-forward.png)

1. Selecteer uw CDN-provider (bijvoorbeeld Akamai, snel door Adobe beheerd, AWS Cloudfront, Azure CDN, Cloudflare of Overige).
2. Voer een e-mail met primaire contactpersoon in.
3. Klik **Activering van het Verzoek** om logboek toe te laten door:sturen.

Zodra geactiveerd, worden de logboeken opgenomen en het dashboard zal met metriek zoals totale agenteninteractie, succestarief, klappen door markt, gebruikersagentenanalyse, en prestaties op URL-niveau bevolken.

## Filters {#filters}

Boven aan de pagina kunt u filters toepassen om de weergave te verfijnen. De filters u kiest zullen **alle** secties beïnvloeden huidig op het dashboard. U kunt het volgende aanpassen:

* **de Waaier van de Datum** - selecteer het tijdkader voor de getoonde gegevens. Bijvoorbeeld de laatste 4 weken. U hebt ook de optie om de tijdperiode aan te passen door de **optie van de Weken van de Douane te selecteren**.
* **Categorie** - filter de getoonde resultaten door vooraf bepaalde categorieën. U kunt douanecategorieën aan dit gebied (**SR** - ook toevoegen?).
* **Platform** - kies welke motor AI om te analyseren.
* **Type van Agent** - filter door het type van AI agent die met uw plaats in wisselwerking stond. U kunt filteren tussen krawlers, chatbots of alle agenten.
* **Tarief van het Succes** - filter door de interactiekwaliteit (hoog, middelgroot of laag). Deze metrisch vertegenwoordigt het percentage succesvolle HTTP- verzoeken, met inbegrip van zowel directe succesvolle reacties als omleidingen.
* **Type van Inhoud** - filter door inhoudstype, of HTML of txt.

Nadat u de gewenste filter selecteert, klik **toepassen Filters** om de selectie op het dashboard toe te passen.

## Verkeersdistributie {#traffic-distribution}

De mening van de Distributie van het Verkeer toont hoe het agentenverkeer over markten, categorieën, en paginatypen wordt verspreid. Als zodanig helpt deze weergave u te bepalen welke geografische gebieden, productgebieden of inhoudopmaak het vaakst door AI-agents worden benaderd tijdens de interactie met uw site.

![&#x200B; Distributie van het Verkeer &#x200B;](/help/dashboards/assets/ag-main.png)

Bovenaan op de pagina staan drie belangrijke meetgegevens waarmee u rekening moet houden:

* **Agentische interactie** - Deze metrisch vertegenwoordigt het totale aantal verzoeken die door agenten AI aan uw website worden gemaakt. Dit omvat al verkeer van onderzoeksmotoren, praatbots, en ander niet-menselijk verkeer.
* **het tarief van het Succes** - Deze metrisch vertegenwoordigt het percentage succesvolle HTTP- verzoeken, met inbegrip van zowel directe succesvolle reacties als omleidingen.
* **Gemiddelde TTFB** - tijd aan Eerste Byte (TTFB) meet de tijd het voor de eerste byte van gegevens neemt die van de server worden ontvangen. Lagere waarden geven snellere responstijden van de server aan.

Tendindicatoren voor elke metrische sleutel tonen hoe deze waarden in de loop der tijd veranderen ten opzichte van de vorige periode.

## Kantoorverkeer {#agentic-trends}

Gebruik de grafiek van de Trends van het Verkeer van het Agentschap om de wekelijkse totalen van succesvolle, ontbroken, en algemene klappen te volgen. Als dusdanig, kunt u veranderingen in agentenactiviteit en prestaties in tijd controleren. U kunt de muis ook boven het diagram houden om de gegevensevolutie over het wekelijkse tijdkader te zien.

![&#x200B; Agentic de Trends van het Verkeer &#x200B;](/help/dashboards/assets/ag-trends.png)

## Boven- en onderomslagen {#top-bottom-movers}

Deze twee metriek sorteren URLs als volgt:

* **Hoogste Bedekken** - URLs met de grootste toename in agentic verkeer van oudste aan nieuwste week.
* **Onderste Bedekken** - URLs met de grootste daling in agentic verkeer van oudste aan nieuwste week.

## Gebruikersagent en URL-prestatieanalyse {#user-url-performance}

De mening van de Analyse van de Prestaties van de Agent van de Gebruiker en URL verstrekt verdere gegevensuitsplitsingen op hoe kruiplers en praatbots met uw plaats in wisselwerking staan. Klik op de onderstaande tabbladen voor gedetailleerde beschrijvingen.

![&#x200B; Agent van de Gebruiker en de Analyse van Prestaties URL &#x200B;](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB  Analyse van de Agent van 0&rbrace; Gebruiker]

De lijst van de Analyse van de Agent van de Gebruiker verstrekt een verdeling van verkeer door paginatype en agententype (bijvoorbeeld, kruiplers tegenover chatbots). Op deze manier is het gemakkelijk te begrijpen welke AI-agents kruipen welke delen van uw site. Het bevat de volgende categorieën:

* **Type van Pagina** - het paginatype.
* **Type van Agent** - de AI agent die de pagina kruipt, of een kruipster of een praatbot.
* **Hits** - het totale aantal verzoeken die door AI agenten voor dat specifieke paginatype worden gemaakt.

U kunt de **optie van de Uitvoer** ook gebruiken om lijst.csv te downloaden en de agentenanalyse met uw team te delen of het in uitvoerende rapportering te omvatten.

>[!TAB  URL de Analyse van Prestaties ]

De lijst van de Analyse van Prestaties URL toont een gedetailleerde mening van individuele URLs. Dit omvat treffers, unieke agenten, hoogste agent, succespercentages, en categorieën. Op deze manier kunt u hoogwaardige pagina&#39;s identificeren, tussenruimten zoeken en inhoud voor AI-engines optimaliseren. De URL&#39;s worden gerangschikt op verkeersvolume. De tabel bevat de volgende categorieën:

* **URL** - onderzochte URL.
* **Totale Hits** - Totaal aantal verzoeken die door AI agenten aan URL worden gemaakt.
* **Unieke Agenten** - het aantal verschillende AI agenten die tot URL toegang hadden.
* **Hoogste Agent** - de AI agent die het meeste verkeer aan URL produceerde.
* **Hoogste Type van Agent** - het type van de AI agent die het meeste verkeer aan dit URL produceerde.
* **Tarief van het Succes** - het percentage succesvolle HTTP- verzoeken, met inbegrip van zowel directe succesvolle reacties als omleidingen.
* **Categorie** - de categorie die het meest de inhoud van uw pagina aanpast.

De tabel met URL-prestaties heeft een zoekveld voor snelle toegang tot URL&#39;s. Ook, kunt u de **optie van de Uitvoer** gebruiken om lijst .csv te downloaden en de inzichten met uw team te delen of de lijst in uitvoerende rapportering te omvatten.

>[!ENDTABS]
