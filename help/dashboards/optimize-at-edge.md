---
title: Optimaliseren bij Edge
description: Leer hoe u optimalisaties in LLM Optimizer kunt leveren aan de CDN-rand zonder dat er ontwerpwijzigingen nodig zijn.
feature: Opportunities
source-git-commit: 3c6f287b3c3787cee95f99b7031412f26692a88b
workflow-type: tm+mt
source-wordcount: '2291'
ht-degree: 0%

---


# Optimaliseren bij Edge

Deze afdeling ...

## Wat is Optimize in Edge?

Optimaliseren in Edge is een op randen gebaseerde implementatiefunctie in LLM Optimizer die kan dienen voor AI-vriendelijke wijzigingen in LLM-gebruikersagents. Omdat het optimalisaties bij de CDN rand levert, zijn geen auteursveranderingen in het Systeem van het Beheer van de Inhoud (CMS) vereist. Het is ook alleen gericht op het agentische verkeer en heeft geen invloed op menselijke gebruikers of SEO-bots.

Wanneer LLM Optimizer mogelijkheden detecteert om een pagina te optimaliseren, kunnen gebruikers correcties direct aan de rand implementeren zonder dat er wijzigingen in het platform nodig zijn.

Dit vermogen is momenteel in Vroege Toegang.

## Waarom zou een klant geinteresseerd moeten zijn?

Optimaliseren in Edge is een sneller en leener alternatief voor traditionele oplossingen die complexe technische inspanningen vereisen. Wanneer klanten een eenmalige installatie hebben voltooid, hoeven er geen platformwijzigingen of lange ontwikkelingscycli te worden uitgevoerd om de wijzigingen op de webpagina&#39;s toe te passen. De gebruiker kan verbeteringen in minuten publiceren, niet in weken, zonder dat de betrokkenheid van de ontwikkelaar vereist is. Dit is een manier met weinig risico en geen code om uw website te optimaliseren voor AI-agents.

### Belangrijkste voordelen en waardevoorstel

* **AI-slechts levering:** serveert geoptimaliseerde HTML aan AI agenten slechts zonder invloed op menselijke bezoekers of SEO bots.
* **Snellere cycli:** publiceer veranderingen in notulen, niet weken. Er zijn geen platformwijzigingen of lange technische cycli vereist.
* **Laag-risico en omkeerbaar:** gesteund met een één-klik het terugschroeven van prijzen vermogen dat de pagina in notulen kan terugkeren.
* **geen prestatieseffect:** op Edge-Gebaseerde optimalisaties en caching houden plaatslatentie onaangetast.
* **CDN en CMS-agnostic:** werkt met om het even welke configuratie CDN en front-end opstelling ongeacht CMS.

## Wie moet het gebruiken?

Optimaliseren in Edge is ontworpen voor zakelijke gebruikers in marketing-, SEO-, content- en digitale strategische teams. Zo kunnen zakelijke gebruikers de volledige reis in LLM Optimizer voltooien: mogelijkheden identificeren, suggesties begrijpen en de oplossingen eenvoudig implementeren. Met Optimaliseren in Edge kunnen gebruikers de wijzigingen vooraf bekijken, deze snel implementeren en controleren of de optimalisaties live zijn. Prestaties kunnen worden bijgehouden in het ecosysteem van LLM Optimizer.

## Welke mogelijkheden zijn er in Edge geoptimaliseerd?

