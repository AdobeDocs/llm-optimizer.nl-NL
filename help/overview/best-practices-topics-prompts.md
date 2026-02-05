---
title: Beste praktijken voor Categorieën, Onderwerpen, Herinneringen, en anderen
description: Optimaliseer LLM inzichten door categorieën, onderwerpen, herinneringen, en andere merken te vormen om met inbegrip van concurrenten voor op maat gemaakte merkcontrole en strategische inhoudanalyse te volgen.
feature: Best Practices, Customer Configuration
source-git-commit: f6d33387337ca097747407099891cbc6b586b9bb
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---


# Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen, en anderen om te volgen

In deze sectie worden de aanbevolen procedures beschreven voor het bepalen van de manier waarop u categorieën, onderwerpen, aanwijzingen en andere opties wilt instellen om bij te houden. Daarnaast bevat het ook informatie over de Industry Prompt Library, die Adobe heeft ontwikkeld met uitgebreid onderzoek met experts uit de industrie.

Dit is een eerste belangrijke stap. Wat u nu beslist bepaalt hoe de informatie aan uw bedrijfscontext wordt aangepast. Eventuele wijzigingen in categorieën in de toekomst stellen historische gegevens opnieuw in.

In het dashboard van [[!UICONTROL Customer Configuration]](/help/dashboards/customer-configuration.md) definieert u hoe uw merk wordt gecontroleerd en geanalyseerd in het LLM-optimaliserplatform. Zie [[!UICONTROL Customer Configuration]](/help/dashboards/customer-configuration.md) voor informatie over het gebruik van het dashboard.

![ het configuratievenster van de Klant ](/help/assets/best-practices/customer-configuration-best-practices.png)

In het dashboard van [!UICONTROL Customer Configuration] kunt u categorieën (zoals bedrijfseenheden of productlijnen) aanpassen, andere merken volgen, en merkaanduidingsaliassen toevoegen om alle variaties van uw merk in verschillende aanwijzingen vast te leggen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

## Industry Promptbibliotheek

Om te helpen met herinneringen en onderwerpen beginnen, heeft Adobe een Bibliotheek van de Vragen van de Industrie gecreeerd die door uitgebreid onderzoek met de industriedeskundigen en analyse van AI onderzoeksgedrag over 6.000+ klanten wordt ontwikkeld. Deze bibliotheek identificeert de meest relevante onderwerpen en herinneringen die op industrie-specifieke tendensen, bevestigde bedrijfsdoelstellingen, en real-world de patronen van het klantenonderzoek worden gebaseerd.

De Industry Prompt Library gebruiken:

1. Navigeer aan het **dashboard van de Configuratie van de Klant**.
1. Selecteer **de Herinneringsbibliotheek van de Download** om het bibliotheekdossier van LLM Optimizer te downloaden.
   ![ de snelle download van de Bibliotheek van de Industrie ](/help/assets/best-practices/customer-configuration-prompts-library.png)
1. Het overzicht stelde **Onderwerpen** voor en **Vragen** voor de industrie van uw merk op het respectieve lusje en kiest de opties die het meest relevant zijn.
1. De kolom van het Stadium van de Reis van de Klant van het overzicht **om snelle opties over de klantenlevenscyclus (bijvoorbeeld, ontdekking aan omzetting aan behoud) te bekijken.** De vroege fase/top van de herinneringen van funnel zijn hoge prioriteit maar ook nadenken later stadium opties om behoud te bevorderen, klantensteun toe te laten, etc.
1. Wijzig de onderwerpen of aanwijzingen die u nodig hebt om uw doelstellingen en doelstellingen zo goed mogelijk te ondersteunen voordat u uw onderwerpen uploadt en vragen naar Adobe LLM Optimizer (voeg bijvoorbeeld uw merk/productnaam toe of voeg terminologie toe voor het merk). Vragen kunnen handmatig of via bulkupload aan LLM Optimizer worden toegevoegd met de meegeleverde sjabloon *.csv* .

>[!TIP]
>
> Gebruik een combinatie van domeinspecifieke herinneringen die door LLM Optimizer tijdens aanvankelijke opstelling en de Bibliotheek van de Vragen van de Industrie worden geadviseerd om uw snelle strategie te leiden.

### Onderzoeksstichting van snelle bibliotheek

De Industry Prompt Library is ontwikkeld via een uitgebreid onderzoeksinitiatief waarin het volgende wordt gecombineerd:

* **intelligentie van de Klant:** Analyse van AI onderzoeksgedrag en voorkeur over 6.000+ klanten
* **deskundigheid van de Industrie:** Perspectieven van deskundigen in Auto, de Financiële Diensten, Gezondheidszorg, Telecom, en de sectoren van de Reizen.
* **Gegevens-gedreven inzichten:** Identificatie van high-impact onderwerpen en vraagpatronen die klantenovereenkomst en omzetting drijven.

De belangrijkste onderwerpen die door klanten over industrieën worden gezocht:

* **Auto:** de auto kwesties van het Oplossen van problemen, die voertuigen en Financiering/Leasing vergelijken
* **Financiële Diensten:** Onderzoek financiële producten
* **Gezondheidszorg:** die symptomen of gezondheidskwesties, de opties van de Behandeling vergelijken, laboratoriumresultaten of medische termijnen begrijpen
* **Telecom:** het vergelijken van plannen, de termijnen en de bevorderingen van het Contract, de Controlerende dienst in lokaal gebied
* **Reizen:** voorbereidend voor een reis, het Onderzoek en het boeken reis

