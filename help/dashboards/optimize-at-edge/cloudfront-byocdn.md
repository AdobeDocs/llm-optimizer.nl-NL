---
title: Optimaliseren bij Edge - CloudFront (BYOCDN)
description: Leer hoe u CloudFront BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 1253d0f0a58f6523699c52fbfab23028dc469c82
workflow-type: tm+mt
source-wordcount: '2228'
ht-degree: 0%

---


# CloudFront (BYOCDN)

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de configuratie van CloudFront instelt, moet u controleren of:

* Een bestaande CloudFront-distributie die uw website bedient.
* AWS IAM-machtigingen om Lambda-functies, IAM-rollen, CloudFront-distributies en cachebeleid te maken.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Stap 1: Creeer Edge optimaliseren Oorsprong**

**Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > het lusje van Oorsprong

1. Klik **creeer oorsprong**.

2. De oorsprong configureren:
   * **Origineel domein:** `live.edgeoptimize.net`
   * **Naam:** `EdgeOptimize_Origin`

3. Laat de standaardwaarden van alle andere velden ongewijzigd.

4. Aangepaste kopteksten toevoegen:

   | Koptekst | Waarde |
   |--------|-------|
   | `x-edgeoptimize-api-key` | Uw API-sleutel |
   | `x-forwarded-host` | `www.example.com` |

   Vervang `www.example.com` door uw huidige websitedomein en `Your API key` door de Edge Optimize API-sleutel die wordt geleverd door uw Adobe-vertegenwoordiger.

5. Klik **creeer oorsprong**.

