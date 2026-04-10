---
title: Log Forwarding - CloudFront (AWS CLI)
description: CDN van CloudFront door:sturen aan Adobe S3 emmer gebruikend AWS CLI voor leveringsopstelling en verrichtingen.
feature: Agentic Traffic
source-git-commit: 3277e7f7f2e0c5e4693e40473d595b12d9e5f2e8
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---


# Log Forwarding: CloudFront (AWS CLI) {#log-forwarding-cloudfront-cli}

Op deze pagina ziet u hoe u CDN-logbestanden van CloudFront naar S3-emmertje van Adobe doorstuurt voor verzameling van hoekige verkeersgegevens. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het aan boord gaan proces volledig is, volg de stappen op deze pagina worden verstrekt om logboek door:sturen te vormen door de [&#x200B; Interface van de Lijn van het Bevel van AWS &#x200B;](https://aws.amazon.com/cli/) in [&#x200B; Stap 2 &#x200B;](#step-2-cli) te gebruiken.

>[!NOTE]
>
> Deze gids verklaart hoe te om logboek door:sturen te vormen door de [&#x200B; Interface van de Lijn van het Bevel van AWS &#x200B;](https://aws.amazon.com/cli/) te gebruiken. Als u logboek door:sturen wilt vormen door **CloudFront UI** te gebruiken, zie [&#x200B; Logboek door:sturen: CloudFront &#x200B;](/help/overview/log-forwarding/cloudfront.md).

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [&#x200B; https://llmo.now/](https://llmo.now/):

1. Ga naar het **dashboard van de Configuratie van de Klant**.

   ![&#x200B; knoop van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![&#x200B; CDN het lusje van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![&#x200B; vormen &#x200B;](/help/overview/assets/log-forwarding/common/configure.png)

1. Ga uw **identiteitskaart van de Rekening van AWS** in.

<!--  ![AWS Account ID](/help/overview/assets/log-forwarding/cloudfront/cloudfront-aws-account.png)-->

1. Selecteer **CloudFront (BYOCDN)**.

   ![&#x200B; Uitgezochte CloudFront &#x200B;](/help/overview/assets/log-forwarding/cloudfront/cloudfront-select.png)

1. Klik **Onboard**.

<!-- ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Stap 2: Het logboek van CDN van de opstelling door:sturen met AWS CLI {#step-2-cli}

CDN van de opstelling het logboek door:sturen met AWS CLI als volgt:

### AWS CLI-gebruikersgegevens configureren

AWS CLI referentie MAC instellen. Open ~/.aws/credentials en voer de waarden voor de onderstaande variabelen in:

```text
[LLMO]
aws_access_key_id=<VALUE_OF_ACCESS_KEY_ID>
aws_secret_access_key=<VALUE_OF_SECRET_KEY>
aws_session_token=<ONLY_IF_USING_SECURITY_TOKEN_SERVICE> ## Optional
```

### De verbinding testen

Voer de onderstaande opdracht uit om de verbinding te testen:

```bash
aws sts get-caller-identity --profile LLMO
```

Voorbeeld van een geslaagde uitvoer:

```bash
aws sts get-caller-identity --profile LLMO
{
    "UserId": "AxxxxxxxxxxxP:user",
    "Account": "012345678912",
    "Arn": "arn:aws:sts::012345678912:assumed-role/klam-master-role-BatlY3dnPVinQLC/user"
}
```

### Variabelen initialiseren

Vervang `REPLACEME123@AdobeOrg` door uw organisatie Adobe IMS Org ID en voer de onderstaande opdracht uit. De uitvoer-id van deze opdracht wordt `TRANSFORM_IMS_ID` genoemd.

```bash
echo "REPLACEME123@AdobeOrg" | sed 's/@AdobeOrg$//' | tr '[:upper:]' '[:lower:]'
```

Voer de waarden voor `CUSTOMER` , `CDN_ID` , `ACCT1` en `TRANSFORM_IMS_ID` in volgens de onderstaande hulplijn en voer vervolgens opdrachten uit vanaf de terminal.

```bash
export PROFILE1=LLMO
export REGION1=us-east-1
export CUSTOMER=<CUSTOMER_NAME> ## No Space, user letters,numbers and dash
export CDN_ID=<YOUR_CLOUDFRONT_DISTRIBUTION_ID>
export ACCT1=<YOUR_AWS_ACCOUNT_NUMBER>
export DELIVERY_DEST_ARN=arn:aws:logs:us-east-1:640168421876:delivery-destination:cdn-logs-<TRANSFORM_IMS_ID>-ams  ## Replace TRANSFORM_IMS_ID with the output of the command above 
```

<!--Use the **Delivery destination ARN** and org values from the LLM Optimizer CDN configuration page if they differ from the pattern above.-->

### De leveringsbron maken

Van de zelfde terminal waarin stap 3 werd uitgevoerd, stel hieronder het bevel in werking:

```bash
aws logs put-delivery-source --name llmo-cf-${CUSTOMER}-${CDN_ID} \
  --profile $PROFILE1 --region $REGION1 \
  --resource-arn arn:aws:cloudfront::${ACCT1}:distribution/${CDN_ID} \
  --log-type ACCESS_LOGS
```

>[!IMPORTANT]
>
>Als u de volgende fout krijgt, onderzoek naar de bestaande leveringsbron: *een fout voorkwam (ConflictException) wanneer het roepen van de verrichting PutDeliverySource: This ResourceId is reeds gebruikt in een andere Levering Source in deze rekening.*
>
>Als u naar de bestaande leveringsbron wilt zoeken, voert u deze opdracht uit:
>
>```bash
>aws logs describe-delivery-sources --region us-east-1 \
>--query "deliverySources[?contains(resourceArns[0], '<CDN DistributionID>')]"
>```
>
>In het volgende bevel, gebruik de naam van de leveringsbron van de resultaten van het bovengenoemde bevel.

### De leveringsconfiguratie maken

```bash
aws logs create-delivery \
  --profile "$PROFILE1" --region "$REGION1" \
  --delivery-source-name "llmo-cf-${CUSTOMER}-${CDN_ID}" \
  --delivery-destination-arn $DELIVERY_DEST_ARN \
  --s3-delivery-configuration '{"suffixPath":"/{yyyy}/{MM}/{dd}/{HH}"}' \
  --record-fields 'date' 'time' 'x-edge-location' 'cs-method' 'cs(Host)' 'cs-uri-stem' 'sc-status' 'cs(Referer)' 'cs(User-Agent)' 'time-to-first-byte' 'sc-content-type' 'x-host-header'
```

&lt;!—Lijn `--record-fields` en `--s3-delivery-configuration` uit met de veldlijst en het padachtervoegsel op de LLM Optimizer CDN-configuratiepagina als de documentatie of productwaarden veranderen.—>
