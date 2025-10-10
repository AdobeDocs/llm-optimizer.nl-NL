---
title: Klantconfiguratie
description: Gebruik de configuratie van de klant om te bepalen hoe uw merk binnen het optimaliseringsplatform LLM wordt gecontroleerd en geanalyseerd.
source-git-commit: 653a6be856412faac8783fa9dc7b759a7c6e1f68
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 0%

---


# Klantconfiguratie

De Configuratie van de klant is waar u bepaalt hoe uw merk binnen het optimaliseringsplatform LLM zal worden gecontroleerd en worden geanalyseerd. U kunt categorieën (zoals bedrijfseenheden of productlijnen) aanpassen, concurrenten volgen, en merkpuntsaliassen toevoegen om alle variaties van uw merk in herinneringen te vangen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

![&#x200B; Dashboard van de Configuratie van de Klant &#x200B;](/help/dashboards/assets/customer-config.png)


## Beste praktijken voor het vormen van categorieën, onderwerpen, en herinneringen

Deze sectie beschrijft beste praktijken om te besluiten hoe u opstelling uw categorieën, onderwerpen, herinneringen, en concurrenten wilt.

Dit is een eerste belangrijke stap. Wat u nu beslist bepaalt hoe de informatie aan uw bedrijfscontext wordt aangepast. Eventuele wijzigingen in categorieën in de toekomst stellen historische gegevens opnieuw in.

### Tips en trucs voor rubrieken

Met Categorieën kunt u uw inhoud ordenen in strategische bedrijfseenheden of logische groepen. Zij zijn het &quot;waar het&quot;emmertje en de top-level organisatorische structuur voor uw inhoud behoort.

Wanneer het beslissen hoe te opstellings categorieën, moet u uw doelstellingen overwegen en wie op wat moet handelen u rapporteert.

>[!IMPORTANT]
>
> Zorg ervoor dat de categorieën vanaf het begin correct zijn ingesteld wanneer wijzigingen in categorieën historische gegevens herstellen. Dat betekent dat als je deze wijzigt, je historische gegevens kwijtraakt voor de wijziging.

Hier volgt een overzicht van de typen benaderingen die u kunt volgen en wanneer u een bepaalde aanpak wilt kiezen:

| Benadering | Beschrijving | Voordeel |
|---------|----------|---------|
| Strategic Business Unit (SBU) | Gebruik deze benadering als uw organisatie door P&amp;L (bijvoorbeeld, Consumenten, Onderneming, de Diensten) wordt gesplitst. | U krijgt schone rapportering door bedrijfslijn en gemakkelijkere verantwoordingsplicht. |
| Map op hoofdniveau website (URL_DIR) | Gebruik deze optie als de architectuur met informatie over uw site het eigendom (/products/, /support/, /docs/, /news/) weerspiegelt. | U wordt uitgelijnd op de manier waarop teams inhoud publiceren en onderhouden. |
| Categorie Product (of Service) | Gebruik deze optie als u een catalogus (SKU&#39;s/services) verkoopt. | U krijgt assortiment meningen, hiaatanalyse, en &quot;welke categorie vereist inhoud&quot;antwoorden. |

Hoe te om te besluiten hoe u opstellingscategorieën op één vraag gebaseerd is: **wie moet op het rapport handelen?**

* Als u a *bedrijfsleider* bent, kies de **SBU** benadering.
* Als u a *Web/inhoudseigenaar* bent, kies de **URL_DIR** benadering.
* Als u a *handelend/aanbiedt manager* bent, kies de **product/de categorie van de Dienst** benadering.

>[!IMPORTANT]
>
> * Kies één aanpak en blijf erbij.
> * U kunt **slechts één** model van de Categorie per rekening/merk hebben. Meng niet tegelijkertijd **SBU** en **URL_DIR**.

Voorbeeld:

| Type locatie | Categorie | Voorbeelden van onderwerptaxonomie |
|---------|----------|---------|
| Ondernemingen met meerdere bedrijven | SBU | kleine intent set (How-to, Troubleshooting, Comparison, Pricing, Policy) |
| Documentatie/ondersteuning voor zware locaties | URL_DIR | Hoe te, het Oplossen van problemen, Verwijzing, de nota&#39;s van de Versie |
| eCommerce/Services-catalogus | Product/service | Vergelijking, Revisies, Prijsstelling/Beschikbaarheid, Hoe kan ik, Problemen oplossen |

### Tips en trucs voor onderwerpen

Onderwerpen helpen u de gebruikersinzet te begrijpen - zij tonen u wat de gebruiker wil. Hiermee kunt u herinneringen groeperen met een vergelijkbare gebruikersintentie. Beschouw het als het groeperen van relevante herinneringen samen.

>[!IMPORTANT]
>
>De onderwerpen zijn universeel over **alle** categorieën, betekenend blijven zij verenigbaar ongeacht de categorie die zij aan worden toegewezen. Zij vertegenwoordigen clusters van vragen of herinneringen die een gemeenschappelijke bedoeling delen.

Wanneer u een beslissing neemt over onderwerpen, wilt u een korte, platte lijst maken (maximaal 6-12). Bijvoorbeeld:

* Producten/services
* Hoe kan ik-onderwerpen (instellen/gebruiken)
* Problemen oplossen (fouten/problemen)
* Vergelijking (X versus Y; &quot;best ... for ...&quot;)
* Beoordelingen en beoordelingen
* Prijzen en beschikbaarheid
* Beleid en garantie
* Contact opnemen met ondersteuning
* Zakelijk/nieuws (als u ze echt nodig hebt)

Houd rekening met het volgende wanneer u de lijst maakt:

* Kan een redacteur het onderwerp in 5 seconden van de snelle tekst begrijpen? Zo niet, wijzig de naam/vereenvoudig.
* Zal een verschillend team de moeilijke situatie voor verschillende onderwerpen bezitten? Zo ja, dan hebt u nuttige onderwerpen gekozen.

Enkele handige tips:

* De kennis van uw zaken of plaats van het gebruik om onderwerpen te bepalen die zich aan de strategische doelstellingen van uw merk richten
* Overweeg hoe uw merk met concurrenten binnen specifieke onderwerpen vergelijkt.

>[!IMPORTANT]
>
> * Houd onderwerpen op intent-Gebaseerd, niet organisatorische.
> * Voeg geen categorieën/filters voor merk/non-brand/geografische aangezien u specifiek voor dit in het **Merken** lusje kunt filtreren.
> * De onderwerpen worden uitgespreid uit over verscheidene categorieën, kunt u **niet** verschillende onderwerpen per categorie hebben.
> * Één enkele herinnering kan in verscheidene onderwerpen of categorieën bestaan.

### Tips en trucs voor vragen

De herinneringen identificeren de specifieke vragen of de vragen die de klanten stellen, die uw zaken kunnen beïnvloeden. Het zijn de daadwerkelijke vragen of vragen die de gebruikers in LLMs invoeren.

Ben zeker om herinneringen regelmatig te herzien en bij te werken om ervoor te zorgen zij zich aan klantenbehoeften en bedrijfsdoelstellingen richten.

>[!TIP]
>
>* U kunt gereedschappen zoals LLM Optimizer en Google Search Console met regex-filters gebruiken om algemene vraagstructuren te identificeren (bijvoorbeeld &quot;hoe,&quot; &quot;wat&quot;, &quot;wanneer&quot;, &quot;waar&quot;).
>* Als u wilt weten welke aanwijzingen relevant zijn voor uw site/merk, kunt u onsite zoekgegevens, veelgestelde vragen in de resultatenpagina&#39;s van zoekprogramma&#39;s gebruiken of zelfs LLM-chatbots rechtstreeks vragen welke vragen klanten kunnen stellen over uw merk.

### Aanbevolen werkwijzen voor concurrenten

De concurrenten laten u zicht en de opmerkingen in reacties controleren LLM voor herinneringen en onderwerpen die voor uw zaken belangrijk zijn.

Het [!UICONTROL **Concurrentie die**] lusje volgen laat u concurrenten toevoegen en hun zicht voor specifieke herinneringen en onderwerpen volgen.

Met het volgen van concurrenten kunt u zien hoe vaak concurrenten naast uw merk in verschillende regio&#39;s en categorieën worden genoemd en hun zichtbaarheid met uw eigen merk vergelijken.

>[!TIP]
>
>Herzie regelmatig de opmerkingen en citaten van concurrenten om gebieden te identificeren waar uw merk kan verbeteren.

## Klantconfiguratiedashboard

Het Klantconfiguratiedashboard is een krachtig hulpmiddel dat inzicht biedt in de zichtbaarheid van uw merk in LLM&#39;s. Door correct opstellingscategorieën, onderwerpen, herinneringen, en concurrenten, kunt u ervoor zorgen uw merk goed gepositioneerd is om in LLM-Gegenereerde reacties te verschijnen. Regelmatig evalueren van inzichten zoals Spraak delen, zichtbaarheid van inhoud en mogelijkheden helpt u uw strategie aan te passen en uw concurrenten voor te blijven.

Als u wilt configureren hoe LLM Optimizer uw aanwezigheid van uw merk controleert en analyseert op verschillende markten en in concurrerende landschappen, hebt u toegang tot de volgende tabbladen:

* [Categorieën](#categories)
* [Concurrentietracering](#competitor-tracking)
* [Merkaliassen](#brand-aliases)
* [Gegevens-inzichten](#data-insights)
* [Agentic CDN](#agentic-cdn)

## Categorieën {#categories}

Vanuit het tabblad Categorieën kunt u bedrijfscategorieën of productlijnen definiëren die u wilt bijhouden en deze aan specifieke gebieden koppelen. Over het algemeen heeft het tabblad Categorieën betrekking op elke andere aanpassing op deze pagina, omdat categorieën in het categorieveld worden weergegeven voor de andere aanpassingen (het bijhouden van concurrenten, aliassen enzovoort). Een nieuwe categorie toevoegen:

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

## Agentic CDN {#agentic-cdn}

Niet beschikbaar (zal het beschikbaar voor versie zijn?)

