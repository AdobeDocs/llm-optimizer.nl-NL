---
title: Adobe Analytics-integratie
description: Leer hoe u Adobe Analytics met LLM Optimizer kunt verbinden om door AI gestuurde detectie, betrokkenheid van sites en bedrijfsresultaten te meten in het Referral Traffic dashboard.
feature: Referral Traffic
source-git-commit: e7c9bc1d40267dc92608baa005f85f4be21cfda1
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# Adobe Analytics-integratie

De Adobe Analytics-integratie maakt verbinding met LLM Optimizer met de Adobe Analytics-gegevens van uw organisatie, zodat u kunt meten hoe de door AI aangestuurde detectie zich vertaalt in echte betrokkenheid van websites en zakelijke resultaten. Nadat het integratieproces volledig is, zullen de gegevens in het **dashboard 1} van het Verkeer van 0} Referral onder het** BedrijfsEffect **tabel beschikbaar zijn.**

Door analysegegevens te koppelen aan AI-zichtbaarheidsinzichten, helpt LLM Optimizer u bij het bijhouden van:

* De betrokkenheid van de gebruiker bij AI-pagina&#39;s.
* Conversiesignalen die gekoppeld zijn aan AI-ontdekkingsreizen.
* Prestatieeffect van GEO-optimalisaties.

Deze integratie overbrugt de kloof tussen de zichtbaarheid van AI en de analyse van de bedrijfsprestaties. Teams kunnen nu niet alleen zien waar het merk voorkomt in AI-reacties, maar wat er gebeurt nadat de gebruikers zijn aangekomen.

## Beschikbaarheid {#availability}

>[!IMPORTANT]
>
>De integratie met Adobe Analytics is inbegrepen in het aanbod van de betaalde LLM Optimizer. Klanten die de gratis proefversie gebruiken, kunnen pas verbinding maken met Adobe Analytics nadat ze een upgrade naar een betaald voorstel hebben uitgevoerd.

## Adobe Analytics verbinden met het verwijzingsverkeer dashboard {#connect}

De verbindingsstroom begint van het [ dashboard van het Verkeer van de Verwijzing ](/help/dashboards/referral-traffic.md) als volgt:

