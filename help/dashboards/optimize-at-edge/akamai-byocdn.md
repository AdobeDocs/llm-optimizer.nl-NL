---
title: Optimaliseren bij Edge - Akamai (BYOCDN)
description: Leer hoe u Akamai BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 9230e525340bb951fcd9f2ae1f88bad557d5b7d7
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---


# Akamai (BYOCDN)

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de regels voor Akamai Property Manager instelt, moet u controleren of u:

* Toegang tot Akamai Property Manager voor uw domein.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

{{retrieve-byocdn-api-key}}

**Configuratie**

De volgende regel van de Manager van het Bezit van Akamai leidt gebruikersagenten LLM aan Edge Optimize. De configuratie bevat de volgende stappen:

**1. Plaats verpletterend criteria (gebruiker-Agent aanpassing)**

Plaats het verpletteren voor volgende gebruiker-agenten :image.png

```
 *AdobeEdgeOptimize-AI*,
 *ChatGPT-User*,
 *GPTBot*,
 *OAI-SearchBot*,
 *PerplexityBot*,
 *Perplexity-User*
```

![&#x200B; plaats verpletterend criteria &#x200B;](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Oorsprong en SSL-gedrag instellen**

Oorsprong instellen als `live.edgeoptimize.net` en SAN afstemmen op `*.edgeoptimize.net`

![&#x200B; Vastgestelde Oorsprong en SSL gedrag &#x200B;](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Cachetoets instellen**

De toetsvariabele voor de cache `PMUSER_EDGE_OPTIMIZE_CACHE_KEY` instellen op `LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}`

![&#x200B; vastgestelde Zeer belangrijke Variabele van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Caching Rules**

![&#x200B; Caching Regels &#x200B;](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Binnenkomende aanvraagheaders wijzigen**

Stel de volgende binnenkomende aanvraagheaders in:
`x-edgeoptimize-api-key` naar de API-sleutel die is opgehaald uit LLMO
`x-edgeoptimize-config` to `LLMCLIENT=TRUE;`
`x-edgeoptimize-url` t/m `{{builtin.AK_URL}}`

![&#x200B; wijzigt Binnenkomende Kopballen van het Verzoek &#x200B;](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Binnenkomende antwoordheaders wijzigen**

![&#x200B; wijzigt Inkomende Kopballen van de Reactie &#x200B;](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Wijziging van cache-id**

![&#x200B; Verandering van identiteitskaart van het Geheime voorgeheugen &#x200B;](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Uitgaande verzoekkopballen wijzigen**

`x-forwarded-host` header instellen op `{{builtin.AK_HOST}}`

![&#x200B; wijzigt Uitgaande Kopballen van het Verzoek &#x200B;](/help/assets/optimize-at-edge/akamai-step8-outgoing-request.png)

**9. Site-failover**

De configuratie van Failover van de Plaats heeft twee delen: het failovergedrag (binnen belangrijkste wordt gevormd optimize-bij-rand die regel verplettert) en een afzonderlijke de kopbalregel van de failovertest die.

**9a. Het Gedrag van Failover van de plaats (binnen belangrijkste optimize-bij-rand die regel verplettert)**

Binnen de belangrijkste verpletterende regel, vorm het gedrag van Failover van de Plaats en het Geavanceerde fragment van XML als volgt:

![&#x200B; Failover van de Plaats &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover.png)

Voeg de aanvraagkoptekst `x-edgeoptimize-request` toe met de waarde `fo` via Geavanceerde XML:

```
<forward:availability.fail-action2>
<add-header>
<status>on</status>
<name>x-edgeoptimize-request</name>
<value>fo</value>
</add-header>
</forward:availability.fail-action2>
```

![&#x200B; Gedrag Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

**9b. De regel van de Kopbal van de Test van Failover (sibling regel)**

>[!IMPORTANT]
>
>Creeer **EdgeOptimize Failover - de regel van de Kopbal van de Test** als a **sibling** (op het zelfde niveau) van de verpletterende regels - **niet** genestelde binnen hen. In de de regelboom van de Manager van het Bezit Akamai, zou de hiërarchie als moeten kijken:
>
>```
>▼ Parent Rule
>   ▶ Optimize at Edge Routing     ← routing rule
>       EdgeOptimize Failover - Test Header       ← sibling, same level
>```
>
>Dit verzekert de de kopbalregel van de failovertest voor **allen** verpletterend regels, niet enkel.

Als de aanvraagheader `x-edgeoptimize-request` -waarde `fo` is, stelt u de uitgaande antwoordheader `x-edgeoptimize-fo` in op `true` .

![&#x200B; Regels Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

Site-failover zorgt ervoor dat als bij Edge Optimize een `4XX` - of `5XX` -fout wordt geretourneerd, de aanvraag automatisch wordt teruggestuurd naar de standaardoorsprong, zodat de eindgebruiker nog steeds een antwoord ontvangt.

| Scenario | Gedrag |
| --- | --- |
| Edge Optimize geeft als resultaat `2XX` | De geoptimaliseerde reactie wordt aan de cliënt gediend. |
| Edge Optimize geeft `4XX` of `5XX` | Het verzoek wordt verpletterd terug naar de standaardoorsprong. |

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

{{return-to-overview}}
