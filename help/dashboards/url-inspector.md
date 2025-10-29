---
title: URL-controle
description: Leer hoe u de URL-controle kunt gebruiken om te analyseren hoe specifieke pagina's op uw domein in AI-zoekopdrachten uitvoeren.
feature: URL Inspector
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# URL-controle

Met de URL-controle kunt u analyseren hoe specifieke pagina&#39;s op uw domein in AI-zoekopdrachten uitvoeren. Het combineert zicht, agentisch verkeer, en verwijzingsgegevens op het niveau URL om u een korrelige mening te geven van welke URLs wordt geciteerd en hoe vaak zij in reacties verschijnen.

![ Inspecteur URL ](/help/dashboards/assets/url-insp.png)

## Filters

Boven aan de pagina kunt u filters toepassen om de weergave te verfijnen. De filters u kiest zullen **alle** secties beïnvloeden huidig op het dashboard. U kunt het volgende aanpassen:

* **de Waaier van de Datum** - selecteer het tijdkader voor de getoonde gegevens. Bijvoorbeeld de laatste 4 weken. U hebt ook de optie om de tijdperiode aan te passen door de **optie van de Weken van de Douane te selecteren**.
* **Categorie** - filter de getoonde resultaten door categorieën.
* **Platform** - kies welke motor AI om te analyseren.
* **Type van Inhoud van de Pagina** - filter door type van inhoud.
* **Gebied** - filter de resultaten door geografie. Niet alle regio&#39;s zijn beschikbaar bij het starten.

Nadat u de gewenste filter selecteert, klik **toepassen Filters** om de selectie op het dashboard toe te passen.

## Overzichtsgegevens

De URL-controle bevat verschillende overzichtsmetriek, zodat u snel kunt beoordelen hoe uw pagina&#39;s in AI-zoekopdrachten worden uitgevoerd. De volgende cijfers worden verstrekt:

* **Unieke herinneringen met bezeten citaten** - het totale aantal unieke AI herinneringen met bezeten citaten.
* **Volledige unieke herinneringen** - het totale aantal unieke AI herinneringen.
* **Unieke geciteerde URLs** - het aantal unieke bezeten URLs die zijn aangehaald.
* **Totale tijden aangehaald** - Totale tijden een bezeten URL is geciteerd in door AI geproduceerde antwoorden.
* **Totale opvallende treffers** - het totale aantal klappen van AI agenten op uw URLs.
* **de treffers van de Verwijzing van LLMs** - het totale aantal klappen die van AI-Gegenereerde antwoorden aan uw URLs worden geleid.

De trendindicatoren voor elk overzichtsmetrisch tonen hoe deze waarden in tijd in vergelijking met de vorige periode veranderen.

## Je opgegeven URL&#39;s

In de weergave URL&#39;s waarnaar wordt verwezen, worden alle URL&#39;s van uw merk weergegeven die in door AI gegenereerde antwoorden zijn genoemd, met ondersteuning voor maatstaven. Beide lijsten hebben een onderzoeksgebied voor snelle toegang tot onderwerpen en u kunt aanpassen welke metriek wordt getoond door **te klikken vormt Kolommen** knoop. Ook, kunt u de **optie van de Uitvoer** gebruiken om lijst .csv te downloaden en de inzichten met uw team te delen of de lijst in uitvoerende rapportering te omvatten.

![ Bewerkte URLs ](/help/dashboards/assets/cited-urls.png)

De volgende cijfers worden verstrekt:

* **URL** - geanalyseerde URL.
* **Geciteerde Tijden** - het aantal tijden URL is geciteerd in AI-Gegenereerde antwoorden.
* **Herinneringen die in** worden vermeld - het aantal unieke AI herinneringen die URL citeren.
* **Categorieën** - de productcategorieën of onderwerpen verbonden aan URL.
* **Gebieden** - het geografische gebied waar URL werd geciteerd.
* **Agentische klappen** - het totale aantal klappen van AI agenten op URLs.
* **de treffers van de Verwijzing** - het aantal klappen die van AI-Gegenereerde antwoorden aan URLs worden geleid.

## Trending URLs concurrerende voor Cites

De trending URLs die voor citatiemening concurreren, benadrukt externe URLs die momenteel in antwoorden relevant voor uw merk worden genoemd, die meten wie citaten in uw ruimte wint. De gegevenslijst heeft een onderzoeksgebied voor snelle toegang tot specifieke URLs. Ook, kunt u de **optie van de Uitvoer** gebruiken om lijst .csv te downloaden en de inzichten met uw team te delen of de lijst in uitvoerende rapportering te omvatten.

![ het Trending URLs die voor Cites ](/help/dashboards/assets/trend-url.png) concurreren

De volgende cijfers worden verstrekt:

* **URL** - geanalyseerde URL
* **Type van Inhoud** - het type van inhoud (bezeten, sociale, verdiende, andere).
* **Geciteerde Tijden** - het aantal tijden URL is geciteerd in AI-Gegenereerde antwoorden.
* **Herinneringen die in** worden vermeld - het aantal unieke AI herinneringen die URL citeren.
* **Categorieën** - de productcategorieën of onderwerpen verbonden aan URL.
* **Gebieden** - het geografische gebied waar URL werd geciteerd.

### Venster Details

Voor zowel de geciteerde als trending meningen, heeft URLs a **Details** knoop aan het eind van elke rij. Als u op de knop klikt, wordt er een apart venster weergegeven met aanvullende gegevens. Het detailvenster toont hoe vaak URL wordt geciteerd, <!--the sentiment of AI responses where it is mentioned,--> de onderwerpen en herinneringen het binnen verschijnt, en tendensen in agentic en verwijzingsverkeer in tijd (voor bezeten URLs).

![ Venster van Details ](/help/dashboards/assets/details-url.png)
