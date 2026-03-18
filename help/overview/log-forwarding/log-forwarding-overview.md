---
title: BYOCDN-overzicht van het doorsturen van logbestanden
description: Leer hoe te om CDN- logboeken van uw leverancier aan Adobe S3 emmertje voor de inzameling van verkeersgegevens in LLM Optimizer door:sturen.
feature: Agentic Traffic
source-git-commit: a1ba7684ccef9baf3452cc158fc0d6a12aa7adb8
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---


# BYOCDN-overzicht van het doorsturen van logbestanden {#cdn-log-forwarding}

Het door:sturen van het logboek voor een klant beheerde CDN (BYOCDN) is het proces om uw CDN toegangslogboeken naar het emmertje van Adobe te verzenden Amazon S3 zodat LLM Optimizer agentic verkeersgegevens kan verzamelen en analyseren. Zonder het logboek CDN door:sturen, kan het [&#128279;](/help/dashboards/agentic-traffic.md) dashboard van het Verkeer 0&rbrace; Agentic geen metriek tonen.

Voor de onderstaande handleidingen gelden dezelfde twee fasen:

1. **Onboard in LLM Optimizer** — registreer uw CDN op de [&#x200B; CDN- Configuratie &#x200B;](/help/dashboards/customer-configuration.md) pagina om de benodigde S3 geloofsbrieven en wegdetails te produceren.
2. **vorm uw CDN** — gebruik die details om een logboek-door:sturen baan (of upload manueel logboeken) in de console van uw CDN leverancier tot stand te brengen.

## CDN-providers {#cdn-providers}

Volg de overeenkomstige gids voor u CDN leverancier.

| CDN-provider | Hulplijn |
|---|---|
| Akamai | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/akamai.md) |
| Cloudflare | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/cloudflare.md) |
| CloudFront | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/cloudfront.md) |
| Snel | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/fastly.md) |
| Imperva | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/imperva.md) |
| Overige (handmatige/niet-ondersteunde CDN) | [&#x200B; gids van de Mening &#x200B;](/help/overview/log-forwarding/other.md) |

>[!NOTE]
>
>Als uw leverancier CDN hierboven niet vermeld is, gebruik **Andere (hand/niet gestaafde CDN)** gids die handmatige uploads, ad-hoc manuscripten en om het even welke CDN behandelt die niet nationaal gesteund wordt.
