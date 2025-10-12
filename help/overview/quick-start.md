---
title: Snel starten
description: 'Ga aan de slag met Adobe LLM Optimizer: ontgrendel uw merk, ontgrendel de zichtbaarheid van AI en verken dashboards om de zoekprestaties te verbeteren.'
source-git-commit: c64995176f6cb50bf23543fe95471c4723ae9a10
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 0%

---


# Snel starten

Als u aan de slag wilt met de LLM-optimalisator, moet u het instapproces voltooien, zoals beschreven in de onderstaande stappen. Nadat u het proces voltooit zult u volledige toegang tot [ LLM Optimizer dashboards ](/help/dashboards/dashboards-overview.md) en andere functionaliteiten hebben.

## Overzicht van onboarding

Het instapproces begint met het instappen van uw domein. Het proces is anders, afhankelijk van of u een AEM Cloud-klant bent of niet. Nadat u het proces voltooit, zult u informatie voor het Logboek moeten verstrekken CDN door:sturen en tenslotte categorieën, onderwerpen, en herinneringen aanpassen. Elk onderdeel van het proces wordt hieronder beschreven samen met handige tips over hoe u zo snel mogelijk met LLM Optimizer aan de slag kunt gaan.

## Stap 1: Aan boord van uw domein

### Probeer het voor je aankoop

Klanten met AEM Cloud (Cloud Service, Managed Services, Edge Delivery Service) kunnen de optie Proefversie gebruiken voordat je de aanbieding koopt. Het is een gratis proefversie van LLM Optimizer met maximaal 200 gratis berichten. Voor het gebruik van meer dan 200 aanwijzingen is een aparte licentieovereenkomst vereist. Toegang wordt verleend op basis van &quot;actuele&quot; en &quot;beschikbare&quot; basis, en kan te allen tijde door Adobe worden gewijzigd, beperkt of verwijderd.

Sommige productmogelijkheden zijn niet beschikbaar in de gratis versie:

* Proefversie is beperkt tot één domein. U kunt het domein dat u hebt opgegeven niet wijzigen nadat u de installatie hebt voltooid.
* Ondersteuning voor het implementeren van optimalisaties is niet beschikbaar.

Zie de onderstaande sectie voor meer informatie over het activeren van de gratis proefversie en het aan boord gaan van uw domein.

### Klanten met AEM Cloud

Als u een Klanten van de Wolk van AEM bent hebt u de optie om LLM Optimizer te proberen door de kaart van de Aankondiging van het Product in [ Experience Hub ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) te gebruiken.

>[!NOTE]
>Nieuw toegevoegde herinneringen zullen niet in het [ dashboard van de Aanwezigheid van het Merk ](/help/dashboards/brand-presence.md) verschijnen tot de verwerking volledig is. Klanten van AEM Cloud (Cloud Service, Managed Services/Edge Delivery Service) kunnen de gratis proefversie van LLM Optimizer gebruiken. Voor het gebruik van meer dan 200 aanwijzingen is een aparte licentieovereenkomst vereist. Toegang wordt verleend op basis van &quot;actuele&quot; en &quot;beschikbare&quot; basis, en kan te allen tijde door Adobe worden gewijzigd, beperkt of verwijderd. Neem contact op met uw accountvertegenwoordiger voor meer informatie.

![ Proefversie van LLM Optimizer ](/help/overview/assets/llm-trial.png)

