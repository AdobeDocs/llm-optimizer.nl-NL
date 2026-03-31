---
title: Snel starten
description: Leer hoe u uw merknaam en domein kunt opnemen, uw proefversie kunt activeren vanuit Experience Hub of Experience Cloud en de installatie voor Adobe LLM Optimizer kunt voltooien.
feature: Quickstart, Onboarding
source-git-commit: dcbeb1c61dd9dcefd83908f65f8303d36c0fb78e
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# Snel starten

Als u aan de slag wilt met LLM Optimizer, moet u het instapproces voltooien. Na aan boord gaan, zult u categorieën, onderwerpen, herinneringen kunnen aanpassen en logboek vormen door:sturen voor nauwkeurigere inzichten en volledige toegang tot [&#x200B; LLM Optimizer dashboards &#x200B;](/help/dashboards/dashboards-overview.md) en andere functionaliteit.

## Overzicht van onboarding

Het instapproces begint met het instappen van uw domein en uw merknaam. Elk deel van de instapreis wordt hieronder beschreven en bevat nuttige tips over hoe u zo snel mogelijk met LLM Optimizer aan de slag kunt gaan.

### Adobe LLM Optimizer toegang geven tot openbare pagina&#39;s

Adobe LLM Optimizer heeft toegang nodig tot uw openbare pagina&#39;s om nauwkeurige inhoud en technische aanbevelingen te kunnen leveren. Dit wordt bereikt door een veilige interne kruipper (Spacecat/1.0 gebruikersagent).

Configuratievereisten:

* Voeg de gebruikersagent Spacecat/1.0 aan de Lijst van gewenste personen in het robots.txt- dossier of allebei-verkeersbeheerregels van uw plaats toe.
* Zorg ervoor dat pagina&#39;s niet op domein of CDN-niveau worden geblokkeerd. Geblokkeerde pagina&#39;s kunnen niet worden geïndexeerd, wat betekent dat er geen optimalisatietaken en inzichten voor deze pagina&#39;s kunnen worden gegenereerd.

Als de zichtbaarheid van de inhoud op het dashboard laag wordt weergegeven, controleert u of de schuifregelaar toegang heeft tot uw domeinen. Beperkte toegang is een gemeenschappelijke oorzaak van onvolledige indexering.

## Stap 1: Aan boord van uw merknaam en domein {#step-1-onboard-your-domain}

Als u aan de slag wilt met LLM Optimizer, activeert u eerst uw proefversie (indien van toepassing) en neemt u uw merknaam en domein aan.

### Uw proefversie activeren

De activeringsstroom is afhankelijk van uw Adobe-product.

#### AEM Cloud-klanten

Als AEM Cloud-klant kunt u uw proefversie activeren door:

* Navigeer aan [&#x200B; Experience Hub &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/experience-hub/experience-hub) en gebruik de kaart van de Aankondiging van het Product om LLM Optimizer te activeren. Nadat u **probeert LLM Optimizer** selecteert, wordt u opnieuw gericht aan [&#x200B; https://llmo.now &#x200B;](https://llmo.now). Meld u aan via IMS en voer vervolgens een domein- en merknaam in om het instapproces te starten.
* Of ga direct naar [&#x200B; https://llmo.now &#x200B;](https://llmo.now) en teken binnen.

![&#x200B; Proefversie van LLM Optimizer &#x200B;](/help/overview/assets/llm-trial.png)

#### Adobe Analytics-klanten

Als u een Adobe Analytics-klant bent, ziet u een banner op de startpagina van Experience Cloud.

![&#x200B; Experience Cloud homepage met Begin uw banner van het Proefabonnement van Adobe LLM Optimizer &#x200B;](/help/overview/assets/experience-cloud-llmo-trial-banner.png)

U kunt uw proefversie op een van de volgende manieren activeren:

* Selecteer **Begin uw Proef van Adobe LLM Optimizer** in de banner.
* Ga direct naar [&#x200B; https://llmo.now &#x200B;](https://llmo.now) en teken binnen.

Wanneer de proefversie actief is, gaat u verder met het instappen van uw merknaam en domein.

>[!NOTE]
>
> * **Gratis proef:** de klanten van de Wolk van AEM en van Adobe Analytics kunnen de vrije proefversie van LLM Optimizer gebruiken.
> * **Klanten die de proef op of na 1 April, 2026** activeren kunnen tot 100 herinneringen, één domein gebruiken, en optimalisaties over maximaal 10 URLs voor één enkel opportuniteitstype opstellen.
> * **Klanten die de proef vóór 1 April, 2026** activeerden blijven toegang tot maximaal 200 herinneringen onder hun bestaande termijnen hebben.
>
>Voor gebruik buiten de opgenomen limieten is een aparte licentieovereenkomst vereist. Toegang wordt verleend op basis van &quot;actuele&quot; en &quot;beschikbare&quot; basis, en kan te allen tijde worden gewijzigd, beperkt of verwijderd. Neem contact op met uw accountvertegenwoordiger voor meer informatie.

#### Aan boord van uw merknaam en domein

Aan boord van uw merknaam en domein om LLM Optimizer te gaan gebruiken.

1. Voer uw merknaam en het bijbehorende domein in.

   * Dit zou het belangrijkste domein moeten zijn waar u inhoud wilt analyseren en optimaliseren.

1. Volledig aan boord gaan.

   * Na verzending begint LLM Optimizer uw domein te analyseren en inzichten te genereren.

![&#x200B; LLM Optimizer domein &#x200B;](/help/overview/assets/domain.png)

>[!NOTE]
>Nieuw toegevoegde herinneringen zullen niet in het [&#x200B; dashboard van de Aanwezigheid van het Merk &#x200B;](/help/dashboards/brand-presence.md) verschijnen tot de verwerking volledig is.

>[!NOTE]
>Het domein u verstrekte zal door iedereen van uw organisatie worden gebruikt en kan niet worden veranderd.

Tijdens de instapkaartfase wordt een kleine set categorieën, onderwerpen en aanwijzingen gegenereerd. De analyse van de Aanwezigheid van het merk op die herinneringen zal beschikbaar zijn kort nadat uw plaats is ingezien.

De mogelijkheid om optimalisaties aan de rand te implementeren is ook beschikbaar. Leer meer in [&#x200B; optimaliseren bij Edge — Veelgestelde vragen &#x200B;](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/resources/optimize-at-edge/overview#frequently-asked-questions).

Bovendien, vorm [&#x200B; het logboek CDN door:sturen &#x200B;](#step-4) voor verkeersanalyse. LLM Optimizer vereist Brand Presence-gegevens en inzichten van het agentische en verwijzingsverkeer om mogelijkheden te identificeren en aanbevelingen te doen die AI-zichtbaarheid bevorderen.

### Klanten die geen AEM Cloud gebruiken

Nadat uw organisatie de bedrijfsovereenkomst heeft voltooid, wordt u aan LLM Optimizer ingeschreven met het domein dat uw organisatie heeft geselecteerd. Wanneer het aan boord gaan eindigt, teken binnen bij [&#x200B; https://llmo.now &#x200B;](https://llmo.now).

## Stap 2: Pas Categorieën, Onderwerpen, en Vragen aan

Zodra uw site is gestart, kunt u de Brand Presence Analysis bekijken op basis van de kleine set aanwijzingen die automatisch zijn gegenereerd tijdens de instapfase. Als u verder gaat, kunt u de categorieën, onderwerpen en aanwijzingen voor uw merk aanpassen. Deze configuratie wordt gecreeerd op het [&#x200B; dashboard van de klantenconfiguratie &#x200B;](/help/dashboards/customer-configuration.md).

![&#x200B; Dashboard van de Configuratie van de Klant &#x200B;](/help/overview/assets/prompt-creation.png)

Vanuit dit dashboard kunt u:

* Voeg **nieuwe categorieën** toe die zich op uw bedrijfsprioriteiten richten. Categorieën kunnen brede inhoudsgebieden zijn die relevant zijn voor uw domein.
* Ga **douaneonderwerpen** of subtopics in u gevolgd wilt. Onderwerpen kunnen specifieke thema&#39;s zijn die zijn gekoppeld aan trefwoorden met een hoog volume zonder branding die aan uw domein zijn gekoppeld.
* Creeer **uw herinneringen** om zicht in specifieke vragen te controleren. Vragen zijn query&#39;s (gebrandmerkt en niet-branded) die een basislijnzichtbaarheid bieden. Slechts zal een beperkt aantal herinneringen automatisch worden geproduceerd gebaseerd op de categorieën en de onderwerpen die u verstrekte.
* Bepaal verwijzings **aliassen** om ervoor te zorgen alle verwijzingen van een merk worden gevangen en rekenschap gegeven.
* Bepaal **andere aliassen** om andere merken nauwkeurig te volgen.

>[!NOTE]
>De nauwkeurige herinneringen u LLMs vraagt zijn niet openbaar beschikbaar omdat zij niet door LLMs worden bekendgemaakt.

>[!NOTE]
>
> Voor meer details op hoe te opstelling zien uw categorieën, onderwerpen, herinneringen de [&#x200B; Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen &#x200B;](/help/overview/best-practices-topics-prompts.md) pagina.

## Stap 3: Merk Presence Insights

Nadat uw domein is ingezien, zult u aanvankelijke inzichten in de mening van de Aanwezigheid van het Merk zien die op de herinneringen wordt gebaseerd die automatisch tijdens onboarding werden geproduceerd. Zodra u uw eigen categorieën, onderwerpen, en herinneringen aanpast, zal LLM Optimizer automatisch de analyse van de Aanwezigheid van het Merk op de herinneringen teweegbrengen u verstrekte en de resultaten zullen over 24 uren beschikbaar zijn.

## Stap 4: Geef informatie op voor CDN-logbestanden die worden doorgestuurd {#step-4}

Om de Inzichten van het Verkeer van het Verkeer van het Bureau en van het Verkeer van de Verwijzing te ontgrendelen, voeg CDN logboek toe door:sturen informatie van het [&#x200B; dashboard van de klantenconfiguratie &#x200B;](/help/dashboards/customer-configuration.md#cdn-configuration). Open het **lusje van de Configuratie 0&rbrace; CDN en selecteer** On board CDN **.**

![&#x200B; Klantenconfiguratie CDN &#x200B;](/help/overview/assets/cc-cdn.png)

Alternatief, als geen leverancier CDN vooraf (zoals hierboven beschreven) is toegevoegd, zult u worden ertoe aangezet om het logboek toe te voegen CDN door:sturen wanneer het toegang tot van het Verkeer van de Agent en van de Verwijzing dashboards voor het eerst. Zie voor meer informatie:

* [Agentic Traffic](/help/dashboards/agentic-traffic.md#cdn-setup)
* [Verwijzingsverkeer](/help/dashboards/referral-traffic.md#setup)

>[!NOTE]
>Voor details betreffende logboek door:sturen wanneer het gebruiken van een klant beheerde CDN (BYOCDN) zie [&#x200B; BYOCDN Logboek dat Overzicht door:sturen &#x200B;](/help/overview/log-forwarding/log-forwarding-overview.md)

## Stap 5: Ontdek dashboards en onderneem actie

Nadat u informatie voor het Door:sturen van het Logboek CDN verstrekt, kunt u:

* Bekijk het [&#x200B; dashboard van de Aanwezigheid van het Merk &#x200B;](/help/dashboards/brand-presence.md) en bekijk uw zichtbaarheidsscore en spoor uw prestaties met betrekking tot andere merken.
* Onderzoek de [&#x200B; Agentische &#x200B;](/help/dashboards/agentic-traffic.md) en [&#x200B; &#x200B;](/help/dashboards/referral-traffic.md) dashboards van het Verkeer van de Verwijzing, als het logboek CDN door:sturen is gevormd.
* Gebruik [&#x200B; Kansen &#x200B;](/help/dashboards/opportunities.md) om inhoud en technische verbeteringen te identificeren.
* Exporteer gegevens en werk samen met uw team of nodig uw collega uit om het product te gebruiken.

Tot slot om de mogelijkheden van LLM Optimizer volledig te begrijpen, zou u alle beschikbare [&#x200B; dashboards &#x200B;](/help/dashboards/dashboards-overview.md) moeten onderzoeken.