![&#x200B; Cloudfront Origin Creation &#x200B;](/help/assets/optimize-at-edge/cloudfront-origin-creation.png)

**Stap 2: Creeer de functie van het kijkerverzoek**

**Navigatie:** AWS Console > CloudFront > Functies

1. Klik **creëren functie**.

2. Configureren:
   * **Naam:** `edgeoptimize-routing`
   * **Runtime:** `cloudfront-js-2.0`

3. Vervang de standaardcode met de code van [&#x200B; viewer-request.js &#x200B;](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/cloudfront-function/viewer-request.js).

   Pas de volgende waarden in de code aan voordat u publiceert:

   * `YOUR_DEFAULT_ORIGIN` — Vervang met de naam van uw bestaande standaardoorsprong (die in CloudFront > Verspreidingen wordt gevonden > [ Uw Distributie ] > het lusje van Oorsprong).
   * `TARGETED_PATHS` — Ingesteld op `null` om alle HTML-pagina&#39;s als doel in te stellen, of op een array van specifieke paden, bijvoorbeeld `['/', '/products', '/about']` .

4. Klik **sparen veranderingen** > **publiceer functie**.

![&#x200B; Cloudfront functie creatie &#x200B;](/help/assets/optimize-at-edge/cloudfront-function-creation.png)


**Stap 3: Vorm geheim voorgeheugenbeleid**

**Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > Gedrag

Controleer het cachebeleid dat momenteel aan uw gedrag is gekoppeld. Klik **uitgeven** op uw gedrag en bekijk de **sleutel van het Geheime voorgeheugen en de oorsprongverzoeken** sectie om uw scenario te identificeren:

* **Scenario A (Verouderd):** u ziet een radioknoop geëtiketteerd **de montages van het geheime voorgeheugen van de Verouderde erfenis** geselecteerd. Er is geen beleidsnaam dropdown — in plaats daarvan ziet u inline TTL en kopbalmontages.
* **Scenario B (het beleid van de Douane):** u ziet **Beleid van het Geheime voorgeheugen** geselecteerd met een beleidsnaam die u of uw team (geen AWS-Geleverd beleid) creeerde.
* **Scenario C (Beheerd beleid):** u ziet **Beleid van het Geheime voorgeheugen** dat met een AWS-Geleide naam zoals `CachingOptimized` wordt geselecteerd, `CachingDisabled`, of `CachingOptimizedForUncompressedObjects` — deze kunnen niet worden uitgegeven.

**Scenario A: De montages van het geheime voorgeheugen van de erfenis**

Als uw gedrag oude cacheinstellingen gebruikt:

1. Onder **sleutel van het Geheime voorgeheugen en oorsprongsverzoeken**, zult u **geselecteerde het geheim voorgeheugenmontages van de Verouderde** zien.

2. Voeg `x-edgeoptimize-config` en `x-edgeoptimize-url` aan de **lijst van gewenste personen van Kopballen** toe:

   * Selecteer **omvatten de volgende kopballen** van dropdown.
   * Voeg `x-edgeoptimize-config` en `x-edgeoptimize-url` toe.
     ![&#x200B; Cloudfront de Verouderde van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-legacy.png)

   Als u reeds **allen** hebt geselecteerd in dropdown Kopballen, overslaat deze stap — alle kopballen worden automatisch door:sturen aan de oorsprong.

3. Controleer het **Voorwerp caching** plaatsen:

   * Als de reeks aan **&#x200B;**&#x200B;aanpast - het wordt geadviseerd om **Minimale TTL** aan `0` te plaatsen. Nochtans, als uw huidige MinimumTTL reeds zeer kort is, kunt u niet het hoeven te veranderen.
   * Als de reeks aan **kopballen van het oorsprongscache van het Gebruik** — geen verandering nodig.

4. Klik **sparen veranderingen**.

**Scenario B: Niet erfenis met een beleid van het douanegeheime voorgeheugen**

Als uw gedrag reeds een beleid van het douanegeheime voorgeheugen gebruikt (u creeerde, niet een AWS geleid beleid):

**Navigatie:** AWS Console > CloudFront > Beleid > Geheime voorgeheugen

1. Klik op het bestaande beleid.

2. Klik **uitgeven**.

3. Het wordt geadviseerd om **Minimale TTL** aan `0` te plaatsen. Nochtans, als uw huidige MinimumTTL reeds zeer kort is, kunt u niet het hoeven te veranderen.
   ![&#x200B; montages van beleidTTL van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

4. Onder **zeer belangrijke montages van het Geheime voorgeheugen** > **Kopballen**, samen met uw bestaande opneming, voeg `x-edgeoptimize-config` en `x-edgeoptimize-url` toe.
   ![&#x200B; de beleidskopballen van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

5. Klik **sparen veranderingen**.

**Scenario C: Niet erfenis met een beheerd (AWS) geheim voorgeheugenbeleid**

Als uw gedrag een door AWS beheerd cachebeleid (bijvoorbeeld `CachingOptimized` ) gebruikt, kunt u dit niet bewerken. U moet een nieuw beleid van het douanegeheime voorgeheugen tot stand brengen dat de bestaande beheerde beleidsmontages herhaalt en Edge toevoegt optimaliseert kopballen bovenop.

**Deel 1: Nota neer uw huidige beheerde montages van het geheim voorgeheugenbeleid**

**Navigatie:** AWS Console > CloudFront > Beleid > Geheime voorgeheugen

1. Zoek en klik op het beheerde cachebeleid dat momenteel is gekoppeld aan uw gedrag (bijvoorbeeld `CachingOptimized` ).

2. Noteer alle bestaande instellingen:
   * Minimale TTL, Maximum TTL, Standaard TTL
   * Kopteksten die zijn opgenomen in de cachemoets
   * Cookies die zijn opgenomen in de cachemoets
   * Query-tekenreeksen opgenomen in de cachemoets
   * Ondersteuning voor compressie (Gzip, Brotli)

**Deel 2: Creeer een nieuw beleid van het douanegeheime voorgeheugen met de zelfde montages + Edge optimaliseren config**

**Navigatie:** AWS Console > CloudFront > Beleid > Geheime voorgeheugen

1. Klik **creeer geheim voorgeheugenbeleid**.

2. **Naam:** `edgeoptimize-cache`

   ![&#x200B; het beleidsnaam van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-name.png)

3. Herhaal alle in deel 1 vermelde instellingen met de volgende wijzigingen:

   * Het wordt geadviseerd om **Minimale TTL** aan `0` te plaatsen. Nochtans, als uw huidige MinimumTTL reeds zeer kort is, kunt u niet het hoeven te veranderen.

   ![&#x200B; montages van beleidTTL van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-ttl.png)

   * Onder **de zeer belangrijke montages van het Geheime voorgeheugen** > **Kopballen**, omvat alles het beheerde beleid had, plus `x-edgeoptimize-config` en `x-edgeoptimize-url` toevoegen.

   ![&#x200B; de beleidskopballen van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-cache-policy-headers.png)

4. Klik **creëren**.

5. Ga terug naar uw gedrag en associeer het pas gecreëerde beleid:

   **Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > Gedrag

   1. Bewerk uw gedrag.
   2. Onder **sleutel van het Geheime voorgeheugen en oorsprongsverzoeken**, uitgezocht **beleid van het Geheime voorgeheugen**.
   3. Kies `edgeoptimize-cache` in de vervolgkeuzelijst.
   4. Klik **sparen veranderingen**.

**Stap 4: Creeer Lambda@Edge functie (oorsprongverzoek en reactie)**

>[!IMPORTANT]
>Lambda@Edge de functies **moeten in het `us-east-1` (Noord) gebied** worden gecreeerd. Dit is een AWS-vereiste. Hoewel de functie is gemaakt in `us-east-1` , wordt deze door AWS automatisch gerepliceerd naar alle CloudFront edge-locaties wereldwijd, zodat deze wordt uitgevoerd op de dichtstbijzijnde randlocatie naar de viewer. Zorg ervoor dat u zich in het `us-east-1` -gebied in de AWS-console bevindt voordat u verdergaat.

**creeer de functie Lambda**

**Navigatie:** de Console van AWS > Lambda

1. Klik **creëren functie**.

2. Selecteer **Auteur van kras**.

3. Configureren:
   * **Naam van de Functie:** `edgeoptimize-origin`
   * Laat de standaardwaarden van alle andere velden ongewijzigd.

4. Klik **creëren functie**.

5. In de coderedacteur, vervang de standaardcode met de code van [&#x200B; oorsprong-verzoek-response.js &#x200B;](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/origin-request-response.js).

6. Klik **opstellen** om de code te bewaren.

7. Noteer de **naam van de uitvoeringsrol** die onder **wordt getoond Configuratie** > **Toestemmingen** (bijvoorbeeld, `edgeoptimize-origin-role-xxxxx`). U hebt dit in de volgende stappen nodig.

**werk het het vertrouwensbeleid van de uitvoeringsrol** bij

De automatisch gemaakte rol vertrouwt alleen op `lambda.amazonaws.com` . Voor Lambda@Edge moet u ook `edgelambda.amazonaws.com` toevoegen.

**Navigatie:** de Console van AWS > IAM > Rollen > [ uw rol van de vorige stap ] > de relaties tabel van het Vertrouwen

1. Klik **uitgeven vertrouwensbeleid**.

2. Vervang het beleid met de inhoud van [&#x200B; trust-policy.json &#x200B;](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/trust-policy.json).

3. Klik **beleid van de Update**.

>[!WARNING]
>Het `edgelambda.amazonaws.com` de diensthoofd wordt **vereist** voor Lambda@Edge. Zonder deze functie kan CloudFront uw functie niet aanroepen op randlocaties.

**bevestig het de toestemmingsbeleid van Logboeken CloudWatch**

De auto-gecreeerde rol komt met een `AWSLambdaBasicExecutionRole` beleid dat voor regelmatige Lambda wordt gevormd, die het verkeerde gebied en de naam van de logboekgroep voor Lambda@Edge heeft. U moet het bijwerken.

**Navigatie:** de Console van AWS > IAM > Rollen > [ uw rol ] > het lusje van Toestemmingen > klikt op de in bijlage beleidsnaam (bijvoorbeeld, `AWSLambdaBasicExecutionRole-xxxx`)

1. Klik **uitgeven**.

2. Vervang het beleid met de inhoud van [&#x200B; cloudwatch-policy.json &#x200B;](https://github.com/adobe-rnd/llmo-edge-optimize-samples/blob/main/cloudfront/lambda/cloudwatch-policy.json).

   Vervang `ACCOUNT_ID` in de JSON door de werkelijke AWS-account-id (in de rechterbovenhoek van de AWS-console) en `FUNCTION_NAME` door de naam van de Lambda-functie (bijvoorbeeld `edgeoptimize-origin` ).

3. Klik **sparen veranderingen**.

>[!WARNING]
>Het gebied in de ARN moet `*` zijn — Lambda@Edge wordt op de dichtstbijzijnde randlocatie uitgevoerd naar de viewer. Logbestanden worden dus geschreven naar CloudWatch in het gebied van de randlocatie (bijvoorbeeld `ap-south-1` , `eu-west-1` ), niet noodzakelijkerwijs `us-east-1` . De loggroep gebruikt de naam `/aws/lambda/us-east-1.FUNCTION_NAME`, waarbij `us-east-1` altijd het thuisgebied van de functie is.

**publiceer een versie**

1. Voor de functiepagina, klik **Acties** (hoogste recht) > **publiceren nieuwe versie**.

2. Voeg een beschrijving toe.

3. Klik **publiceren**.
   ![&#x200B; Lambda publiceert &#x200B;](/help/assets/optimize-at-edge/cloudfront-lambda-publish.png)

4. Kopieer of neem nota onderaan **ARN van de Functie** — u hebt dit in de volgende stap nodig.
   ![&#x200B; Lambda ARN &#x200B;](/help/assets/optimize-at-edge/cloudfront-lambda-arn.png)

**Stap 5: Koppel de functies en geheim voorgeheugenbeleid met gedrag**

**Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > Gedrag

1. Bewerk uw gedrag.

2. Als u een nieuw geheim voorgeheugenbeleid in Stap 3 (Scenario C) creeerde, plaats **beleid van het Geheime voorgeheugen** aan `edgeoptimize-cache`.
   ![&#x200B; Beleid van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/cloudfront-behaviour-cache.png)

3. Onder **associaties van de Functie**, vorm:

   * **verzoek van de Kijker:** `edgeoptimize-routing`
   * **verzoek van de Oorsprong:** Versioned ARN van de Functie van Stap 4 (in **publiceer een versie**)
   * **Oorsprong reactie:** Versioned ARN van de Functie van Stap 4 (in **publiceer een versie**)

   ![&#x200B; de associatieconfiguratie van de Functie &#x200B;](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Klik **sparen veranderingen**.

**Stap 6: Test de configuratie**

**1. Het verkeer van de Bot van de test (zou moeten worden geoptimaliseerd)**

Verzend een verzoek met een agentische beide gebruikersagent. Op het **eerste verzoek**, optimaliseert Edge kan een proxy (niet-geoptimaliseerde) reactie terugkeren terwijl het de pagina verwerkt en in cache plaatst. U kunt dit herkennen aan de header van `x-edgeoptimize-proxy: 1` in de reactie.

Simuleer een AI bot request using an agentic user-agent:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

Een succesvol antwoord bevat de header `x-edgeoptimize-request-id` , waarmee wordt bevestigd dat het verzoek is gerouteerd via Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Het menselijke verkeer van de test (zou NIET moeten worden beïnvloed)**

Simuleer een regelmatig verzoek van een menselijke browser:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

De reactie zou **&#x200B;**&#x200B;niet `x-edgeoptimize-request-id` kopbal moeten bevatten. De pagina-inhoud en de reactietijd moeten gelijk blijven aan voordat u Optimaliseren in Edge inschakelt.

**3. Hoe te tussen de twee scenario&#39;s te onderscheiden**

| Koptekst | Bot-verkeer (geoptimaliseerd) | Menselijk verkeer (niet beïnvloed) |
|---|---|---|
| `x-edgeoptimize-request-id` | Huidig — bevat een unieke aanvraag-id | Afwezig |
| `x-edgeoptimize-fo` | Alleen aanwezig als failover is opgetreden (waarde: `1`) | Afwezig |

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

**4. Verifieer de logboeken correct stromen**

Nadat u de bovenstaande testaanvragen hebt uitgevoerd, controleert u of er logbestanden worden geschreven voor zowel de functie CloudFront als de functie Lambda@Edge.

*CloudFront functielogboeken (`edgeoptimize-routing`)*

**Navigatie:** AWS Console > CloudWatch > de groepen van het Logboek (in `us-east-1` of het gebied waar uw distributie CloudFront wordt gevormd)

1. Zoek een loggroep met de naam `/aws/cloudfront/function/edgeoptimize-routing` .
2. Open de meest recente logstream.
3. Voor agentische verzoeken, zou u ingangen zoals moeten zien:
   * `Adding origin group for userAgent: chatgpt-user`
   * `Routing to Edge Optimize origin for userAgent: chatgpt-user`
4. Voor niet-agentische verzoeken, zou u moeten zien:
   * `Routing to Default origin for userAgent: ...`

U kunt het **lusje van Metriek** onder **Console van AWS > CloudFront > Functies > aanpassen-verpletteren** aan meningsaanroepingtellingen en foutentarieven ook controleren.

*Lambda@Edge logboeken (`edgeoptimize-origin`)*

>[!IMPORTANT]
>Lambda@Edge de logboeken worden geschreven aan CloudWatch in het **gebied van de randplaats** die het verzoek, niet `us-east-1` diende. Controleer CloudWatch in het AWS-gebied dat het dichtst bij de locatie ligt waar u de curl-opdracht hebt uitgevoerd.

**Navigatie:** AWS Console > CloudWatch > de groepen van het Logboek (zorg ervoor u in het correcte gebied bent)

1. Zoek een loggroep met de naam `/aws/lambda/us-east-1.edgeoptimize-origin` .
2. Open de meest recente logstream.
3. Voor agentische verzoeken, zou u ingangen zoals moeten zien:
   * `Calling Edge Optimize Origin for agentic requests` — primair pad
   * `Calling Default Origin in case of failover for agentic requests` — uitvalbeveiligingspad
   * `Failover Triggered for agentic requests` — failover-detectie van oorsprong en antwoord

Als de logboekgroep niet aanwezig is, verifieer dat de toestemmingen IAM correct in Stap 4 werden bijgewerkt. Controleer ook andere nabijgelegen AWS-regio&#39;s. De randlocatie die uw verzoek heeft gedaan, kan afwijken van wat u verwacht.

**Problemen oplossen**

| Probleem | Mogelijke oorzaak | Oplossing |
|-------|----------------|----------|
| Geen `x-edgeoptimize-request-id` in reactie op agentische aanvragen | Oorspronkelijke groep die niet naar Edge Optimize routeert | Controleer of `YOUR_DEFAULT_ORIGIN` correct is vervangen in de code van de functie CloudFront (stap 2). |
| 403 fouten op agentische verzoeken | Ongeldige of ontbrekende API-sleutel | Controleer de headerwaarde `x-edgeoptimize-api-key` in de aangepaste kopteksten voor Edge optimaliseren (stap 1). |
| Kan geen CloudWatch-logbestanden vinden voor Lambda@Edge | Onjuiste IAM-machtigingen | Controleer of het machtigingsbeleid van de CloudWatch-logbestanden is bijgewerkt (stap 4). Opmerking: Lambda@Edge-logbestanden worden weergegeven in het randgebied dat de aanvraag heeft verzonden, niet noodzakelijkerwijs in `us-east-1` . |
| Cache blijft niet behouden `cache-control: no-store` | Minimale TTL kan te hoog zijn | Plaats MinimumTTL aan `0` in uw geheim voorgeheugenbeleid (Stap 3). Als uw Minimale TTL reeds zeer kort is, kan dit niet de kwestie zijn. |
| Regelmatig (niet-opgewonden) verkeer gebroken na opstelling | Onjuiste configuratie cachebeleid | Als u een nieuw geheim voorgeheugenbeleid (Scenario C) creeerde, zorg ervoor u alle montages van het originele beheerde beleid herhaalde. |

**onbruikbaar makend en re-toelatend optimaliseer bij Edge**

De functie Lambda@Edge (`edgeoptimize-origin`) is gekoppeld aan de gebeurtenissen voor de oorspronkelijke aanvraag en de oorspronkelijke reactie van uw gedrag in CloudFront. Omdat het inline loopt op elk verzoek dat door dat gedrag gaat — zowel menselijk als agentisch — een Lambda@Edge stroomonderbreking zal al levend verkeer beïnvloeden, niet alleen agentische verzoeken. Als u een Lambda@Edge stroomonderbreking ontdekt, verwijder de functieverenigingen onmiddellijk om normale verkeersstroom aan uw standaardoorsprong te herstellen.

**hoe te om een Lambda@Edge stroomonderbreking** te ontdekken

* **de Gezondheidsdashboard van de Dienst van AWS** - controleer het [&#x200B; Dashboard van de Gezondheid van de Dienst van AWS &#x200B;](https://health.aws.amazon.com/health/status) voor om het even welke actieve incidenten die **Amazon CloudFront** of **AWS Lambda** beïnvloeden. Een wereldwijde of regionale uitval die hier wordt gemeld, is de snelste manier om dit probleem te bevestigen, is aan de kant van de AWS-infrastructuur in plaats van in uw configuratie.
* **Lambda@Edge fouten** — Navigeer aan **Console van AWS > CloudFront > Controle > [ Uw Distributie]**. Open de **Lambda@Edge fouten** tabel en controleer de **foutengrafiek van de Uitvoering** voor uitvoeringsfouten. Als deze hoog zijn, kan Lambda@Edge neer zijn.

**Ontstekend de functie Lambda@Edge**

**Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > Gedrag

1. Klik **uitgeven** op uw gedrag.

2. De rol neer aan de **verenigingen van de Functie** sectie.

3. Plaats de volgende verenigingen aan **Geen vereniging**:

   | Gebeurtenis | Wijzigen in |
   |---|---|
   | Viewer-verzoek | Geen koppeling |
   | Aanvraag oorsprong | Geen koppeling |
   | Oorspronkelijke reactie | Geen koppeling |

   ![&#x200B; de associatieconfiguratie van de Functie &#x200B;](/help/assets/optimize-at-edge/cloudfront-no-function-association.png)

4. Klik **sparen veranderingen**.

5. Wacht tot de distributie van CloudFront klaar is met de implementatie. De statusveranderingen van **het Opstellen** aan de laatste gewijzigde datum, typisch binnen een paar notulen.

Zodra opgesteld, alle verkeersroutes direct aan uw standaardoorsprong. Geen configuratie wordt geschrapt; de functie Lambda en zijn verenigingen kunnen op elk ogenblik worden hersteld.

**re-attaching de functie Lambda@Edge**

**Navigatie:** de Console van AWS > CloudFront > Verdelingen > [ Uw Distributie ] > Gedrag

1. Klik **uitgeven** op uw gedrag.

2. De rol neer aan de **verenigingen van de Functie** sectie.

3. De koppelingen herstellen:

   | Gebeurtenis | Instellen op |
   |---|---|
   | Viewer-verzoek | `edgeoptimize-routing` (functie CloudFront) |
   | Aanvraag oorsprong | Versioned Lambda ARN van Stap 4 |
   | Oorspronkelijke reactie | Versioned Lambda ARN van Stap 4 |

   Gebruik versioned **ARN van de Functie** u in Stap 4 (in **publiceer een versie**) noteerde.

   ![&#x200B; de associatieconfiguratie van de Functie &#x200B;](/help/assets/optimize-at-edge/cloudfront-function-association.png)

4. Klik **sparen veranderingen**.

5. Wacht tot de distributie klaar is met implementeren, en controleer vervolgens of de hoekige aanvragen de `x-edgeoptimize-request-id` header retourneren zoals beschreven in Stap 6.

{{return-to-overview}}
