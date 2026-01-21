---
title: Agentic Traffic
description: Leer hoe te om het dashboard van het Verkeer van de Agent te gebruiken om te zien hoe de agenten van AI met uw plaats in wisselwerking staan.
feature: Agentic Traffic
source-git-commit: a75ce71dc0ab9ffe7956a3dbd09dca23ea5f7096
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---


# Agentic Traffic {#agentic-traffic}

Het dashboard van het Verkeer van de Agentic toont hoe de agenten van AI (kruipende agenten en praatbots) met uw plaats in wisselwerking staan. Met deze weergave kunt u het totale aantal aanvragen en algemene prestatiegegevens bijhouden. U kunt de distributie van verkeer over markten, categorieën, pagina&#39;s, en agenten ook bekijken. De gegevens die door dit dashboard worden gebruikt zijn afkomstig van de CDN- logboeken zodat moet u **CDN logboek vormen door:sturen** om metriek te tonen. Er zijn ook aanpasbare filters waarmee u de weergegeven gegevens kunt verfijnen.

![ Distributie van het Verkeer ](/help/dashboards/assets/ag-main.png)

Op deze pagina vindt u het volgende:

* [Filters](#filters)
* [CDN instellen](#cdn-setup)
* [Verkeersdistributie](#traffic-distribution)
* [Kantoorverkeer](#agentic-trends)
* [Boven- en onderomslagen](#top-bottom-movers)
* [Gebruikersagent en URL-prestatieanalyse](#user-url-performance)

## CDN-logboek doorsturen {#cdn-setup}

Zonder **CDN logboek door:sturen**, is het Agentic dashboard van het Verkeer leeg. Om agentische interactie te bekijken, moet u **het logboek vormen CDN door:sturen**.  Bij de eerste aanmelding wordt een bericht weergegeven zoals in de onderstaande afbeelding wordt getoond.

![ CDN Opstelling ](/help/dashboards/assets/ag-log-forward1.png)

Selecteer **gaan naar Configuratie** en u zult automatisch aan de **CDN Configuratie** tabel van het [ dashboard van de klantenconfiguratie ](/help/dashboards/customer-configuration.md) navigeren.

![ CDN Opstelling Onboard ](/help/dashboards/assets/ag-log-forward2.png)

Op dit lusje, uitgezochte **Onboard CDN**. En het CDN leveranciersvenster wordt getoond.

<!-- [CDN Provider](/help/dashboards/assets/ag-log-forward3.png)-->
Op het **Aan boord CDN Providervenster**:

1. Selecteer uw CDN-provider (bijvoorbeeld Akamai, snel door Adobe beheerd, AWS Cloudfront, Azure CDN, Cloudflare of Overige).
2. Klik **Onboard** om logboek toe te laten door:sturen.

Als u **Andere** selecteert, zult u uit aan llmo-now@adobe.com voor hulp moeten bereiken.

Zodra geactiveerd, worden de logboeken opgenomen en het dashboard zal met metriek zoals totale agenteninteractie, succestarief, klappen door markt, gebruikersagentenanalyse, en prestaties op URL-niveau bevolken.

LLM Optimizer verwerkt een subset met velden uit de CDN-logboeken. Hoewel de ruwe namen van het logboekgebied door leverancier CDN variëren, worden zij genormaliseerd en voorgesteld als:

* URL (alleen pad)
* Gebruikersagent
* Statuscode
* Refererenkop
* Hostkop
* Tijd naar eerste byte (TTFB)
* Aanvraagmethode
* Tijdstempel
* Inhoudstype

Deze genormaliseerde velden worden weergegeven via de hoekweergave. Op het [ dashboard van het Verkeer van 0} Referral {, worden de logboeken CDN gebruikt om de metriek van de paginascheiding te tonen. ](/help/dashboards/referral-traffic.md) Er wordt geen persoonlijk identificeerbare informatie (PII) verwerkt of opgeslagen in een stadium van CDN-logopname of daaropvolgende gegevensverwerking.

## Filters {#filters}

Boven aan de pagina kunt u filters toepassen om de weergave te verfijnen. De filters u kiest zullen **alle** secties beïnvloeden huidig op het dashboard. U kunt het volgende aanpassen:

* **de Waaier van de Datum** - selecteer het tijdkader voor de getoonde gegevens. Bijvoorbeeld de laatste 4 weken. U hebt ook de optie om de tijdperiode aan te passen door de **optie van de Weken van de Douane te selecteren**.
* **Categorie** - filter de getoonde resultaten door vooraf bepaalde categorieën of douanecategorieën.
* **Platform** - kies welke motor AI om te analyseren.
* **Type van Agent** - filter door het type van AI agent die met uw plaats in wisselwerking stond. U kunt filteren tussen krawlers, chatbots of alle agenten.
* **Tarief van het Succes** - filter door de interactiekwaliteit (hoog, middelgroot of laag). Deze metrische waarde vertegenwoordigt het percentage geslaagde HTTP-aanvragen, inclusief zowel directe en geslaagde antwoorden (statuscodes 2xx) als omleidingen (statuscodes 3xx).
* **Type van Inhoud** - bekijk agentic interactie voor verschillende inhoudstypes, zoals HTML, PDF etc.

Nadat u de gewenste filter selecteert, klik **toepassen Filters** om de selectie op het dashboard toe te passen.

## Verkeersdistributie {#traffic-distribution}

De mening van de Distributie van het Verkeer toont hoe het agentenverkeer over markten, categorieën, en paginatypen wordt verspreid. Als zodanig helpt deze weergave u te bepalen welke geografische gebieden, productgebieden of inhoudopmaak het vaakst door AI-agents worden benaderd tijdens de interactie met uw site.

![ Distributie van het Verkeer ](/help/dashboards/assets/ag-main.png)

Bovenaan op de pagina staan drie belangrijke meetgegevens waarmee u rekening moet houden:

* **Agentische interactie** - Deze metrisch vertegenwoordigt het totale aantal verzoeken die door agenten AI aan uw website worden gemaakt. Dit omvat al verkeer van onderzoeksmotoren, praatbots, en ander niet-menselijk verkeer.
* **het tarief van het Succes** - Deze metrisch vertegenwoordigt het percentage succesvolle HTTP- verzoeken, met inbegrip van zowel directe succesvolle reacties als omleidingen.
* **Gemiddelde TTFB** - tijd aan Eerste Byte (TTFB) meet de tijd het voor de eerste byte van gegevens neemt die van de server worden ontvangen. De gemiddelde waarde wordt gewogen op basis van het aantal aanvragen dat elke code retourneert en sluit aanvragen uit die tot 5xx reacties hebben geleid. Lagere waarden geven snellere responstijden van de server aan.

Tendindicatoren voor elke metrische sleutel tonen hoe deze waarden in de loop der tijd veranderen ten opzichte van de vorige periode.

## Kantoorverkeer {#agentic-trends}

Gebruik de grafiek van de Trends van het Verkeer van het Agentschap om de wekelijkse totalen van succesvolle, ontbroken, en algemene klappen te volgen. Als dusdanig, kunt u veranderingen in agentenactiviteit en prestaties in tijd controleren. U kunt de muis ook boven het diagram houden om de gegevensevolutie over het wekelijkse tijdkader te zien.

![ Agentic de Trends van het Verkeer ](/help/dashboards/assets/ag-trends.png)

## Boven- en onderomslagen {#top-bottom-movers}

In de weergave Boven en Onder omslagen worden URL&#39;s gemarkeerd met de grootste week-over-week wijzigingen in het verkeer van personen: bezoeken of hits van AI-systemen die toegang hebben tot uw inhoud. **Bovenste Bedekken** toont pagina&#39;s die zicht of overeenkomst bereiken, terwijl **Onderste Bedekken** URLs met de steepste ontleedingen onthult. Zo kunt u snel vaststellen welke inhoud naar boven buigt, wat aandacht nodig kan hebben en waar door AI gestuurde detectiepatronen verschuiven.

![ Hoogste en Onderste Bedekken ](/help/dashboards/assets/movers.png)

## Gebruikersagent en URL-prestatieanalyse {#user-url-performance}

De mening van de Analyse van de Prestaties van de Agent van de Gebruiker en URL verstrekt verdere gegevensuitsplitsingen op hoe kruiplers en praatbots met uw plaats in wisselwerking staan. Klik op de onderstaande tabbladen voor gedetailleerde beschrijvingen.

![ Agent van de Gebruiker en de Analyse van Prestaties URL ](/help/dashboards/assets/user-agent.png)

>[!BEGINTABS]

>[!TAB  Analyse van de Agent van 0} Gebruiker]

De lijst van de Analyse van de Agent van de Gebruiker verstrekt een verdeling van verkeer door paginatype en agententype (bijvoorbeeld, kruiplers tegenover chatbots). Op deze manier is het gemakkelijk te begrijpen welke AI-agents kruipen welke delen van uw site. Het bevat de volgende categorieën:

* **Type van Pagina** - het paginatype.
* **Type van Agent** - de AI agent die de pagina kruipt, of een kruipster of een praatbot.
* **Hits** - het totale aantal verzoeken die door AI agenten voor dat specifieke paginatype worden gemaakt.

U kunt aanpassen welke metriek door te klikken **wordt getoond Kolommen** knoop vormen.

>[!TAB  URL de Analyse van Prestaties ]

De lijst van de Analyse van Prestaties URL toont een gedetailleerde mening van individuele URLs. Dit omvat treffers, unieke agenten, hoogste agent, succespercentages, en categorieën. Op deze manier kunt u hoogwaardige pagina&#39;s identificeren, tussenruimten zoeken en inhoud voor AI-engines optimaliseren. De URL&#39;s worden gerangschikt op verkeersvolume. De tabel bevat de volgende categorieën:

* **URL** - onderzochte URL.
* **Totale Hits** - Totaal aantal verzoeken die door AI agenten aan URL worden gemaakt.
* **Unieke Agenten** - het aantal verschillende AI agenten die tot URL toegang hadden.
* **Hoogste Agent** - de AI agent die het meeste verkeer aan URL produceerde.
* **Hoogste Type van Agent** - het type van de AI agent die het meeste verkeer aan dit URL produceerde.
* **Tarief van het Succes** - het percentage succesvolle HTTP- verzoeken, met inbegrip van zowel directe succesvolle reacties als omleidingen.
* **Categorie** - de categorie die het meest de inhoud van uw pagina aanpast.
* **Gemiddelde TTFB (ms)** - tijd aan Eerste Byte (TTFB) meet de tijd het voor de eerste byte van gegevens neemt die van de server (in milliseconden) moeten worden ontvangen. De gemiddelde waarde wordt gewogen op basis van het aantal aanvragen dat elke code retourneert en sluit aanvragen uit die tot 5xx reacties hebben geleid. Lagere waarden geven snellere responstijden van de server aan.
* **Codes van de Reactie** - de de statuscodes van HTTP die voor URL worden waargenomen.

De URL prestatieslijst heeft een onderzoeksgebied voor snelle toegang tot URLs en u kunt aanpassen welke metriek wordt getoond door **te klikken vormt Kolommen** knoop. U kunt extra details voor elke URL ook bekijken door op het **pictogram van Details** aan het eind van elke rij te klikken.

![ details URL ](/help/dashboards/assets/details.png)

De weergave URL-details biedt een holistisch inzicht in de prestaties van een pagina, waarbij wordt getoond hoe vaak deze wordt genoemd, het gevoel van AI-reacties op de plaats waar deze wordt genoemd, de onderwerpen en aanwijzingen waarin deze wordt weergegeven en trends in het agonische en verwijzingsverkeer in de loop van de tijd.

>[!ENDTABS]

Op beide lijsten, kunt u de **Uitvoer** optie gebruiken om lijst .csv te downloaden en de inzichten met uw team te delen of de lijsten in uitvoerende rapportering te omvatten.