De tendensen van de klant op AI onderzoek en snel gedrag in hulpmiddelen LLM:

* Klanten stellen vragen of gebruiken trefwoorden tijdens het gebruik van de zoekgereedschappen voor LLM.
* Zij gebruiken hoofdzakelijk LLM onderzoeksinstrumenten voor vroege onderzoek en ontdekking.
* Klanten hebben de neiging om een specifiek merk of een productnaam in hun herinneringen te vermelden.

## Tips en trucs voor rubrieken

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

![ Toevoegend categorieën in LLM Optimizer ](/help/assets/best-practices/add-category.png)

>[!IMPORTANT]
>
> * Kies één aanpak en blijf erbij.
> * U kunt **slechts één** model van de Categorie per rekening/merk hebben. Meng niet tegelijkertijd **SBU** en **URL_DIR**.
<!--Can you mix Product/Service with these?-->

Voorbeeld:

| Type locatie | Categorie | Voorbeelden van onderwerptaxonomie |
|---------|----------|---------|
| Ondernemingen met meerdere bedrijven | SBU | Kleine intent set (Hoe kan ik, Problemen oplossen, Vergelijking, Prijsstelling, Beleid) |
| Documentatie/ondersteuning voor zware locaties | URL_DIR | Hoe te, het Oplossen van problemen, Verwijzing, de nota&#39;s van de Versie |
| eCommerce/Services-catalogus | Product/service | Vergelijking, Revisies, Prijsstelling/Beschikbaarheid, Hoe kan ik, Problemen oplossen |

## Tips en trucs voor onderwerpen

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
* Bedrijfs/Nieuws (als u dit echt nodig hebt)

![ Toevoegend onderwerpen in LLM Optimizer ](/help/assets/best-practices/add-topic.png)

Houd rekening met het volgende wanneer u de lijst maakt:

* Kan een redacteur het onderwerp in 5 seconden van de snelle tekst begrijpen? Zo niet, wijzig de naam/vereenvoudig.
* Zal een verschillend team de moeilijke situatie voor verschillende onderwerpen bezitten? Zo ja, dan hebt u nuttige onderwerpen gekozen.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Enkele handige tips:

* De kennis van uw zaken of plaats van het gebruik om onderwerpen te bepalen die zich aan de strategische doelstellingen van uw merk richten
* Overweeg hoe uw merk met andere merken binnen specifieke onderwerpen vergelijkt.

>[!IMPORTANT]
>
> * Houd onderwerpen op intent-Gebaseerd, niet organisatorische.
> * Voeg geen categorieën/filters toe voor merk/niet-merk/geografische locatie, aangezien u hiervoor specifiek kunt filteren op het tabblad **[!UICONTROL Brands]** .
> * Onderwerpen worden verspreid over verschillende categorieën. U **kunt niet** unieke onderwerpen aan elke categorie bepalen.
> * Één enkele herinnering **kan** in verscheidene onderwerpen of categorieën bestaan.

## Tips en trucs voor vragen

De herinneringen identificeren de specifieke vragen of de vragen die de klanten stellen, die uw zaken kunnen beïnvloeden. Het zijn de daadwerkelijke vragen of vragen die de gebruikers in LLMs invoeren.

Ben zeker om herinneringen regelmatig te herzien en bij te werken om ervoor te zorgen zij zich aan klantenbehoeften en bedrijfsdoelstellingen richten.

Tips en trucs voor aanwijzingen:

* Groepeer gelijkaardige herinneringen samen gebaseerd op wat de mensen vragen.
* Focus op de vragen die het belangrijkst zijn voor uw klanten.
* Controleer of uw merk een goede kans heeft om voor bepaalde herinneringen te worden vermeld.

>[!TIP]
>
>* Met gereedschappen als Adobe LLM Optimizer en Google Search Console met regex-filters kunt u veelvoorkomende vraagstructuren identificeren (bijvoorbeeld &quot;hoe&quot;, &quot;wat&quot;, &quot;wanneer&quot; en &quot;waar&quot;) en nagaan welke aanwijzingen mensen gebruiken om uw site te bezoeken.
>* Als u wilt weten welke aanwijzingen relevant zijn voor uw site/merk, kunt u onsite zoekgegevens, veelgestelde vragen in de resultatenpagina&#39;s van zoekprogramma&#39;s gebruiken of zelfs LLM-chatbots rechtstreeks vragen welke vragen klanten kunnen stellen over uw merk.

## Aanbevolen procedures voor het bijhouden van andere merken

Het volgen van Anderen laat u zicht en bedenkingen in reacties LLM voor herinneringen en onderwerpen controleren die voor uw zaken belangrijk zijn.

[!UICONTROL **anderen die**] tabel volgen laat u anderen met inbegrip van concurrenten toevoegen om hun zicht voor specifieke herinneringen en onderwerpen te volgen.

Met anderen die volgen, kunt u zien hoe vaak andere merken naast uw merk in verschillende regio&#39;s en categorieën worden vermeld en hun zicht aan uw vergelijken.

>[!TIP]
>
>Regelmatig beoordelen van concurrenten of andere aanhalingstekens en citaten om gebieden te identificeren waar uw merk kan verbeteren.

## Meer informatie

* [ dashboard van de Configuratie van de Klant ](/help/dashboards/customer-configuration.md) is waar u uw categorieën, onderwerpen, herinneringen, en anderen het volgen vormt.
* [ de beste praktijken van LLM Optimizer ](/help/tutorials/best-practices.md) beschrijft beste praktijken rond Optimalisering LLM