1. Open het ](/help/dashboards/referral-traffic.md) dashboard van het Verkeer 0} Referral. [De standaardmening is **Inzichten van het Verkeer**.

   ![ het dashboard van het Verkeer van verwijzingen, het lusje van de Inzichten van het Verkeer ](/help/dashboards/assets/aa-integration-01-referral-traffic-traffic-insights.png)

1. Selecteer het **BedrijfsEffect** lusje. Als geen analyseleverancier wordt aangesloten, verschijnt een banner: **verbindt om BedrijfsEffect** te zien, met **verbindt met Analytics**.

   ![ BedrijfsEffect lusje met verbindt met Analytics ](/help/dashboards/assets/aa-integration-02-business-impact-connect.png)

1. Selecteer **verbind met Analytics**. Dit opent het ](/help/dashboards/customer-configuration.md) dashboard van de Configuratie van de Klant 0} {op **Analytics** tabel.[

   ![ Configuratie van de Klant, het lusje van Analytics ](/help/dashboards/assets/aa-integration-03-analytics-tab.png)

1. Onder **Geloofsbrieven**, ga **identiteitskaart van de Cliënt** en **Geheime Cliënt** in, dan uitgezocht **verifieer &amp; ga** verder. Houd rekening met het volgende:

   * **verifieer &amp; ga** is beschikbaar slechts wanneer beide gebieden worden gevuld.
   * Na een geslaagde verificatie worden de rapportsuites geladen.
   * Gebruik **identiteitskaart van de Cliënt** en **Geheime Cliënt** van a [ technische rekening ](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/) die toegang tot de rapportreeks heeft u wenst.

   ![ de geloofsbrieven van Analytics en verifiëren &amp; verdergaan ](/help/dashboards/assets/aa-integration-04-credentials.png)

1. Onder **Configuratie**, kies de Reeks van het a **Rapport**.

   Wanneer een rapportreeks wordt geselecteerd, laadt LLM Optimizer de **pagina URL Dimension** opties beschikbaar voor die reeks.

   ![ geselecteerde de reeks van het Rapport en dimensies ladend ](/help/dashboards/assets/aa-integration-05-report-suite.png)

1. Kies Dimension van de a **Pagina URL** (reeks-specifieke afmetingenlijst), dan uitgezocht **sparen &amp; laat** toe.

   * **Pagina URL Dimension** blijft gehandicapt tot een rapportreeks wordt geselecteerd en de afmetingen hebben geladen.
   * **sparen &amp; laat toe** is beschikbaar slechts nadat u een paginaURL afmeting selecteert.

   ![ de dimensie van URL van de Pagina en sparen &amp; laat ](/help/dashboards/assets/aa-integration-06-page-url-dimension.png) toe

1. Na het bewaren, zou de configuratie de **Verbonden** status moeten tonen. U kunt op het dashboard van het Verkeer van de Verwijzing met **terugkeren naar het Dashboard van het Verkeer van de Verwijzing**. In **Verkeer van de Verwijzing** op het **BedrijfsEffect** lusje, zou de status als **moeten verschijnen verbonden met Adobe Analytics**.

   ![ verbonden met Adobe Analytics in configuratie en BedrijfsEffect ](/help/dashboards/assets/aa-integration-07-connected.png)

### Nadat u verbinding hebt gemaakt {#after-connect}

* LLM Optimizer backfills de **laatste vier volledige kalenderweken** en de **huidige kalenderweek aan datum**.
* Na backfill, wordt het gegeven verfrist **dagelijks** met een trekkracht van de **volledige voorafgaande dag**.

>[!NOTE]
>
>De backfill kan een paar uur duren.

## Hoe werkt het {#how-it-works}

### Configuratie

Tijdens de installatie definieert u welke rapportsuite en pagina-dimensie LLM Optimizer gebruikt voor de Adobe Analytics-opname. De afmetingen van de pagina kunnen, afhankelijk van uw rapportsuite, de standaardtoewijzing `variables/page` of een aangepaste `eVar` zijn.

### Hoe het verkeer LLM wordt geïdentificeerd

Het op LLM-Gebaseerde verkeer wordt geïdentificeerd door het type van Referteur van Adobe Analytics [ te gebruiken - de Conversationele hulpmiddelen van AI ](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/referrer-type#conversational-ai-tools).

### Gegevens ingevoerd {#data-ingested}

De volgende gegevens worden door LLM Optimizer ingevoerd:

**Afmetingen**

* Refererdomein
* Type referentie
* Land
* Apparaattype
* Geselecteerde paginadimensie

**Metriek**

* Paginaweergaven
* Bezoeken
* Bezoekers
* Berichten
* Afsluiten
* Bounces
* Bezoeken van één pagina
* Tijd besteed
* Houtskaarten
* Extra winkelwagentjes
* Winkelwagentjes
* Winkelweergaven
* Afbeeldingen
* Orders
* Ontvangsten
* Eenheden

### Hoe LLM Optimizer deze gegevens gebruikt

Deze dataset geeft LLM Optimizer inzicht in:

* LM-verkeersprestaties op paginaniveau.
* Refereringsprestaties in LLM-bronnen.
* Regionale trends en ontwikkelingen op apparaatniveau.
* De handelsresultaten stroomafwaarts.

## Veelgestelde vragen {#faq}

V: Is de integratie van Adobe Analytics beschikbaar tijdens het proces?

Nee. De integratie is alleen beschikbaar voor klanten van LLM Optimizer die abonnementsgeld betalen.

V: Welke gegevens worden verzameld of opgeslagen?

Zie [ Gegevens ingebed ](#data-ingested) hierboven hoofdstuk. LLM Optimizer werkt met geaggregeerde meetgegevens van de Adobe Analytics API&#39;s die door uw organisatie zijn geautoriseerd, en niet met de onbewerkte gegevens op raakniveau.

V: Hoe worden gegevens opgenomen?

Uw organisatie geeft LLM Optimizer toestemming om Adobe Analytics API&#39;s op te vragen. Het verwijzingsverkeer dat aan bronnen LLM wordt gericht wordt verbruikt door die APIs.

V: Hoe vaak worden gegevens vernieuwd?

De gegevens worden verfrist **dagelijks** (volledige vroegere dag nadat de backfill voltooit).

V: Zijn onbewerkte gegevens op raakniveau opgeslagen in LLM Optimizer?

Nee. Slechts **samengevoegde** metriek worden gebruikt om verkeerspatronen en tendensen te begrijpen.

V: Zijn volledige URL&#39;s, querytekenreeksen of pagina-inhoud opgeslagen?

Volledige URL&#39;s die voor de geselecteerde paginadimensie worden gebruikt, kunnen worden opgenomen. Voor deze integratie worden queryreeksen en pagina-inhoud niet opgenomen.

V: Zijn de gebruikers-id&#39;s (ECID, IP-adres, cookie-id&#39;s) opgeslagen?

Nee.

V: Hoe lang worden gegevens bewaard?

Houd er rekening mee dat het retentiebeleid zich kan ontwikkelen. Gegevens worden momenteel voor onbepaalde tijd opgeslagen.

V: Zijn gegevens gecodeerd in doorvoer en in rust?

Gegevens worden momenteel gecodeerd in doorvoer en niet in rust. Dit kan in toekomstige updates veranderen.

V: Zijn historische gegevens teruggezet?

Ja. Na een geslaagde installatie worden de laatste vier volledige kalenderweken en de huidige kalenderweek teruggezet. Zie ook [ nadat u ](#after-connect) verbindt.
