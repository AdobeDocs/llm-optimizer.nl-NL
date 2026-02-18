---
title: Optimaliseren bij Edge - Akamai (BYOCDN)
description: Leer hoe u Akamai BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '302'
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

![&#x200B; Failover van de Plaats &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover.png)

![&#x200B; Gedrag Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-behaviors.png)

![&#x200B; Regels Failover &#x200B;](/help/assets/optimize-at-edge/akamai-step9-failover-rules.png)

Site-failover zorgt ervoor dat als bij Edge Optimize een `4XX` - of `5XX` -fout wordt geretourneerd, de aanvraag automatisch wordt teruggestuurd naar de standaardoorsprong, zodat de eindgebruiker nog steeds een antwoord ontvangt.

| Scenario | Gedrag |
| --- | --- |
| Edge Optimize geeft als resultaat `2XX` | De geoptimaliseerde reactie wordt aan de cliënt gediend. |
| Edge Optimize geeft `4XX` of `5XX` | Het verzoek wordt verpletterd terug naar de standaardoorsprong. |

{{verify-setup-byocdn}}

{{return-to-overview}}
