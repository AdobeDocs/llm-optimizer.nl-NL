---
title: Log Forwarding - Cloudflare
description: Leer hoe te om CDN- logboeken van Cloudflare aan Adobe S3 emmertje voor de inzameling van verkeersgegevens in LLM Optimizer door:sturen.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Log doorsturen: wolkenflakkering {#log-forwarding-cloudflare}

Deze pagina details hoe te om CDN- logboeken van Cloudflare aan het emmertje van Adobe S3 voor de inzameling van hoekige verkeersgegevens door:sturen. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het aan boord gaan proces volledig is, volg de stappen op deze pagina worden verstrekt om logboek het door:sturen in de dashboardconsole van de Wolk te vormen die.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [&#x200B; https://llmo.now/](https://llmo.now/):

1. Ga naar het **dashboard van de Configuratie van de Klant**.

   ![&#x200B; knoop van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![&#x200B; CDN het lusje van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png) -->

1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![&#x200B; vormen &#x200B;](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecteer **Cloudflare (BYOCDN)**.

   ![&#x200B; Uitgezochte Cloudflare &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-select.png)

1. Klik **Onboard**.

   <!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Stap 2: Een Logpush-taak maken in Cloudflare {#step-2}

Op het [&#x200B; dashboard van de Wolk &#x200B;](https://dash.cloudflare.com/login), volg deze stappen:

1. Ga naar de **Logpush** pagina op het **Domein (streek)** niveau.
1. Selecteer **creeer een Logpush baan**.
1. In **selecteer een bestemming**, kies **Amazon S3**.
1. Voer de volgende doelgegevens in:

   - **Emmertje** — de naam van het S3 emmertje. Kopieer de waarde van de LLM Optimizer CDN-configuratiepagina.

     ![&#x200B; Naam van het Emmertje &#x200B;](/help/overview/assets/log-forwarding/common/bucket-name.png)

   - **Weg** — de emmer plaats binnen de opslagcontainer. Kopieer de waarde van de LLM Optimizer CDN-configuratiepagina.

     ![&#x200B; Cloudflare weg &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-path.png)

   - **organiseer logboeken in dagelijkse subfolders** (geadviseerd).

     ![&#x200B; Dagelijkse subfolders &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-daily-subfolders.png)

   - **gebied van het Emmertje** — kopieer de waarde van de pagina van de Configuratie van LLM Optimizer CDN.

     <!-- ![Region](/help/overview/assets/log-forwarding/cloudflare/cloudflare-region.png)-->

   - Laat de optie uitgeschakeld als codering op de server niet nodig is.

   Nadat u de stappen hierboven voltooit, uitgezochte **gaat** verder.

1. Cloudflare stuurt een bestand naar de door u aangewezen bestemming om het eigendom te bewijzen. Om het teken te vinden, klik de **Open** knoop in het **Overzicht** lusje van het dossier van de eigendomsuitdaging. Kopieer het eigendomstoken van de LLM Optimizer CDN-configuratiepagina en plak het in het dashboard Wolk om uw toegang tot het emmertje te verifiëren. Ga het Token van de Eigendom in en selecteer **verdergaan**.

   <!--![Ownership token](/help/overview/assets/log-forwarding/cloudflare/cloudflare-ownership-token.png)-->

1. Selecteer de **dataset van HTTP- Verzoeken** aan duw aan de opslagdienst.

1. Configureer uw Logpush-taak:

   - Ga de **naam van de Baan** in.

   - In **verzend de volgende gebieden**, zie de waarden in de configuratiepagina van LLM Optimizer.

     ![&#x200B; Logpush gebieden &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-logpush-fields.png)

   - **formaat van het Logboek**: JSON.

     <!--![JSON format](/help/overview/assets/log-forwarding/cloudflare/cloudflare-json-format.png)-->

1. In **Geavanceerde Opties**:

   - Kies de indeling van tijdstempelvelden in uw logboeken: `RFC3339` .

     ![&#x200B; formaat van de Chronologie &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-timestamp-format.png)

   - Voor steekproeftarieven, selecteer **Alle logboeken**.

     ![&#x200B; Bemonsteringsfrequentie &#x200B;](/help/overview/assets/log-forwarding/cloudflare/cloudflare-sampling-rate.png)

1. Selecteer **voorleggen** zodra u klaar bent vormend de Logpush baan.
