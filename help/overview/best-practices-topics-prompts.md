---
title: Beste praktijken voor Categorieën, Onderwerpen, en Vragen
description: Optimaliseer LLM-inzichten door categorieën, onderwerpen, vragen en concurrenten te configureren voor op maat gemaakte merkbewaking en strategische inhoudanalyse.
source-git-commit: c7c66566137ad1f5bda89f55748b9d81ddf36f76
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---


# Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen, en concurrenten

Deze sectie beschrijft beste praktijken om te besluiten hoe u opstelling uw categorieën, onderwerpen, herinneringen, en concurrenten wilt.

Dit is een eerste belangrijke stap. Wat u nu beslist bepaalt hoe de informatie aan uw bedrijfscontext wordt aangepast. Eventuele wijzigingen in categorieën in de toekomst stellen historische gegevens opnieuw in.

In het dashboard van [[!UICONTROL Customer Configuration]](/help/dashboards/customer-configuration.md) definieert u hoe uw merk wordt gecontroleerd en geanalyseerd in het LLM-optimaliserplatform. Zie [[!UICONTROL Customer Configuration]](/help/dashboards/customer-configuration.md) voor informatie over het gebruik van het dashboard.

![ het configuratievenster van de Klant ](/help/assets/best-practices/customer-configuration-best-practices.png)

In het dashboard van [!UICONTROL Customer Configuration] kunt u categorieën (zoals bedrijfseenheden of productlijnen) aanpassen, concurrenten volgen, en merkaanduidingsaliassen toevoegen om alle variaties van uw merk in verschillende aanwijzingen vast te leggen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

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

>[!IMPORTANT]
>
> * Kies één aanpak en blijf erbij.
> * U kunt **slechts één** model van de Categorie per rekening/merk hebben. Meng niet tegelijkertijd **SBU** en **URL_DIR**.
>   <!--Can you mix Product/Service with these?-->

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

Houd rekening met het volgende wanneer u de lijst maakt:

* Kan een redacteur het onderwerp in 5 seconden van de snelle tekst begrijpen? Zo niet, wijzig de naam/vereenvoudig.
* Zal een verschillend team de moeilijke situatie voor verschillende onderwerpen bezitten? Zo ja, dan hebt u nuttige onderwerpen gekozen.
  <!-- Last bullet point does not make sense. Clarification needed. Also not sure what is meant by "editor"?-->

Enkele handige tips:

* De kennis van uw zaken of plaats van het gebruik om onderwerpen te bepalen die zich aan de strategische doelstellingen van uw merk richten
* Overweeg hoe uw merk met concurrenten binnen specifieke onderwerpen vergelijkt.

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

## Aanbevolen werkwijzen voor concurrenten

De concurrenten laten u zicht en de opmerkingen in reacties controleren LLM voor herinneringen en onderwerpen die voor uw zaken belangrijk zijn.

Het [!UICONTROL **Concurrentie die**] lusje volgen laat u concurrenten toevoegen en hun zicht voor specifieke herinneringen en onderwerpen volgen.

Met het volgen van concurrenten kunt u zien hoe vaak concurrenten naast uw merk in verschillende regio&#39;s en categorieën worden genoemd en hun zichtbaarheid met uw eigen merk vergelijken.

>[!TIP]
>
>Herzie regelmatig de opmerkingen en citaten van concurrenten om gebieden te identificeren waar uw merk kan verbeteren.

## Meer informatie

* [ dashboard van de Configuratie van de Klant ](/help/dashboards/customer-configuration.md) is waar u uw categorieën, onderwerpen, herinneringen, en concurrenten vormt.
* [ de beste praktijken van LLM Optimizer ](/help/tutorials/best-practices.md) beschrijft beste praktijken rond Optimalisering LLM

