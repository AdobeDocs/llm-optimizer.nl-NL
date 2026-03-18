---
title: Log Forwarding - CloudFront
description: Leer hoe u CDN-logboeken doorstuurt van CloudFront naar Adobe S3 bucket voor verzameling van hoekige verkeersgegevens in LLM Optimizer.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Log doorsturen: CloudFront {#log-forwarding-cloudfront}

Deze pagina verklaart hoe te om CDN- logboeken van CloudFront aan het S3 emmertje van Adobe voor de inzameling van hoekige verkeersgegevens door:sturen. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het instapproces is voltooid, volgt u de stappen op deze pagina om het doorsturen van logbestanden te configureren in de dashboardconsole van CloudFront.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [ https://llmo.now/](https://llmo.now/):

1. Ga naar het **dashboard van de Configuratie van de Klant**.

   ![ knoop van de Configuratie ](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![ CDN het lusje van de Configuratie ](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![ vormen ](/help/overview/assets/log-forwarding/common/configure.png)

1. Ga uw **identiteitskaart van de Rekening van AWS** in.

   ![ identiteitskaart van de Rekening van AWS ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)

1. Selecteer **CloudFront (BYOCDN)**.

   ![ Uitgezochte CloudFront ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Klik **Onboard**.

   ![ knoop Onboard ](/help/overview/assets/log-forwarding/common/onboard-button.png)

## Stap 2: Standaardlogboekregistratie inschakelen (CloudFront-console) {#step-2}

Om standaardregistreren toe te laten, van de [ console van het Beheer van AWS ](https://aws.amazon.com/console/):

1. Heb toegang tot de [ console CloudFront ](https://console.aws.amazon.com/cloudfront/v4/home) en [ werk een bestaande distributie ](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/HowToUpdateDistribution.html#HowToUpdateDistributionProcedure) bij.

1. Open het **Registreren** lusje.

1. Kies **toevoegen**, dan de dienst om logboeken te ontvangen, in dit geval **Amazon S3**.

1. Voor **Bestemming**, selecteer of creeer het middel. Ga de **emmernaam** in, kunt u de waarde van de de configuratiepagina van LLM Optimizer kopiëren CDN.

   ![ CloudFront emmernaam ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-bucket-name.png)

1. Vorm **Extra montages**:

   - **selectie van het Gebied** — kies de gebieden van het logboekdossier. Zie de vereiste gebieden op de LLM Optimizer CDN configuratiepagina.

     ![ CloudFront gebiedsselectie ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-field-selection.png)

   - **het Verdelen** — kopieer het **wegachtervoegsel** van de de configuratiepagina van LLM Optimizer.

     ![ CloudFront het verdelen ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-partitioning.png)

   - **formaat van de Output** — het formaat zou JSON moeten zijn.

     ![ CloudFront outputformaat ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-output-format.png)

1. Voer de stappen uit om de distributie bij te werken of te maken.

1. Op de **Logboeken** pagina, bevestig dat **Toegelaten** naast de distributie verschijnt.

## Standaardlogboekregistratie inschakelen voor levering tussen accounts {#cross-account}

De **bronrekening** (met de distributie CloudFront) verzendt toegangslogboeken naar de **bestemmingsrekening** (het S3 emmer dat in de de configuratiepagina van LLM Optimizer CDN wordt getoond). Beide accounts moeten de juiste machtigingen hebben.

Bijvoorbeeld: de bronaccount `111111111111` verzendt logbestanden naar een S3-emmertje in een doelaccount `222222222222` . U kunt de [ Interface van de Lijn van het Bevel van AWS gebruiken ](https://aws.amazon.com/cli/).

>[!NOTE]
>
>In de bevelen hieronder, vervang de waarde van de leveringsbestemmingsARN (`arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination`) met de waarde van **bestemmingsARN van de Levering** van de de configuratiepagina van LLM Optimizer.

![ bestemmingsARN van de Levering ](/help/overview/assets/log-forwarding/cloudfront/cloudfront-delivery-destination-arn.png)

### De bronaccount configureren {#source-account}

Vervolgens moet u de bronaccount configureren:

1. **creeer een leveringsbron** - vervang de naam en distributie ARN:

   ```bash
   aws logs put-delivery-source --name s3-cf-delivery \
     --resource-arn arn:aws:cloudfront::111111111111:distribution/E1TR1RHV123ABC \
     --log-type ACCESS_LOGS
   ```

1. **creeer de levering** - verbindingsbron aan bestemming; gebruik bestemmingsARN van de &quot;vorm de stap van de bestemmingsrekening&quot;:

   ```bash
   aws logs create-delivery --delivery-source-name s3-cf-delivery \
     --delivery-destination-arn arn:aws:logs:us-east-1:222222222222:delivery-destination:cloudfront-delivery-destination
   ```

1. **verifieer:**

   - In de **bron** rekening: console CloudFront > uw distributie > **het Registreren** tabel. Onder **Type** zou u de S3 levering van het dwars-rekeningslogboek moeten zien.
   - In de **bestemmings** rekening: S3 console > emmer. Het voorvoegsel (bijvoorbeeld `MyLogPrefix` ) en de logbestanden in die map moeten worden weergegeven.
