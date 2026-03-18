---
title: Log doorsturen - Andere (handmatig uploaden)
description: Leer hoe te om CDN logboeken aan Adobe S3 emmertje voor de inzameling van hoekige verkeersgegevens in LLM Optimizer manueel te uploaden wanneer het gebruiken van een niet gestaafde CDN leverancier.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 0%

---


# Log doorsturen: ander (handmatig uploaden) {#log-forwarding-other}

De **Andere BYOCDN** leveringsmethode is een catch-all optie voor klanten die CDN logboeken aan LLM Optimizer willen verstrekken wanneer:

- **Hand uploadt** heeft de voorkeur - bijvoorbeeld, voeren de operationele teams logboeken uit en uploaden hen periodiek.
- **Ad hoc geautomatiseerde processen** worden gebruikt - eenmalig manuscripten, geplande uitvoer, serverless banen.
- De klant gebruikt a **CDN die niet** door het ingebouwde logboek door:sturen integratie wordt gesteund.

Deze methode imiteert het &quot;ononderbroken door:sturen&quot;model: stammen worden geproduceerd en in de verwachte plaats geupload S3 en uiteindelijk automatisch door de innamepijpleidingen verwerkt.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op [ LLM Optimizer ](https://llmo.now/):

1. Ga naar **Configuratie**.

   ![ knoop van de Configuratie ](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![ CDN het lusje van de Configuratie ](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.

   <!-- ![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![ vormen ](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecteer **Andere**.

   ![ Uitgezochte Andere ](/help/overview/assets/log-forwarding/other/other-select.png)

1. Klik **Onboard**.

<!--   ![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Stap 2: Logboeken voorbereiden en uploaden {#step-2}

### Vereiste logbestandsindeling (JSON Lines) {#log-format}

De logboeken moeten als nieuwe lijn worden geupload afgebakend JSON (**één voorwerp JSON per lijn**). Elke logboeklijn moet de volgende gebieden **precies zoals hieronder gespeld** omvatten.

#### Veld-voor-veld schema {#schema}

| Veld | Type | Beschrijving | Voorbeeld |
|---|---|---|---|
| **timestamp** | String | Tijdstempel van het verzoek na het **formaat ISO 8601**. | `"2025-02-01T23:00:05Z"` |
| **gastheer** | String | Het webdomein dat de client heeft aangevraagd. | `"www.example.com"` |
| **url** | String | De **weg** en de **vraagparameters** worden vereist, terwijl het domein **niet** zou moeten worden omvat. | `"/home?utm_source=google"` |
| **request_method** | String | De HTTP-aanvraagmethode, ook wel HTTP-werkwoorden genoemd. | `"GET"` |
| **request_user_agent** | String | De HTTP Gebruiker-Agent verzoekkopbal. | `"Mozilla/5.0 (compatible; GPTBot/1.0"` |
| **request_referer** | String | De HTTP Referer request header (kan leeg zijn). | `"https://chatgpt.com"` |
| **response_status** | Geheel | De statuscode van het HTTP-antwoord. | `200` |
| **response_content_type** | String | De HTTP Content-Type response header. | `"text/html; charset=utf-8"` |
| **time_to_first_byte** | Geheel | De tijd tussen het creëren van een verbinding aan de server en het downloaden van de inhoud van een Web-pagina in **milliseconden**. Instellen op nul indien onbekend of niet beschikbaar. | `42` |

#### Voorbeelden van logboekregels {#example}

In het volgende voorbeeld worden drie logregels getoond:

```json
{"timestamp":"2025-02-01T23:06:14Z","host":"www.example.com","url":"/products/llm-optimizer?utm_source=google","request_method":"GET","request_user_agent":"Mozilla/5.0 (compatible; GPTBot/1.0; +https://openai.com/gptbot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":198}
{"timestamp":"2025-02-01T23:19:32Z","host":"www.example.com","url":"/services/ai-consulting/overview","request_method":"GET","request_user_agent":"PerplexityBot/1.0 (+https://www.perplexity.ai/perplexitybot)","response_status":200,"request_referer":"","response_content_type":"text/html; charset=utf-8","time_to_first_byte":255}
{"timestamp":"2025-02-01T23:44:05Z","host":"www.example.com","url":"/products/pricing/enterprise?utm_medium=social","request_method":"GET","request_user_agent":"ClaudeBot/1.0 (+https://www.anthropic.com)","response_status":200,"request_referer":"","response_content_type":"application/pdf","time_to_first_byte":312}
```

### Kritische disclaimer (spelling en typen) {#disclaimer}

De opname en samenvoegingspijpleidingen zijn strikt over **gebiedsnamen en gegevenstypes**.

- De namen van het gebied moeten **precies** (geval en spelling) aanpassen.
- Gegevenstypen moeten correct zijn, en wel als volgt:
   - **timestamp** moet een koord met **formaat zijn ISO 8601**. UNIX-achtige tijdstempels werken mogelijk niet.
   - **response_status** moet een geheel zijn.
   - **time_to_first_byte** moet een geheel zijn en milliseconden gebruiken.
   - Tekenreeksen moeten geldige JSON-tekenreeksen zijn.
- Onjuist gevormde JSON- of ontbrekende/onjuiste velden kunnen ertoe leiden dat logbestanden worden overgeslagen of niet worden geparseerd, waardoor gegevens in de rapporten ontbreken.

### Locatie en verwerkingscapaciteit uploaden {#upload-location}

#### Padregel {#path-rule}

Upload logbestanden via het juiste mappad met de notatie: **`yyyy/mm/dd/`** (met schuine strepen).

Een voorbeeldlogboek van 1 februari 2025 UTC: `ABC123AdobeOrg/raw/byocdn-other/2025/02/01/`

#### Verwerkingsregel {#processing-rule}

- Logboeken die tijdens een bepaalde **UTC dag** worden geupload worden verwerkt door de pijpleidingen **dichtbij het eind van die dag UTC** (dagelijkse looppas).
- Logs die in **worden geupload de omslagen van vorige dagen** (backfill) worden **ontdekt en verwerkt** binnen 24 uren.

## Scenarios {#scenarios}

### Scenario 1: Logs in Splunk / Elasticsearch — export en upload naar S3 {#scenario-splunk}

**Doel**: Haal logboeken van bestaande observatieplatforms terug en lever hen aan de S3 plaats.

- Haal de vereiste gebieden uit Splunk/Elastic onderzoeksgebeurtenissen.
- Transformeer elke gebeurtenis naar één JSON-object volgens het bovenstaande schema (JSON-regels).
- Upload het resulterende dossier(s) aan de aangewezen S3 emmer en de **huidige UTC dag** weg: `…/byocdn-other/yyyy/mm/dd/`
- De logbestanden worden automatisch verwerkt aan het einde van de UTC-dag.

### Scenario 2: Lambda / Azure Function — format and upload to S3 {#scenario-serverless}

**Doel**: De serverloze van het gebruik gegevens om CDN- logboeken te halen/te ontvangen, hen te normaliseren, en hen te leveren aan de S3 plaats.

- De functie wint logboeken van de bron van de klant (logboekopslag, rij, blob opslag, enz.) terug.
- De functie brengt gebieden in het verwachte schema in kaart en geeft **lijnen JSON** uit.
- De functie uploadt uitvoer naar: `…/byocdn-other/yyyy/mm/dd/`
- De logbestanden worden automatisch verwerkt aan het einde van de UTC-dag.

## Snelle checklist {#checklist}

- **Één voorwerp JSON per lijn** (Lijnen JSON)
- **Exacte gebiedspelling** zoals gespecificeerd
- Gegevenstypen corrigeren
- **time_to_first_byte** in milliseconden (geheel)
- Upload aan de aangewezen omslag UTC: **yyyy/mm/dd/** onder **bycdn-andere**
