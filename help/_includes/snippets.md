---
source-git-commit: beae935e7a34f5bccbe21578fa9a928912958710
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---
# Fragmenten

## Verifieer de opstelling - Adobe Beheerde CDN {#verify-setup-adobe-aem-cs-cdn}

**verifieer de opstelling**

Na de voltooiing van de opstelling, verifieer dat beide verkeer aan Edge Optimize wordt verpletterd en dat het menselijke verkeer onaangetast blijft.

**1. Het verkeer van de Bot van de test (zou moeten worden geoptimaliseerd)**

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

![&#x200B; AI Verkeer die status met toegelaten verpletteren verplettert &#x200B;](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

## Setup controleren - BYOCDN {#verify-setup-byocdn}

**verifieer de opstelling**

Na de voltooiing van de opstelling, verifieer dat beide verkeer aan Edge Optimize wordt verpletterd en dat het menselijke verkeer onaangetast blijft.

**1. Het verkeer van de Bot van de test (zou moeten worden geoptimaliseerd)**

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

## Ophaalstappen voor API-sleutel {#retrieve-byocdn-api-key}

**Stappen om uw API sleutel terug te winnen:**

1. Navigeer aan **Configuratie van de Klant** en selecteer de **CDN Configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Onder **AI Verkeer dat verplettert om Optimalisaties** op te stellen, tik **optimalisaties aan AI Agenten** checkbox opstelt.

   ![&#x200B; Tik stel Optimalisaties aan AI Agenten &#x200B;](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png) op

3. Kopieer de API sleutel en ga met de verpletterende configuratiestappen hieronder te werk.

   ![&#x200B; Kopieer de API sleutel &#x200B;](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >In dit stadium, kan de status een rood kruis tonen die erop wijst dat de opstelling nog niet voltooid is. Dit wordt verwacht — zodra u de verpletterende configuratie hieronder voltooit en AI bot het verkeer begint te stromen, zal de status aan een groen controleteken bijwerken bevestigend dat het verpletteren met succes wordt toegelaten.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

## Terug naar overzicht {#return-to-overview}

Meer leren over Optimaliseren bij Edge, met inbegrip van beschikbare kansen, auto-optimaliseringswerkschema&#39;s, en FAQs, terugkeer aan [&#x200B; optimaliseren bij het overzicht van Edge &#x200B;](/help/dashboards/optimize-at-edge.md).
