---
title: Log doorsturen - snel
description: Leer hoe te om CDN- logboeken van Fastly aan Adobe S3 emmertje voor de inzameling van verkeersgegevens in LLM Optimizer door:sturen.
feature: Agentic Traffic
source-git-commit: d1f98770b39f550c36d93ece9b89933c0e90f189
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Log doorsturen: snel {#log-forwarding-fastly}

Deze pagina verklaart hoe te om CDN- logboeken van Fastly aan het emmertje van Adobe S3 voor de inzameling van hoekige verkeersgegevens door:sturen. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het aan boord gaan proces volledig is, volg de stappen op deze pagina worden verstrekt om logboek het door:sturen in de Snelle Webconsole te vormen die.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [ https://llmo.now/](https://llmo.now/):

1. Ga naar **Configuratie**.

   ![ knoop van de Configuratie ](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![ CDN het lusje van de Configuratie ](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.
1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![ vormen ](/help/overview/assets/log-forwarding/common/configure.png)
1. Selecteer **snelst (BYOCDN)**.

   ![ Uitgezochte snel ](/help/overview/assets/log-forwarding/fastly/fastly-select.png)
1. Klik **Onboard**.

## Stap 2: Maak snel een S3-eindpunt {#step-2}

Om een S3 eindpunt, op het **Snelle Controlebord** te creëren:

1. In het Fastly dashboard, ga naar **diensten CDN** (niet de diensten van de Berekening).
1. In het **Amazon Web Services S3** gebied, klik **leidt eindpunt** tot.
1. Vul **uit creeer een het eindpunt van Amazon S3** gebieden:

| Veld | Beschrijving |
| --- | --- |
| **Naam** | De mens-leesbare naam voor het eindpunt. |
| **Plaatsing** | Standaard |
| **formaat van het Logboek** | Gebruik het koord van het logboekformaat dat in het **formaatkoord van het Logboek** hieronder wordt getoond. |
| **formaat van de Chronologie** | `%Y-%m-%dT%H:%M:%S.000` |
| **naam van het Emmertje** | Kopieer de **Naam van het Emmertje** van de de configuratiepagina van LLM Optimizer. ![Emmernaam ](/help/overview/assets/log-forwarding/fastly/fastly-bucket-name.png) |
| **Domein** | Kopieer de **Naam van het Domein** van de de configuratiepagina van LLM Optimizer. ![Domeinnaam ](/help/overview/assets/log-forwarding/fastly/fastly-domain-name.png) |
| **methode van de Toegang** | **Referenties van de Gebruiker** |
| **Referenties van de Gebruiker** | Kopieer de **Sleutel van de Toegang** en **Geheime Sleutel** van de de configuratiepagina van LLM Optimizer. ![Toegangstoetsen ](/help/overview/assets/log-forwarding/common/access-keys.png) |
| **Periode** | `300` |

**het formaatkoord van het Logboek:**

```json
{ "timestamp": "%{strftime(\{"%Y-%m-%dT%H:%M:%S%z"\}, time.start)}V", "host": "%{if(req.http.Fastly-Orig-Host, req.http.Fastly-Orig-Host, req.http.Host)}V", "url": "%{json.escape(req.url)}V", "request_method": "%{json.escape(req.method)}V", "request_referer": "%{json.escape(req.http.referer)}V", "request_user_agent": "%{json.escape(req.http.User-Agent)}V", "response_status": %{resp.status}V, "response_content_type": "%{json.escape(resp.http.Content-Type)}V", "client_country_code": "%{client.geo.country_name}V", "time_to_first_byte": "%{time.to_first_byte}V" }
```

>[!WARNING]
>
>De managers van het wachtwoord kunnen het **Geheime Zeer belangrijke** gebied met uw Fastly wachtwoord automatisch vullen. Als de AWS-integratie mislukt, voert u de Secret Key handmatig in.

Nadat u de stappen hierboven voltooit, klik **Geavanceerde opties** en reeks:

| Veld | Beschrijving |
| --- | --- |
| **Weg** | Kopieer **Weg** van de de configuratiepagina van LLM Optimizer. ![Pad ](/help/overview/assets/log-forwarding/fastly/fastly-path.png) |
| **selecteer een formaat van de logboeklijn** | Leeg |
| **Compressie** | Gzip |
| **niveau van de Overtolligheid** | Standaard |
| **ACL** | Geen |
| **de zijencryptie van de Server** | Geen |
| **Maximale bytes** | 0 |

Nadat u de geavanceerde opties hebt ingesteld:

1. Klik **creëren** om het eindpunt tot stand te brengen.
1. Van **activeer** menu, uitgezochte **activeert op Productie** om op te stellen.

>[!NOTE]
>
>Met de snelste streams worden continu logbestanden gemaakt naar S3, maakt de S3-website en API alleen bestanden beschikbaar nadat het uploaden is voltooid.

### Voorbeeld van logbestandvermelding {#example}

Hieronder ziet u een voorbeeld van een indelingstekenreeks voor het verzenden van gegevens naar Amazon S3:

```json
{
  "timestamp": "2026-02-10T05:05:36+0000",
  "host": "example.com",
  "url": "/my/path",
  "request_method": "GET",
  "request_referer": "https://example.com/my/other/path",
  "request_user_agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 13_2_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.0.3 Mobile/15E148 Safari/604.1",
  "response_status": 200,
  "response_content_type": "text/css; charset=utf-8",
  "client_country_code": "argentina",
  "time_to_first_byte": "0.138"
}
```
