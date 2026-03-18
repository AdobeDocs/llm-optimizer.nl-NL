---
title: Log Forwarding - Imperva
description: Leer hoe te om CDN- logboeken van Imperva aan Adobe S3 emmertje voor de inzameling van verkeersgegevens in LLM Optimizer door:sturen.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---


# Log doorsturen: Imperva {#log-forwarding-imperva}

Deze gids verklaart hoe te om CDN- logboeken van Imperva aan Adobe S3 emmertje voor de inzameling van agentic verkeersgegevens door:sturen. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het aan boord gaan proces volledig is, volg de stappen op deze pagina worden verstrekt om logboek door:sturen van de Imperva Webconsole te vormen die.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [&#x200B; https://llmo.now/](https://llmo.now/):

1. Ga naar **Configuratie**.

   ![&#x200B; knoop van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![&#x200B; CDN het lusje van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)
1. Klik **krijgen Begonnen**.
1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![&#x200B; vormen &#x200B;](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecteer **Imperva (BYOCDN)**.

   ![&#x200B; Uitgezochte Imperva &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-select.png)
1. Klik **Onboard**.

## Stap 2: Vorm logboek door:sturen in Imperva {#step-2}

Op de [&#x200B; console Imperva &#x200B;](https://my.imperva.com):

>[!NOTE]
>
>Logbestanden moeten dagelijks worden verzonden.

1. Login aan uw rekening Imperva in [&#x200B; https://my.imperva.com &#x200B;](https://my.imperva.com).

2. In sidebar, ga naar **Logboeken** > **Opstelling van het Logboek** (of **Integratie van het Logboek**).

3. Selecteer **Amazon S3 ARN** als verbindingstype (logboekbestemming).

4. Voer het volgende in:

   | Veld | Beschrijving | Opmerking |
   |---|---|---|
   | **naam van de Verbinding** | Een beschrijvende naam voor de verbinding (bijvoorbeeld productielogboeken S3). U kunt de standaardnaam wijzigen. | |
   | **Weg** | De locatie van de map waarin logbestanden worden opgeslagen. Gebruik de indeling `<Amazon S3 bucket name>/<log folder>` . Bijvoorbeeld: `MyBucket/MyImpervaLogFolder` . | `Amazon S3 bucket name` is de **Naam van het Emmertje** van de de configuratiepagina van LLM Optimizer. ![De Naam van het emmertje &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-bucket-name.png) de logboekomslag is **Weg** van de de configuratiepagina van LLM Optimizer. ![Pad &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-path.png) |

5. Klik **verbinding van de Test**. Imperva voert een volledige test uit waarin een testdossier (geen echte gegevens) naar de aangewezen omslag wordt verzonden en dan wordt verwijderd wanneer de overdracht volledig is.

   - **Beschikbaar** — de opslagdetails zijn geldig; u kunt logboeken vormen om deze verbinding te gebruiken.
   - **Niet gedefiniëerd** — of de vereiste details ontbreken of de ontbroken test.

6. Klik **sparen** om de configuratie op te slaan.

7. Vorm logboekopties (logboektypes, logboekniveau, formaat, compressie) en **Niveaus van het Logboek**. U kunt de waarden ophalen via de LLM Optimizer-configuratiepagina.

   | Veld | Opmerking |
   |---|---|
   | Modus voor logboekintegratie | ![&#x200B; de integratiemodus van het Logboek &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-log-integration-mode.png) |
   | Leveringsmethode | ![&#x200B; methode van de Levering &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-delivery-method.png) |
   | Logbestandstypen | ![&#x200B; de types van Logboek &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-log-types.png) |
   | Logboekniveau | ![&#x200B; Niveau van het Logboek &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-log-level.png) |
   | Indeling | ![&#x200B; Formaat &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-format.png) |
   | Logbestanden comprimeren | ![&#x200B; Compress logboeken &#x200B;](/help/overview/assets/log-forwarding/imperva/imperva-compress-logs.png) |
