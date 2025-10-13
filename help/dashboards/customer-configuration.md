---
title: Klantconfiguratie
description: Gebruik de configuratie van de klant om te bepalen hoe uw merk binnen het optimaliseringsplatform LLM wordt gecontroleerd en geanalyseerd.
source-git-commit: a37c4e7d2e26f16dc10dc7bc39ba58ba1df77cd5
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---


# Klantconfiguratie {#customer-configuration}

Het Klantconfiguratiedashboard is een krachtig hulpmiddel dat inzicht biedt in de zichtbaarheid van uw merk in LLM&#39;s. Door categorieën, onderwerpen en herinneringen correct op te zetten, kunt u ervoor zorgen dat uw merk goed gepositioneerd is om in LLM-Gegenereerde reacties te verschijnen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

![ Dashboard van de Configuratie van de Klant ](/help/dashboards/assets/customer-config.png)

Als u wilt configureren hoe LLM Optimizer uw aanwezigheid van uw merk controleert en analyseert op verschillende markten en in concurrerende landschappen, hebt u toegang tot de volgende tabbladen:

* [Categorieën](#categories)
* [Overige bijhouden](#others-tracking)
* [Merkaliassen](#brand-aliases)
* [Gegevens-inzichten](#data-insights)
* [CDN-configuratie](#agentic-cdn)

>[!IMPORTANT]
>
> Voor meer details op hoe te opstelling zien uw categorieën, onderwerpen, herinneringen de [ Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen ](/help/overview/best-practices-topics-prompts.md) pagina.

## Categorieën {#categories}

Vanuit het tabblad Categorieën kunt u bedrijfscategorieën of productlijnen definiëren die u wilt bijhouden en deze aan specifieke gebieden koppelen. Over het geheel genomen heeft het tabblad Categorieën betrekking op bijna elke andere aanpassing op deze pagina, omdat categorieën in het categorieveld worden weergegeven voor de andere aanpassingen (andere bijhouden, aliassen enzovoort). Een nieuwe categorie toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, voeg de **Naam van de Categorie** toe.
3. Pas het **Verwante Gebied** aan waar de categorie zal worden gecontroleerd.
4. Klik **sparen** en de nieuwe categorie zal op de categorielijst verschijnen.

Het toevoegen van nieuwe categorieën zal automatisch geen onderwerpen en herinneringen produceren - deze zullen manueel van de [ Inzichten van Gegevens ](#data-insights) tabel moeten worden toegevoegd.

Als u een categorie wilt verwijderen, klikt u op het pictogram Verwijderen in de categorielijst. Wees voorzichtig, omdat **het schrappen van een categorie ook de bijbehorende punten** als merkaliassen zal schrappen die met die specifieke categorie verbonden zijn.

## Overige bijhouden {#others-tracking}

Op dit tabblad kunt u bijhouden hoe uw andere namen worden vermeld ten opzichte van uw merk in verschillende categorieën en regio&#39;s. Controleer hun aanwezigheid en prestaties in uw marktsegmenten. Tekstspatiëring aanpassen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Voeg de naam van de ander toe.
4. Pas indien nodig de andere alias en domeinen aan.
5. Klik **sparen**.

Als u een item uit de lijst wilt verwijderen, klikt u op het pictogram Verwijderen.

## Merkaliassen {#brand-aliases}

Door merkaliassen te gebruiken, kunt u alternatieve namen en variaties van uw merk vormen die over verschillende categorieën en gebieden zouden moeten worden gevolgd. Dit zorgt voor een uitgebreide controle op alle merkvermeldingen. Een merkalias toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Selecteer het **Gebied** waar alias zal worden gecontroleerd.
4. Voeg de merkalias toe.
5. Klik **sparen** en merkalias zal op de lijst verschijnen.

Als u een merkalias wilt verwijderen, klikt u op het verwijderpictogram in de lijst met aliassen.

## Gegevens-inzichten {#data-insights}

Op dit tabblad kunt u vragen controleren, beheren en aanpassen. U kunt de gegevensinzichten van de Aanwezigheid van de a [ ](/help/dashboards/brand-presence.md#data-insights) .csv uploaden en de lijst met herinneringen en onderwerpen van die analyse worden bevolkt. U kunt onderwerpen en hun bijbehorende herinneringen ook schrappen wijzigen en toevoegen zoals nodig.

Als u een CSV-bestand met gegevensinzichten wilt importeren, moet u eerst een bestand exporteren vanaf het dashboard Handaanwezigheid. Zie de [ gegevensinzichten ](/help/dashboards/brand-presence.md#data-insights) sectie leren hoe te om dat te doen. Zodra u het bestand hebt:

1. Op het dashboard, klik **uploadt CSV**.
2. In het venster Gegevens importeren sleept u het bestand en zet u het neer of kiest u het bestand handmatig.
3. Klik **uploadt Gegevens**.

U kunt een nieuw Csv- dossier ook tot stand brengen door het malplaatje van het **venster van de Inzichten van Gegevens van de Invoer** te downloaden. Zodra u het malplaatje hebt, open het en input uw onderwerpen samen met hun bijbehorende herinneringen, categorieën, en gebieden elk in een nieuwe lijn.

Bovendien kunt u onderwerpen/herinneringen aan de lijst onafhankelijk van een Csv- dossier ook toevoegen. Hiervoor moet u op het dashboard:

1. Klik **toevoegen Onderwerp** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Voer de onderwerpnaam in.
4. Voeg de snelle tekst toe.
5. Selecteer het gebied.
6. Klik **toevoegen Vragen** en het onderwerp met de herinnering zal op de lijst verschijnen.

>[!NOTE]
>Nieuw toegevoegde herinneringen zullen niet in MerkAanwezigheid verschijnen tot de verwerking volledig is.

Voor de lijst, kunt u elk onderwerp klikken en de bijbehorende herinnering(en) zullen verschijnen, om het onderwerp en zijn bijbehorende herinneringen te schrappen, klik het schrappingspictogram van de lijst.

## CDN-configuratie {#cdn-configuration}

Vanuit dit tabblad kunt u uw CDN-streams configureren, zodat Adobe LLM Optimizer uw CDN-gegevens kan analyseren. Deze gegevens worden gebruikt om dashboards (zoals het Verkeer van de Agentica), die inzicht in verkeerspatronen, prestatiesmetriek, en optimaliseringskansen verstrekken te aandrijven. Aan boord van uw leverancier CDN, klik **Op boord CDN**.

![ Klantenconfiguratie CDN ](/help/overview/assets/cc-cdn.png)

Op het **Aan boord CDN Providervenster**:

1. Selecteer uw CDN-provider.
2. Klik **Onboard** om logboek toe te laten door:sturen.

Als u **Andere** selecteert, zult u aan Adobe voor hulp moeten bereiken.