Zodra u de **knoop van de Probeer LLM Optimizer** klikt, zult u aan [ https://llmo.now ](https://llmo.now) opnieuw worden gericht. U moet zich vervolgens aanmelden via IMS. Wanneer u zich hebt aangemeld, start u het instapproces door een domein en de merknaam op te geven.

![ LLM Optimizer domein ](/help/overview/assets/domain.png)

>[!NOTE]
>Het domein u verstrekte zal door iedereen van uw organisatie worden gebruikt en kan niet worden veranderd.

Om de Analyse van de Aanwezigheid van het Merk teweeg te brengen, zult u categorieën, onderwerpen, en herinneringen moeten verstrekken.

![ de Analyse van de Aanwezigheid van het Merk ](/help/overview/assets/bp-analysis.png)

Bovendien, moet u ook [ het logboek vormen CDN door:sturen ](#step-4) voor verkeersanalyse. LLM Optimizer vereist dat er merkgegevens en inzichten van het agentische en verwijzingsverkeer worden verzameld om mogelijkheden te identificeren en aanbevelingen te doen om de zichtbaarheid van AI te vergroten.

### Klanten die geen AEM Cloud zijn

Zodra de bedrijfsovereenkomst is voltooid, wordt u aan boord genomen via de slackbot-opdracht met het domein dat u op LLM Optimizer wilt laten instappen. Zodra dit onboarding volledig is, zult u aan login aan LLM Optimizer via [ https://llmo.now ](https://llmo.now) kunnen.

### Stap 2: Pas Categorieën, Onderwerpen, en Vragen aan

Als u de Brand Presence-analyse wilt activeren en het dashboard wilt vullen met inzichten in de zichtbaarheid van uw merk, moet u Categorieën, Onderwerpen en Vragen aanpassen. Deze configuratie wordt gecreeerd op het [ dashboard van de klantenconfiguratie ](/help/dashboards/customer-configuration.md).

![ Dashboard van de Configuratie van de Klant ](/help/overview/assets/prompt-creation.png)

Vanuit dit dashboard kunt u:

* Voeg **nieuwe categorieën** toe die zich op uw bedrijfsprioriteiten richten. Categorieën kunnen brede inhoudsgebieden zijn die relevant zijn voor uw domein.
* Ga **douaneonderwerpen** of subtopics in u gevolgd wilt. Onderwerpen kunnen specifieke thema&#39;s zijn die zijn gekoppeld aan trefwoorden met een hoog volume zonder branding die aan uw domein zijn gekoppeld.
* Creeer **uw herinneringen** om zicht in specifieke vragen te controleren. Vragen zijn query&#39;s (gebrandmerkt en niet-branded) die een basislijnzichtbaarheid bieden. Slechts zal een beperkt aantal herinneringen automatisch worden geproduceerd gebaseerd op de categorieën en de onderwerpen die u verstrekte.
* Bepaal verwijzings **aliassen** om ervoor te zorgen alle verwijzingen van een merk worden gevangen en rekenschap gegeven.
* Bepaal **concurrent aliassen** om concurrenten nauwkeurig te volgen.

>[!NOTE]
>De nauwkeurige herinneringen u LLMs vraagt zijn niet openbaar beschikbaar omdat zij niet door LLMs worden bekendgemaakt.

### Stap 3: Automatische voorpopulatie van inzichten

Zodra uw domein wordt geregistreerd en u categorieën, en onderwerpen hebt verstrekt, zal LLM Optimizer automatisch de analyse van de Aanwezigheid van het Merk teweegbrengen.

### Stap 4: Geef informatie op voor CDN-logbestanden die worden doorgestuurd {#step-4}

Om de Inzichten van het Verkeer van het Verkeer van het Bureau en van het Verkeer van verwijzingen te ontgrendelen, moet u informatie voor het logboek verstrekken CDN door:sturen. Het kan van het dashboard van de klantenconfiguratie worden toegevoegd door naar het lusje van de Configuratie te gaan CDN en **Onboard CDN** te klikken.

![ Klantenconfiguratie CDN ](/help/overview/assets/cc-cdn.png)

Alternatief, als geen leverancier CDN vooraf is geselecteerd, zult u worden ertoe aangezet om het logboek toe te voegen CDN door:sturen wanneer het toegang tot van het de verkeersdashboards van het Agentschap en van de Verwijzing voor het eerst. Zie voor meer informatie:

* [Agentic Traffic](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Verwijzingsverkeer](/help/dashboards/referral-traffic.md#setup#setup)

### Stap 5: Ontdek dashboards en onderneem actie

Nadat u informatie voor het Door:sturen van het Logboek CDN verstrekt, kunt u:

* Bekijk het [ dashboard van de Aanwezigheid van het Merk ](/help/dashboards/brand-presence.md), bekijk uw zichtbaarheidsscore en spoor uw prestaties met betrekking tot uw concurrenten.
* Onderzoek de [ Agentische ](/help/dashboards/agentic-traffic.md) en [ ](/help/dashboards/referral-traffic.md) dashboards van het Verkeer van de Verwijzing, als het logboek CDN door:sturen is gevormd.
* Gebruik [ Kansen ](/help/dashboards/opportunities.md) om inhoud en technische verbeteringen te identificeren.
* Exporteer gegevens en werk samen met uw team of nodig uw collega uit om het product te gebruiken.

Tot slot om de mogelijkheden van optimizer volledig te begrijpen LLM, onderzoek alle beschikbare [ dashboards ](/help/dashboards/dashboards-overview.md).
