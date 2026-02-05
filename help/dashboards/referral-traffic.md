---
title: Verwijzingsverkeer
description: Leer hoe u het dashboard Referral-verkeer kunt gebruiken om te zien hoe bezoekers uw site bereiken via externe platforms, AI-citaties en verwijzingskoppelingen.
feature: Referral Traffic
source-git-commit: e50c87e8e5a669526f3c10855c1629ce82b67aef
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Verwijzingsverkeer

Het Verkeer van de verwijzing toont hoe de bezoekers bij uw plaats van externe platforms, AI citaties, en verwijzingsverbindingen aankomen. Het volgt en analyseert verkeersbronnen, verwijzingspatronen, en omzettingsmetriek van externe websites en platforms. Dit zal u helpen begrijpen welke bronnen, gebieden, en pagina&#39;s het meest betrokken verkeer drijven. <!--Data is sourced from the CDN logs, a privacy-preserving source that does not capture personal user data.--> Er zijn ook aanpasbare filters waarmee u de weergegeven gegevens kunt verfijnen.

![&#x200B; Verwijzing Pagina &#x200B;](/help/dashboards/assets/referral-traffic.png)

Op deze pagina vindt u het volgende:

* [Instellen](#setup)
* [Filters](#filters)
* [Algemene verwijzingsprestaties](#overall-performance)
* [URL&#39;s verwijzing bovenaan](#top-referrals)
* [Referral-verkeersdetails](#traffic-details)

## Instellen {#setup}

Bij de eerste aanmelding kan het dashboard Referral-verkeer leeg worden weergegeven. Om uw gegevens te bekijken, moet u [&#x200B; CDN logboek vormen door:sturen &#x200B;](/help/dashboards/customer-configuration.md#cdn-configuration), door te selecteren **ga naar Configuratie**.

![&#x200B; Opstelling van de Verwijzing &#x200B;](/help/dashboards/assets/referral-setup1.png)

<!--- 1. Select your Source (either CDN logs or AEM Operational Telemetry).
2. Enter a primary contact email.
3. Click **Request activation** to enable data ingestion. Hiding this until confirmation from PM-->

Zodra geactiveerd, zal het dashboard met verwijzingsverkeersmetriek worden bevolkt.

## Filters {#filters}

Boven aan de pagina kunt u filters toepassen om de weergave te verfijnen. De filters u kiest zullen **alle** secties beïnvloeden huidig op het dashboard. U kunt het volgende aanpassen:

* **de Waaier van de Datum** - selecteer het tijdkader voor de getoonde gegevens. Bijvoorbeeld de laatste 4 weken. U hebt ook de optie om de tijdperiode aan te passen door de **optie van de Weken van de Douane te selecteren**.
* **Platform** - kies een specifieke verkeersbron zoals Google, OpenAI, of sociale media.
* **Intentie van de Pagina** - het verwijzingsverkeer van de Filter door gebruikersinzet.
* **Source van het Kanaal** - filter door de bron van het kanaal. Dit zijn onder andere: LLM&#39;s, verdiende, betaalde of gemengde verwijzingskanalen.
* **Type van Apparaat** - analyseer verkeer door het apparatentype van de bezoeker of Desktop, mobiel of alle apparaten.
  **Gebied** - de verwijzingspatronen van de mening over verschillende geografische gebieden.

Nadat u de gewenste filter selecteert, klik **toepassen Filters** om de selectie op het dashboard toe te passen.

## Algemene verwijzingsprestaties {#overall-performance}

Het dashboard benadrukt de algemene verwijzingsprestaties door zeer belangrijke metriek met inbegrip van te tonen:

* **Totaal Verkeer van de Verwijzing** - het totale verwijzingsverkeer uit alle bronnen.
* **Verkeer van de verwijzing van LLM** - het totale verwijzingsverkeer van LLM.
* **Constante tarief** - het percentage bezoekers die een toestemmingsherinnering goedkeuren.
* **Stuitpercentage** - het percentage zittingen van verwijzingsbronnen die geen betrokkenheidsgebeurtenis hadden.

![&#x200B; Verwijzing Pagina &#x200B;](/help/dashboards/assets/referral-traffic.png)

Naast de algemene prestatiemetriek die hierboven wordt voorgesteld, zijn er drie extra panelen die de verkeersdistributie over verschillende markten, verwijzingsbronnen en de categorieën van de paginaintentie tonen <!-- the **Top Regions** panel breaks down traffic by geography. Meanwhile, the **Top Referral Sources** panel shows the platforms driving the most visits. Trend indicators for the metrics show how these values are changing over time compared to the previous period.-->

<!--## Top Referral URLs {#top-referrals}

The Top Referral URLs list surfaces your site's most visited pages from referrals.

![Top Referral URLs](/help/dashboards/assets/top-url.png)-->

## Referral-bronnen en URL-prestatieanalyse {#traffic-details}

De de gegevensdetails van de Bron van de Verwijzing en lijsten van de Analyse van de Prestaties URL helpen u zowel verkeersvolume als kwaliteit evalueren. Klik op elk tabblad hieronder voor meer informatie:

![&#x200B; Details van het Verkeer van de Verwijzing &#x200B;](/help/dashboards/assets/traffic-details.png)

>[!BEGINTABS]

>[!TAB  Brondetails van de Referral ]

De mening van de Details van de Bronnen van Referral onderbreekt verkeer dat uit verschillende platforms zoals OpenAI, Microsoft, Google, en Perplexiteit komt. Het toont zeer belangrijke metriek zoals bezoeken, stuitsnelheid en kanaaltype, die u helpen welke AI en onderzoeksbronnen het meest betrokken verkeer aan uw plaats drijven.

* **Source** - de bron van het verwijzingsverkeer.
* **bezoeken** - het totale aantal bezoeken voor elke bron.
* **Stuitpercentage** - het percentage zittingen van de verwijzingsbron die geen betrokkenheidsgebeurtenis had.
* **Kanaal** - het kanaal voor de bron, of verdiend, betaald of allebei.

>[!TAB  URL de Analyse van Prestaties ]

De URL mening van de Analyse van Prestaties rangschikt best-presterende pagina&#39;s die op verwijzingsverkeersvolume van LLMs en andere bronnen worden gebaseerd. Het benadrukt metriek zoals verkeer, stuitsnelheid, toestemmingstarief, en paginaintentie, die u helpt identificeren welke pagina&#39;s de meest betrokken bezoekers van AI-gedreven verwijzingen aantrekken en behouden. De lijst heeft een onderzoeksgebied voor snelle toegang tot onderwerpen.

>[!ENDTABS]

Op beide lijsten, kunt u de **Uitvoer** optie gebruiken om lijst .csv te downloaden en de inzichten met uw team te delen of de lijsten in uitvoerende rapportering te omvatten. Bovendien, voor beide lijsten, kunt u aanpassen welke metriek door te klikken **wordt getoond Kolommen** knoop vormen.