De kansen die de agentische Webervaring kunnen verbeteren worden gesteund met Optimize in Edge. Leer meer over elke kans in [&#x200B; sectie van Kansen &#x200B;](/help/dashboards/opportunities.md).

## Onboarding

U kunt Optimize bij Edge toelaten nadat u aan LLM Optimizer hebt ingezien en uw CDN- logboeken door:sturen.

Een ingenieur CDN wordt vereist om de aanvankelijke opstelling te voltooien om Optimize bij Edge toe te laten.

Vereisten voor installatie:

* Een API-sleutel genereren.
* Voeg Optimize bij Edge toe die regels in CDN verplettert.
* Door de gebruiker gedefinieerde paden of het hele domein Lijsten van gewenste personen.
* Voeg een user-defined lijst van gebruikersagenten LLM aan doel toe.
* Zorg ervoor dat robots.txt geen gebruikersagents blokkeert die zijn bedoeld als doel.
* Bevestig optimaliseren bij het verpletteren van Edge is in de UI van LLM Optimizer.

Adobe verstrekt de fragmenten van de steekproefconfiguratie voor de meeste belangrijkste CDNs om het opstellingsproces te begeleiden. De voorbeelden van fragmenten die in onze richtsnoeren zijn opgenomen, moeten worden aangepast aan de werkelijke live-configuratie. Adobe raadt u aan eerst wijzigingen in de lagere omgevingen te implementeren.

>[!BEGINTABS]

>[!TAB  de Dienst van de Wolk AEM beheerde CDN (snelst) ]

**Tokowaka BYOCDN - Adobe Beheerde CDN**

Gebruikt alleen originSelectors om de oorsprong Tokowaka te selecteren.

In het volgende voorbeeld worden LLM-agents aangevraagd voor een specifiek domein dat overeenkomt met het patroon &quot;/es/*&quot; of exacte paden (alleen HTML-pagina&#39;s worden gerouteerd). Het voorbeeld wordt verondersteld om een uitgangspunt te verstrekken en voor het geval u veelvoudige originSelectors in uw config hebt wordt het geadviseerd om dit eerst te plaatsen.

Belangrijke opmerkingen:

* x-tokowaka-verzoek moet worden gecontroleerd alvorens aan de achtergrond van Tokowaka te verpletteren. Alleen aanvragen die deze header niet hebben, moeten naar de achtergrond van Tokowaka worden geleid.
* de originSelector regel dat de routes aan de achtergrond van Tokowaka eerst in de lijst zouden moeten zijn als er veelvoudige regels zijn.
* Het TOKOWAKA_API_KEY-geheim moet worden geïmplementeerd voordat cdn.yaml kan worden geïmplementeerd

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Tokowaka backend
  originSelectors:
    rules:
      - name: route-to-tokowaka-backend
        when:
          allOf:
            - reqHeader: x-tokowaka-request
              exists: false # avoid loops when requests comes from Tokowaka
            - reqHeader: user-agent
              matches: "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: tokowaka-backend
          headers:
            x-tokowaka-api-key: "${{TOKOWAKA_API_KEY}}"
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"
```

>[!TAB  Akamai (BYOCDN) ]

**Tokowaka BYOCDN - Akamai**

```
{
    "name": "Project Tokowaka CDN Rule",
    "children": [
        {
            "name": "Connection settings",
            "children": [],
            "behaviors": [
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.health-detect.status>off</forward:availability.health-detect.status>\n<forward:availability>\n<max-reforwards>1</max-reforwards>\n<max-reconnects>1</max-reconnects>\n</forward:availability>\n<match:forward.server-type value=\"CUSTOMER_ORIGIN\">\n<network:http.read>%(PMUSER_HTTP_READ)</network:http.read>\n<network:http.first-byte-timeout>%(PMUSER_FIRST_BYTE_TIMEOUT)</network:http.first-byte-timeout>\n<network:http.connect-timeout>%(PMUSER_HTTP_CONNECT_TIMEOUT)</network:http.connect-timeout> \n</match:forward.server-type>"
                    },
                    "uuid": "4a8c027b-1b23-44a7-8e12-f8d07e453679",
                    "templateUuid": "41c77091-419f-43f2-9a84-0b406b050cc8"
                }
            ],
            "uuid": "4759571b-8036-4c16-9b60-d3aeb84958f1",
            "criteria": [],
            "criteriaMustSatisfy": "all"
        },
        {
            "name": "Site Failover Behavior",
            "children": [],
            "behaviors": [
                {
                    "name": "failAction",
                    "options": {
                        "actionType": "RECREATED_CO",
                        "contentCustomPath": false,
                        "contentHostname": "www.adobe.com",
                        "enabled": true
                    }
                },
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.fail-action2>\n<add-header>\n<status>on</status>\n<name>x-tokowaka-request</name>\n<value>fo</value>\n</add-header>\n</forward:availability.fail-action2>"
                    }
                }
            ],
            "uuid": "b3000c12-1ab8-49b1-a5d0-75e58bb18c9c",
            "criteria": [
                {
                    "name": "matchResponseCode",
                    "options": {
                        "lowerBound": 400,
                        "matchOperator": "IS_BETWEEN",
                        "upperBound": 599
                    }
                },
                {
                    "name": "originTimeout",
                    "options": {
                        "matchOperator": "ORIGIN_TIMED_OUT"
                    }
                }
            ],
            "criteriaMustSatisfy": "any",
            "comments": "If Tokowaka origin returns a 4xx or 5xx error (or times out), failover condition is to send the request back to Akamai and set the x-tokowaka-request header so we don't re-send the request to Tokowaka"
        }
    ],
    "behaviors": [
        {
            "name": "origin",
            "options": {
                "cacheKeyHostname": "ORIGIN_HOSTNAME",
                "compress": true,
                "customValidCnValues": [
                    "{{Origin Hostname}}",
                    "{{Forward Host Header}}",
                    "*.tokowaka.now"
                ],
                "enableTrueClientIp": true,
                "forwardHostHeader": "ORIGIN_HOSTNAME",
                "hostname": "edge.tokowaka.now",
                "httpPort": 80,
                "httpsPort": 443,
                "ipVersion": "IPV4",
                "minTlsVersion": "DYNAMIC",
                "originCertificate": "",
                "originCertsToHonor": "STANDARD_CERTIFICATE_AUTHORITIES",
                "originSni": true,
                "originType": "CUSTOMER",
                "ports": "",
                "standardCertificateAuthorities": [
                    "akamai-permissive",
                    "THIRD_PARTY_AMAZON"
                ],
                "tlsVersionTitle": "",
                "trueClientIpClientSetting": true,
                "trueClientIpHeader": "True-Client-IP",
                "verificationMode": "CUSTOM"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_LLMCLIENT",
                "variableValue": "TRUE"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "caseSensitive": false,
                "extractLocation": "CLIENT_REQUEST_HEADER",
                "globalSubstitution": false,
                "headerName": "Accept-Language ",
                "regex": "^([a-zA-Z]{2}).*",
                "replacement": "$1",
                "transform": "SUBSTITUTE",
                "valueSource": "EXTRACT",
                "variableName": "PMUSER_LANG"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_X_FORWARDED_HOST",
                "variableValue": "{{builtin.AK_HOST}}"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY",
                "variableValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}};X_FORWARDED_HOST={{user.PMUSER_X_FORWARDED_HOST}}"
            }
        },
        {
            "name": "caching",
            "options": {
                "behavior": "CACHE_CONTROL_AND_EXPIRES",
                "cacheControlDirectives": "",
                "defaultTtl": "1d",
                "enhancedRfcSupport": false,
                "honorMustRevalidate": false,
                "honorPrivate": false,
                "mustRevalidate": false
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-tokowaka-api-key",
                "newHeaderValue": "<your api-key here>",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-config",
                "newHeaderValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-tokowaka-url",
                "newHeaderValue": "{{builtin.AK_URL}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "cacheId",
            "options": {
                "rule": "INCLUDE_VARIABLE",
                "variableName": "PMUSER_TOKOWAKA_CACHE_KEY"
            }
        },
        {
            "name": "modifyIncomingResponseHeader",
            "options": {
                "action": "DELETE",
                "customHeaderName": "Age",
                "standardDeleteHeaderName": "OTHER"
            }
        },
        {
            "name": "prefreshCache",
            "options": {
                "enabled": true,
                "prefreshval": 90
            }
        },
        {
            "name": "modifyOutgoingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-Forwarded-Host",
                "newHeaderValue": "{{builtin.AK_HOST}}",
                "standardModifyHeaderName": "OTHER"
            }
        }
    ],
    "criteria": [
        {
            "name": "userAgent",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "IS_ONE_OF",
                "matchWildcard": true,
                "values": [
                    "*Tokowaka-AI*",
                    "*ChatGPT-User*",
                    "*GPTBot*",
                    "*OAI-SearchBot*"
                ]
            }
        },
        {
            "name": "path",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "MATCHES_ONE_OF",
                "normalize": false,
                "values": [
                ]
            }
        },
        {
            "name": "requestHeader",
            "options": {
                "headerName": "x-tokowaka-request",
                "matchOperator": "DOES_NOT_EXIST",
                "matchWildcardName": false
            }
        },
        {
            "name": "matchVariable",
            "options": {
                "matchCaseSensitive": true,
                "matchOperator": "IS",
                "matchWildcard": false,
                "variableExpression": "FALSE",
                "variableName": "PMUSER_TOKOWAKA_DISABLE"
            }
        }
    ],
    "criteriaMustSatisfy": "all"
}
```

Belangrijke overwegingen:

* De Regel van Tokowaka zal op gebruiker-Agent + Weg + x-tokowaka-verzoek (als niet aanwezig) + variabele TOKOWAKA_DISABLE (om uit het gebruiken van één enkele veranderlijke knevel toe te staan) worden gebaseerd
* De regels van de opstelling aan **wijzigen Inkomende Kopballen van het Verzoek** regel om douanekopballen te plaatsen
* Cachesleutel in Akamai plaatsen gebruikend user-defined variabele door cache-ID wijzigingsmechanisme. Er is slechts één door de gebruiker gedefinieerde variabele toegestaan, dus maak een aparte variabele voor cache_key en stel deze dienovereenkomstig in.
* Lang: gehaald uit de kopbal van de Accepteren-Taal gebruikend &quot;regex&quot;: &quot;^ ([ a-zA-Z ] \ {2 \}).*&quot;
* Met de Wijziging van het Geheime voorgeheugen identiteitskaart binnen een gelijke op Gebruikersagent, kan de inhoud niet door URL (enkel FYI) worden gezuiverd
* Het mechanisme van de failover van de plaats: Met de gelijke op gebruiker-Agent regel, staat Akamai niet aan failover toe die op gezondheidscontrole wordt gebaseerd, maar slechts basis van oorsprongreactie/connectiviteit per verzoek. Plaats **x-tokowaka-fo:true** resp- kopbal in het geval van failoverreactie.
* SWR wordt niet ondersteund door Akamai. Alleen op TTL gebaseerde caching is er. Zo, vorm een regel in Akamai om de kopbal van de Leeftijd van oorsprongreactie te ontdoen anders zou op TTL gebaseerd caching niet werken.
* Zorg ervoor dat de Tokowaka-regel de onderste regel in de regelhiërarchie is (zodat deze alle andere regels overschrijft).

>[!TAB  Fastly (BYOCDN) ]

**Tokowaka BYOCDN - snel - VCL**

![&#x200B; VCL van de Fastly &#x200B;](/help/assets/optimize-at-edge/fastly-vcl.png)

![&#x200B; voeg VCL fragmenten &#x200B;](/help/assets/optimize-at-edge/add-vcl-snippets.png) toe

**vcl_recv fragment**

```
unset req.http.x-tokowaka-url;
unset req.http.x-tokowaka-config;
unset req.http.x-tokowaka-api-key;

if (!req.http.x-tokowaka-request
    && req.http.user-agent ~ "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-tokowaka-url = req.url; # required for identifying the original url
  set req.http.x-tokowaka-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-tokowaka-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_Tokowaka;
}
```

**vcl_hash fragment**

```
if (req.http.x-tokowaka-config) {
  set req.hash += "tokowaka";
  set req.hash += req.http.x-tokowaka-config;
}
```

**vcl_delivery fragment**

```
if (req.http.x-tokowaka-config && resp.status >= 400) {
  set req.http.x-tokowaka-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-tokowaka-config && req.http.x-tokowaka-request == "failover") {
  set resp.http.x-tokowaka-fo = "1";
}
```

>[!ENDTABS]


Voor andere CDN-providers kunt u contact opnemen met llmo-at-edge@adobe.com om uw IT/CDN-teams te helpen bij het instappen.

<!--This should probably be included Opportunities dashboard content. Content also needs serious editing - lots of "customer needs"and business user" etc.-->

Nadat de configuraties zijn voltooid, kunnen zakelijke gebruikers suggesties voor Optimaliseren bij Edge-mogelijkheden in LLM Optimizer implementeren.

## Kansen

| Opportunity | Type | Automatisch identificeren | Automatisch voorstellen | Automatisch optimaliseren |
|---------|----------|----------|----------|----------|
| Zichtbaarheid van inhoud herstellen | Technische GEO | Detecteert pagina&#39;s waarop kritieke inhoud van AI-agents wordt verborgen. Hiermee worden beïnvloede URL&#39;s en verwachte inhoud weergegeven die kunnen worden hersteld. | Hiermee wordt de inhoud gemarkeerd die beschikbaar kan worden gemaakt voor AI-agents en wordt aangeraden om pre-rendering voor deze pagina&#39;s in te schakelen. | Serveert een volledig teruggegeven, AI-vriendschappelijke momentopname van HTML aan zinloos verkeer dat de eerder verborgen inhoud terugkrijgt. |
| Koppen voor AI optimaliseren | Inhoud optimaliseren | Hiermee scant u koppen om lege, dubbele, ontbrekende of dubbelzinnige koppen te detecteren die de leesbaarheid van de machine kunnen verminderen. | Stelt een duidelijkere koptekshiërarchie en verbeterde labels voor en toont een voorvertoning van de bijgewerkte structuur voor elke pagina. | Hiermee wordt de verbeterde kopstructuur voor AI-agents geïnjecteerd, zodat uw visuele ontwerp behouden blijft en de pagina begrijpelijker wordt voor LLM&#39;s. |
| AI-vriendelijke samenvattingen toevoegen | Inhoud optimaliseren | Hiermee worden lange of complexe pagina&#39;s aangegeven waarvoor geen beknopte overzichten op pagina- of sectieniveau beschikbaar zijn, waardoor het voor AI moeilijker wordt om snel te scannen en te begrijpen. | Hiermee raadt u korte, door AI gegenereerde overzichten op paginaniveau en sectieniveau aan om toetsinhoud vast te leggen. | Hiermee voegt u de samenvattingen in de desbetreffende HTML-secties in, waardoor modellen de pagina-inhoud beter kunnen interpreteren en beschrijven. |
| Relevante veelgestelde vragen toevoegen | Inhoud optimaliseren | Hiermee worden gaten in de intentie in de bestaande pagina-inhoud gedetecteerd die baat kunnen hebben bij veelgestelde vragen. | Stelt door AI gegenereerde veelgestelde vragen-inhoud voor die is uitgelijnd op gebruikersinzichten en bestaande onderwerpen. | Hiermee wordt veelgestelde vragen-inhoud in de HTML geïnjecteerd, waardoor pagina&#39;s beter te ontdekken en relevanter worden in door AI gestuurde antwoorden. |
| Complexe inhoud vereenvoudigen | Inhoud optimaliseren | Hiermee markeert u pagina&#39;s met complexe tekst die AI-begrip kan belemmeren. | Verstrekt door AI gegenereerde vereenvoudigde versies van complexe test met behoud van de oorspronkelijke betekenis. | Hiermee herschrijft u complexe secties op de pagina en verbetert u de leesbaarheid van AI. |

### Zichtbaarheid van inhoud herstellen

Deze kans geeft pagina&#39;s weer waar de belangrijkste inhoud verborgen is voor AI-agents vanwege renderen op de client. Voor elke geïdentificeerde pagina wordt exact weergegeven welke inhoud ontbreekt in de AI-agentweergave, worden de zichtbaarheidsverschillen gemarkeerd en kunt u direct wijzigingen toepassen om de verborgen inhoud te herstellen. Wanneer u deze kans met Optimize in Edge opstelt, wordt een pre-teruggegeven, AI-geoptimaliseerde versie van de pagina aan gebruikersagenten LLM getoond zodat kunnen zij tot de volledige context toegang hebben zonder JavaScript uit te voeren.

**dit pre-teruggevend vermogen is automatisch op alle kansen van toepassing die wanneer opgesteld met Optimize bij Edge volgen.** Zo weet u zeker dat de pagina volledig zichtbaar is voor AI-agents. Er worden aanvullende verbeteringen toegepast op die vooraf gerenderde HTML.

#### Extra gereedschappen

Is uw webpagina te vinden? De [&#x200B; Adobe LLM Optimizer: Is uw webpagina citeerbaar?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Met de Chrome-extensie kunt u precies zien hoeveel van uw webpagina-inhoud LLM&#39;s kunnen benaderen en wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie.

Met één klik kunt u de gereedschapsleesbaarheid van elke site evalueren, naast elkaar een vergelijking bekijken van wat AI-agents zien ten opzichte van wat menselijke gebruikers zien en inschatten hoeveel inhoud met LLM Optimizer kan worden hersteld. Zie [&#x200B; AI uw website lezen?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) voor meer informatie.

### Koppen voor LLM&#39;s optimaliseren

Deze kans detecteert pagina&#39;s waar de kopstructuur het voor AI-agents moeilijk maakt de pagina te begrijpen vanwege lege, dubbele, ontbrekende of dubbelzinnige koppen. Voor elke betrokken pagina wordt met deze optie de suboptimale koppen weergegeven en wordt een duidelijkere hiërarchie aanbevolen. Bij de implementatie met Optimize in Edge worden de verbeterde koppen in de HTML toegepast op zintuiglijk verkeer, wat kan helpen de leesbaarheid van de machine te verbeteren terwijl uw mensgerichte lay-out onveranderd blijft.

### LLM-vriendelijke samenvattingen toevoegen

Deze kans identificeert pagina&#39;s die van beknopte overzichten kunnen profiteren om LLMs te helpen snel begrijpen waar de pagina over is. Voor elke pagina, ontdekt de kans waar een samenvatting het meest nodig is en leidt tot AI-geproduceerde samenvattingen op paginaniveau en/of sectieniveau. Wanneer u met Optimize bij Edge opstelt worden deze samenvattingen opgenomen in de HTML die AI agenten terugwinnen, verbeterend de kansen om uw inhoud te hebben nauwkeuriger worden beschreven.

### Relevante veelgestelde vragen toevoegen

Deze kans markeert pagina&#39;s waar de extra inhoud van Vragen en antwoorden beter gebruikersintent en herinneringen in AI-gedreven ontdekking kon aanpassen. Voor elke pagina worden door AI gegenereerde blokken FAQ voorgesteld die zijn gekoppeld aan de gebruikersinhoud en -inhoud op de pagina. Met Optimize in Edge worden deze veelgestelde vragen in de HTML geïnjecteerd, waardoor uw pagina AI-vriendelijker wordt en de kans groter wordt dat de AI-antwoorden direct uw richtlijnen weerspiegelen.

### Complexe inhoud vereenvoudigen

Deze kans vindt pagina&#39;s met lange, complexe alinea&#39;s die AI-begrip kunnen verminderen. Voor elke pagina die de leesbaarheidsdrempels overschrijdt, wordt er door AI gegenereerde inhoud gemaakt die eenvoudiger en scannbaarder is, terwijl de oorspronkelijke betekenis behouden blijft. Wanneer opgesteld bij de rand, de vereenvoudigde inhoud die aan agentic verkeer wordt geleverd helpt LLMs uw inhoud interpreteren en nauwkeuriger samenvatten.

## Suggesties

Voor elke gelegenheid kunt u de optimalisaties aan de rand voorvertonen, bewerken, implementeren, live voorvertonen en terugdraaien.

### Voorvertoning

Met Voorvertoning kunnen gebruikers zien wat het effect is van een suggestie op de pagina voordat er iets live gaat. Er wordt een verschil tussen de huidige pagina en de voor AI geoptimaliseerde versie verwacht na het toepassen van de suggestie. In deze weergave wordt dezelfde logica voor optimaliseren bij Edge gebruikt die live verkeer mogelijk maakt, maar in een veilige, geïsoleerde voorvertoningsmodus. Dit beïnvloedt levend verkeer niet aangezien het een read-only simulatie voor overzicht is.

![&#x200B; Voorproef &#x200B;](/help/assets/optimize-at-edge/preview.png)

### Bewerken

Met Bewerken kunnen gebruikers de automatisch gegenereerde suggestie verfijnen of herschrijven voordat ze deze implementeren. In plaats van passief de suggestie te accepteren, behouden gebruikers volledige controle via deze &#39;human-in-the-loop&#39; workflow. In de weergave worden voorgestelde wijzigingen weergegeven in een gestructureerde editor, waar gebruikers de tekst kunnen wijzigen om deze beter aan te passen aan hun intentie. De bewerkte versie wordt vervolgens aan AI-agents geleverd zodra deze zijn geïmplementeerd.

![&#x200B; geeft &#x200B;](/help/assets/optimize-at-edge/edit.png) uit

### Implementeren

Met Deploy publiceert u de geselecteerde suggesties, zodat de geoptimaliseerde ervaringen van de rand naar AI-agents kunnen worden gestuurd. Als CDN volledig wordt verpletterd, gaan alle pagina&#39;s in het domein met de nieuwe veranderingen typisch binnen notulen. Als het verpletteren voor uitgezochte wegen slechts is gevormd, slechts gaan de gevoegde op lijst van gewenste personen pagina&#39;s met de optimalisaties.

![&#x200B; opstellen &#x200B;](/help/assets/optimize-at-edge/deploy.png)

### Live weergeven

Met Live View kunnen gebruikers controleren of de optimalisatie live is en zich gedraagt zoals verwacht voor zintuiglijk verkeer, een weergave die anders moeilijk toegankelijk zou zijn. Gebruikers kunnen de actieve pagina weergeven onder Vaste suggesties, waardoor de pagina wordt weergegeven zoals deze wordt weergegeven aan AI-agents.

![&#x200B; Levende Mening &#x200B;](/help/assets/optimize-at-edge/view-live.png)

### Terugdraaien

Met Terugdraaien wordt een eerder geïmplementeerde optimalisatie veilig hersteld. De alleen-AI-versie van de pagina wordt doorgaans binnen enkele minuten teruggezet naar de vorige staat, zodat gebruikers, indien nodig, veilig kunnen experimenteren met optimalisaties.

![&#x200B; Terugkeer &#x200B;](/help/assets/optimize-at-edge/rollback.png)

## Veelgestelde vragen

V. Welk soort LLMs richt u met Optimize bij Edge?

De lijst van gebruikersagenten aan doel wordt volledig bepaald door de klant bij onboarding.

V. Wat betekent &quot;Edge&quot; in Optimize in Edge?

In onze context betekent &quot;Edge&quot; dat de optimalisatie wordt toegepast op de CDN-laag en niet binnen uw CMS.

V. Waarom vereist deze optimalisatie een CDN?

In CDN wordt de geoptimaliseerde versie van de pagina samengesteld en aan AI-agents geleverd. We gebruiken de CDN om ervoor te zorgen dat de CMS van oorsprong ongewijzigd blijft. Met deze scheiding kunt u de zichtbaarheid van LLM verbeteren zonder de bestaande publicatieworkflows te wijzigen.

V. Wat gebeurt er als ik nog niet aan boord ben om te optimaliseren in Edge?

Als u **klikt stel optimalisaties** op alvorens de vereiste opstelling te voltooien, zal niets op uw plaats worden toegepast. In plaats daarvan wordt u in een pop-updialoogvenster gevraagd contact op te nemen met ons team op llmo-at-edge@adobe.com voor hulp bij het instappen. Totdat het instappen volledig is, kunt u nog de ontdekte kansen en de suggesties onderzoeken, maar de één-klik plaatsingswerkschema zal inactief blijven.

V: Wat gebeurt er als de inhoud bij de bron wordt bijgewerkt?

Wij dienen de geoptimaliseerde versie van de pagina van geheim voorgeheugen zolang de onderliggende bronpagina niet is veranderd. Wanneer de bron echter wel verandert, wordt ons systeem automatisch vernieuwd, zodat AI-agents altijd de meest actuele inhoud ontvangen. Dit komt omdat we TTL&#39;s met lage cache in volgorde van minuten gebruiken, zodat updates van inhoud op uw site een nieuwe optimalisatie binnen dat venster activeren. Aangezien er geen universele TTL is die elke plaats past, kunnen wij deze TTL vormen die op uw regels van de geheim voorgeheugenongeldigheid wordt gebaseerd om beide systemen te verzekeren in synchronisatie blijven.

V. Is Optimize bij Edge alleen voor sites die gebruikmaken van Adobe Edge Delivery Service (EDS)?

Nee. Optimaliseren in Edge is niet alleen CDN-agnostisch en werkt met elke front-end architectuur, niet alleen met architectuur die op Adobe EDS Stack wordt geïmplementeerd.

V. Hoe wordt Optimaliseren bij Edge-pre-rendering anders dan bij traditionele rendering op de server?

Deze twee oplossingen bieden verschillende problemen en kunnen samenwerken. Traditionele SSR rendert inhoud aan serverzijde maar omvat geen inhoud die later in browser wordt geladen. Optimaliseren bij voorrendering van Edge legt de pagina vast nadat JavaScript en client-side gegevens zijn geladen, waardoor de volledig geassembleerde versie aan de CDN-rand wordt geproduceerd. SSR richt zich op het verbeteren van de menselijke ervaring en Optimize in Edge verbetert de webervaring voor LLMs.


















