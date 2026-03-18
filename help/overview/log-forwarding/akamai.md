---
title: Log doorsturen - Akamai
description: Leer hoe te om CDN- logboeken van Akamai aan Adobe S3 emmertje voor de inzameling van verkeersgegevens in LLM Optimizer door:sturen.
feature: Agentic Traffic
source-git-commit: b590cd14ba7d64e56a6c972fd6090e2df9de58f6
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# Log doorsturen: Akamai {#log-forwarding-akamai}

Deze pagina verklaart hoe te om CDN- logboeken van Akamai aan het emmertje van S3 van Adobe voor de inzameling van agentic verkeersgegevens door:sturen. U gebruikt de LLM Optimizer CDN-configuratiepagina voor toegang tot LLM Optimizer. Nadat het instapproces is voltooid, volgt u de stappen op deze pagina om het doorsturen van logbestanden in het Configuratiescherm van Akamai te configureren.

## Stap 1: Aan boord in LLM Optimizer {#step-1}

Op de pagina van LLM Optimizer [&#x200B; https://llmo.now/](https://llmo.now/):

1. Ga naar het **dashboard van de Configuratie van de Klant**.

   ![&#x200B; knoop van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/config-button.png)

1. Klik de **CDN Configuratie** tabel.

   ![&#x200B; CDN het lusje van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/common/cdn-config-tab.png)

1. Klik **krijgen Begonnen**.

   <!--![Onboard CDN button](/help/overview/assets/log-forwarding/common/onboard-cdn-button.png)-->

1. Naast **activeer AI de Inzichten van het Verkeer**, klik **vormen**.

   ![&#x200B; vormen &#x200B;](/help/overview/assets/log-forwarding/common/configure.png)

1. Selecteer **Akamai (BYOCDN)**.

   ![&#x200B; Uitgezochte Akamai &#x200B;](/help/overview/assets/log-forwarding/akamai/akamai-select.png)

1. Klik **Onboard**.

   <!--![Onboard button](/help/overview/assets/log-forwarding/common/onboard-button.png)-->

## Stap 2: Een stream maken in Akamai {#step-2}

Op het Akamai controlepaneel [&#x200B; https://control.akamai.com/ &#x200B;](https://control.akamai.com/) volgt de stappen van de officiële documentatie Akamai aan [&#x200B; een stroom &#x200B;](https://techdocs.akamai.com/datastream2/docs/create-stream) creëren.

## Stap 3: gegevensparameters kiezen {#step-3}

Na het creëren van de stroom, op het Akamai controlepaneel, klik naast verdergaan **Reeksen van Gegevens** tabel. Volg de stappen van de officiële documentatie Akamai om de [&#x200B; gegevensparameters &#x200B;](https://techdocs.akamai.com/datastream2/docs/choose-data-parameters) te kiezen. De volgende velden uit de LLM Optimizer-configuratie zijn vereist:

![&#x200B; LLMO configuratiegebieden &#x200B;](/help/overview/assets/log-forwarding/akamai/akamai-llmo-config-fields.png)

De toewijzing moet als volgt zijn:

* **de Informatie van het Logboek**
reqTimeSec -> Aanvraagtijd
* **Geo Gegevens**
land -> Land/regio
* **de uitwisselingsgegevens van het Bericht**
reqHost -> Aanvraaghost
reqPath -> Aanvraagpad
queryStr -> Query-tekenreeks
reqMethod -> Request, methode
ua -> Gebruikersagent
statusCode -> HTTP-statuscode
rspContentType -> Response Content-Type
* **de kopbalgegevens van het Verzoek**
referentie -> Referer
* **de prestatiesgegevens van het Netwerk**
timeToFirstByte -> Tijd tot eerste byte

De velden voor de Akamai-gegevensset (inclusief id&#39;s) zijn als volgt:

110, # reqTimeSec -> Aanvraagtijd
2012, # country -> Country/Region
1011, # reqHost -> Aanvraaghost
1013, # reqPath -> Aanvraagpad
2009, # queryStr -> Query-tekenreeks
1012, # reqMethod -> Aanvraagmethode
1017, # ua -> User-Agent
1008, # statusCode -> HTTP-statuscode
1032, # reference -> Referer
1016, # rspContentType -> Response Content-Type
2025 # timeToFirstByte -> Tijd naar eerste byte

## Stap 4: Vorm bestemming {#step-4}

Na het creëren van de gegevensstromen en het kiezen van de parameters moet u de bestemming vormen. Voer de volgende stappen uit om de bestemming te configureren:

1. In **Bestemming**, uitgezochte **S3**.
2. In **Naam**, ga een human-readable beschrijving voor de bestemming in.
3. In **Emmertje**, kopieer de **Naam van het Emmertje** van de de configuratiepagina van LLM Optimizer.

   ![&#x200B; Naam van het Emmertje &#x200B;](/help/overview/assets/log-forwarding/common/bucket-name.png)

4. In **weg van de Omslag**, kopieer het **Weg** van de de configuratiepagina van LLM Optimizer.

   ![&#x200B; configuratie van de Weg &#x200B;](/help/overview/assets/log-forwarding/akamai/akamai-path-config.png)

5. In **Gebied**, kopieer het **Gebied** van de de configuratiepagina van LLM Optimizer.

   <!--![Region](/help/overview/assets/log-forwarding/common/region.png)-->

6. In **zeer belangrijke identiteitskaart van de Toegang** en **Geheime toegangssleutel**, kopieer beide waarden van de de configuratiepagina van LLM Optimizer.

   ![&#x200B; sleutels van de Toegang &#x200B;](/help/overview/assets/log-forwarding/common/access-keys.png)

7. Klik **bevestigen &amp; sparen** om de verbinding aan de bestemming te bevestigen, en sparen de details u verstrekte. Als onderdeel van dit validatieproces gebruikt het systeem de opgegeven toegangssleutel-id en geheime toegangssleutel om een verificatiebestand in uw S3-map te maken met een tijdstempel in de bestandsnaam in de `Akamai_access_verification_[TimeStamp].txt` -indeling. Dit bestand wordt alleen weergegeven als het validatieproces is geslaagd en u toegang hebt tot het Amazon S3-emmertje en de map waarnaar u de logbestanden wilt verzenden.

8. In het **menu van de Opties van de Levering**, geef het **Filename** gebied als volgt uit:

   a. Verander de **prefix**. Kopieer de waarde van de de configuratiepagina van LLM Optimizer onder **het dossierprefix van het Logboek**:

   ```
   {%Y}-{%m}-{%d}T{%H}:{%M}:{%S}.000
   ```

   b. Verander het **achtervoegsel**. Kopieer de waarde van de de configuratiepagina van LLM Optimizer onder **het dossierachtervoegsel van het Logboek**.

9. Verander de **Pushfrequentie**. Kopieer de waarde van de de configuratiepagina van LLM Optimizer onder **Interval van het Logboek**.

   ![&#x200B; interval van het Logboek &#x200B;](/help/overview/assets/log-forwarding/akamai/akamai-log-interval.png)

10. Klik **daarna** om het proces te voltooien.

Vóór definitieve bevestiging, zou de configuratie aan dit voorbeeld gelijkaardig moeten kijken:

![&#x200B; Bevestiging van de Configuratie &#x200B;](/help/overview/assets/log-forwarding/akamai/akamai-validation.png)
