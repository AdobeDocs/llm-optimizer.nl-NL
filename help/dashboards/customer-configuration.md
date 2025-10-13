---
title: Klantconfiguratie
description: Gebruik de configuratie van de klant om te bepalen hoe uw merk binnen het optimaliseringsplatform LLM wordt gecontroleerd en geanalyseerd.
source-git-commit: a699f8f3c50f77d07f29cd354fd1ef8e6eed8ff9
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%

---


# Klantconfiguratie {#customer-configuration}

Het Klantconfiguratiedashboard is een krachtig hulpmiddel dat inzicht biedt in de zichtbaarheid van uw merk in LLM&#39;s. Door correct opstellingscategorieën, onderwerpen, herinneringen, en concurrenten, kunt u ervoor zorgen uw merk goed wordt geplaatst om in LLM-Gegenereerde reacties te verschijnen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

![&#x200B; Dashboard van de Configuratie van de Klant &#x200B;](/help/dashboards/assets/customer-config.png)

Als u wilt configureren hoe LLM Optimizer uw aanwezigheid van uw merk controleert en analyseert op verschillende markten en in concurrerende landschappen, hebt u toegang tot de volgende tabbladen:

* [Categorieën](#categories)
* [Concurrentietracering](#competitor-tracking)
* [Merkaliassen](#brand-aliases)
* [Gegevens-inzichten](#data-insights)
* [CDN-configuratie](#agentic-cdn)

>[!IMPORTANT]
>
> Voor meer details op hoe te opstelling zien uw categorieën, onderwerpen, herinneringen, en concurrenten [&#x200B; Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen, en concurrenten &#x200B;](/help/overview/best-practices-topics-prompts.md) pagina.

## Categorieën {#categories}

Vanuit het tabblad Categorieën kunt u bedrijfscategorieën of productlijnen definiëren die u wilt bijhouden en deze aan specifieke gebieden koppelen. Over het algemeen heeft het tabblad Categorieën betrekking op bijna elke andere aanpassing op deze pagina, omdat categorieën in het categorieveld worden weergegeven voor de andere aanpassingen (het bijhouden van concurrenten, aliassen enzovoort). Een nieuwe categorie toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, voeg de **Naam van de Categorie** toe.
3. Pas het **Verwante Gebied** aan waar de categorie zal worden gecontroleerd.
4. Klik **sparen** en de nieuwe categorie zal op de categorielijst verschijnen.

Het toevoegen van nieuwe categorieën zal automatisch geen onderwerpen en herinneringen produceren - deze zullen manueel van de [&#x200B; Inzichten van Gegevens &#x200B;](#data-insights) tabel moeten worden toegevoegd.

Als u een categorie wilt verwijderen, klikt u op het pictogram Verwijderen in de categorielijst. Wees voorzichtig, omdat **het schrappen van een categorie ook de bijbehorende punten** als concurrenten zal schrappen u opstelling of merkaliassen zou kunnen hebben die met die specifieke categorie verbonden zijn.

## Concurrentietracering {#competitor-tracking}

Door het volgen van concurrenten te gebruiken, kunt u volgen hoe uw concurrenten met betrekking tot uw merk in verschillende categorieën en regio&#39;s worden vermeld. Controleer hun aanwezigheid en prestaties in uw marktsegmenten. Het bijhouden van concurrenten aanpassen:

1. Om een nieuwe concurrent toe te voegen, klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Voeg de naam van de concurrent toe.
4. Pas indien nodig de Alias en Domains van de concurrent aan.
5. Klik **sparen** en de nieuwe concurrent zal op de mededingerslijst verschijnen.

Als u een concurrent wilt verwijderen, klikt u op het verwijderpictogram in de lijst met concurrenten.

## Merkaliassen {#brand-aliases}

Door merkaliassen te gebruiken, kunt u alternatieve namen en variaties van uw merk vormen die over verschillende categorieën en gebieden zouden moeten worden gevolgd. Dit zorgt voor een uitgebreide controle op alle merkvermeldingen. Een merkalias toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Selecteer het **Gebied** waar alias zal worden gecontroleerd.
4. Voeg de merkalias toe.
5. Klik **sparen** en merkalias zal op de lijst verschijnen.

Als u een merkalias wilt verwijderen, klikt u op het verwijderpictogram in de lijst met aliassen.

## Gegevens-inzichten {#data-insights}

Op dit tabblad kunt u vragen controleren, beheren en aanpassen. U kunt de gegevensinzichten van de Aanwezigheid van de a [&#x200B; &#x200B;](/help/dashboards/brand-presence.md#data-insights) .csv uploaden en de lijst met herinneringen en onderwerpen van die analyse worden bevolkt. U kunt onderwerpen en hun bijbehorende herinneringen ook schrappen wijzigen en toevoegen zoals nodig.

Als u een CSV-bestand met gegevensinzichten wilt importeren, moet u eerst een bestand exporteren vanaf het dashboard Handaanwezigheid. Zie de [&#x200B; gegevensinzichten &#x200B;](/help/dashboards/brand-presence.md#data-insights) sectie leren hoe te om dat te doen. Zodra u het bestand hebt:

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

![&#x200B; Klantenconfiguratie CDN &#x200B;](/help/overview/assets/cc-cdn.png)

Op het **Aan boord CDN Providervenster**:

1. Selecteer uw CDN-provider (bijvoorbeeld Akamai, snel door Adobe beheerd, AWS Cloudfront, Azure CDN, Cloudflare of Overige).
2. Klik **Onboard** om logboek toe te laten door:sturen.

Als u **Andere** selecteert, zult u aan Adobe voor hulp moeten bereiken.
