---
title: Verwijzingsverkeer
description: Dit is het artikeloverzicht.
source-git-commit: c83b4929a82331534654fcfdccd41d91eefe6d92
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Verwijzingsverkeer

Het Verkeer van de verwijzing toont hoe de bezoekers bij uw plaats van externe platforms, AI citaties, en verwijzingsverbindingen aankomen. Het volgt en analyseert verkeersbronnen, verwijzingspatronen, en omzettingsmetriek van externe websites en platforms. Dit zal u helpen begrijpen welke bronnen, gebieden, en pagina&#39;s het meest betrokken verkeer drijven. De gegevens zijn afkomstig van of de CDN- logboeken of de Operationele Telemetrie van AEM **(voeg verbinding toe)**. Beide bronnen zijn privacybescherming en leggen geen persoonlijke gebruikersgegevens vast.

Er zijn ook aanpasbare filters waarmee u de weergegeven gegevens kunt verfijnen.

Op deze pagina vindt u het volgende:

* [Instellen](#setup)
* [Filters](#filters)
* [Algemene verwijzingsprestaties](#overall-performance)
* [URL&#39;s verwijzing bovenaan](#top-referrals)
* [Referral-verkeersdetails](#traffic-details)

## Instellen {#setup}

Bij de eerste aanmelding kan het dashboard Referral-verkeer leeg worden weergegeven. Om uw gegevens te bekijken, moet u een verwijzingsverkeersleverancier vormen.

![ Opstelling van de Verwijzing ](/help/dashboards/assets/referral-setup.png)

1. Selecteer uw Source (CDN-logboeken of AEM Operational Telemetry).
2. Voer een e-mail met primaire contactpersoon in.
3. Klik **activering van het Verzoek** om gegevensopname toe te laten.

Zodra geactiveerd, zal het dashboard met verwijzingsverkeersmetriek bevolken.

## Filters {#filters}

Boven aan de pagina kunt u filters toepassen om de weergave te verfijnen. De filters u kiest zullen **alle** secties beïnvloeden huidig op het dashboard. U kunt het volgende aanpassen:

**de Waaier van de Datum** - selecteer het tijdkader voor de getoonde gegevens. Bijvoorbeeld de laatste 4 weken. U hebt ook de optie om de tijdperiode aan te passen door de **optie van de Weken van de Douane te selecteren**.
**Platform** - kies een specifieke verkeersbron zoals Google, OpenAI, of sociale media.
**Kanaal** - filter tussen kanalen zoals verdiend of betaald. Als u een mengeling tussen twee verkiest selecteer **Alle Kanalen** optie.
**Source van het Kanaal** - filter door de bron van het kanaal. opties zijn onder meer: weergeven, zoeken, doorverwijzen, video en sociaal. U kunt **Alle Platforms** ook gebruiken om alle kanaalbronnen te tonen.
**Type van Apparaat** - analyseer verkeer door het apparatentype van de bezoeker of Desktop, mobiel of alle apparaten.
**Gebied** - de verwijzingspatronen van de mening over verschillende geografische gebieden.

Nadat u de gewenste filter selecteert, klik **toepassen Filters** om de selectie op het dashboard toe te passen.

## Algemene verwijzingsprestaties {#overall-performance}

Het dashboard benadrukt de algemene verwijzingsprestaties door de volgende belangrijkste metriek te tonen:

* **Totaal Verkeer van de Verwijzing** - het totale verwijzingsverkeer uit alle bronnen.
* **Constante tarief** - het percentage bezoekers die een toestemmingsherinnering goedkeuren.
* **Stuitpercentage** - het percentage zittingen van verwijzingsbronnen die geen betrokkenheidsgebeurtenis hadden.

![ Verwijzing Pagina ](/help/dashboards/assets/referral-traffic.png)

Naast de algemene prestatiesmetriek die hierboven wordt voorgesteld, onderbreekt het **Hoogste Gebieden** paneel verkeer door geografie. Ondertussen, toont het **Belangrijkste paneel van de Verwijzing Bronnen** de platforms die de meeste bezoeken drijven.

## URL&#39;s verwijzing bovenaan {#top-referrals}

De lijst URL&#39;s met verwijzingen naar verwijzingen bevat de meest bezochte pagina&#39;s van uw site.

![ Hoogste Verwijzing URLs ](/help/dashboards/assets/top-url.png)

## Referral-verkeersdetails {#traffic-details}

De lijst van de Details van het Verkeer van de Verwijzing helpt u zowel verkeersvolume als kwaliteit evalueren. Het verstrekt een gedetailleerde uitsplitsing door bron, met inbegrip van bezoektellingen, stuittarieven, en kanaaltype.

![ Details van het Verkeer van de Verwijzing ](/help/dashboards/assets/traffic-details.png)

De tabel bevat de volgende categorieën:

**Source** - de bron van het verwijzingsverkeer.
**bezoeken** - het totale aantal bezoeken voor elke bron.
**Stuitpercentage** - het percentage zittingen van de verwijzingsbron die geen betrokkenheidsgebeurtenis had.
**Kanaal** - het kanaal voor de bron, of verdiend, betaald of allebei.

U kunt de **optie van de Uitvoer** gebruiken om lijst.csv te downloaden en de inzichten met uw team te delen of de verwijzingsverkeerstabel in uitvoerende rapportering te omvatten.
