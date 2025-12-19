---
title: Optimaliseren bij Edge
description: Leer hoe u optimalisaties in LLM Optimizer kunt leveren aan de CDN-rand zonder dat er ontwerpwijzigingen nodig zijn.
feature: Opportunities
source-git-commit: 1ef457043d1ad06dc7fa19363fab232562b30d6c
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 0%

---


# Optimaliseren bij Edge

Deze pagina biedt een gedetailleerd overzicht van hoe u optimalisaties aan de CDN-rand kunt leveren zonder dat er ontwerpwijzigingen nodig zijn. Het behandelt het aan boord gaan proces, de beschikbare optimaliseringsmogelijkheden en hoe te om aan rand automatisch te optimaliseren.

>[!NOTE]
>Deze functionaliteit is momenteel in Vroege Toegang.

## Wat is Optimize in Edge?

Optimaliseren bij Edge is een op randen gebaseerde implementatiefunctie in LLM Optimizer die voor AI vriendelijke wijzigingen zorgt voor LLM-gebruikersagents. In de huidige context betekent &quot;Edge&quot; dat de optimalisatie wordt toegepast op de CDN-laag. Omdat het optimalisaties bij de laag CDN levert, worden geen auteursveranderingen in het Systeem van het Beheer van de Inhoud (CMS) vereist zodat uw oorsprong CMS onveranderd blijft. Met deze scheiding kunt u de zichtbaarheid van LLM verbeteren zonder de bestaande publicatieworkflows te wijzigen. Het is alleen gericht op agentisch verkeer en heeft geen invloed op menselijke gebruikers of SEO-bots. Wanneer LLM Optimizer mogelijkheden detecteert om een pagina te optimaliseren, kunnen gebruikers correcties direct bij de CDN-rand implementeren.

Optimaliseren in Edge is een sneller en leener alternatief voor traditionele oplossingen die complexe technische inspanningen vereisen. Zoals vermeld, zodra u eenmalig opstelling voltooit, worden geen platformveranderingen of lange ontwikkelingscycli vereist om de veranderingen toe te passen. U kunt verbeteringen in minuten publiceren zonder dat u hiervoor de betrokkenheid van de ontwikkelaar nodig hebt. U kunt uw website op deze manier zonder code optimaliseren voor AI-agents.

Optimaliseren in Edge is ontworpen voor zakelijke gebruikers in marketing-, SEO-, content- en digitale strategische teams. Zo kunnen zakelijke gebruikers de volledige reis in LLM Optimizer voltooien: mogelijkheden identificeren, suggesties begrijpen en de oplossingen eenvoudig implementeren. Met Optimaliseren bij Edge kunnen gebruikers de wijzigingen voorvertonen, deze snel implementeren aan de CDN-rand en controleren of de optimalisaties live zijn. Prestaties kunnen worden bijgehouden in het ecosysteem van LLM Optimizer.

### Belangrijkste voordelen

* **AI-slechts levering:** serveert geoptimaliseerde HTML slechts aan AI agenten zonder invloed op of menselijke bezoekers of OSEO bots.
* **Snellere cycli:** publiceer veranderingen in notulen, niet weken. Er zijn geen platformwijzigingen of lange technische cycli vereist.
* **Omkeerbaar:** gesteund met één-klik het terugschroeven van prijzen vermogen dat de pagina in notulen kan terugkeren.
* **geen prestatieseffect:** Op Edge gebaseerde optimalisaties en caching houden plaatslatentie onaangetast.
* **CDN en CMS-agnostic:** werkt met om het even welke configuratie CDN en front-end opstelling ongeacht het Systeem van het Beheer van de Inhoud.

### Welke mogelijkheden worden gesteund met Optimize in Edge?

De kansen die de agentische Webervaring kunnen verbeteren worden gesteund met Optimize in Edge. Leer meer over elke kans zowel in de [&#x200B; pagina van het Dashboard van Kansen &#x200B;](/help/dashboards/opportunities.md) als de opportuniteitssectie in de huidige pagina.

## Onboarding

Neem contact op met uw Adobe-accountteam of FDE-team om het instapproces te starten. Uw IT- of CDN-team is ook vereist om de voorwaarden en het installatieproces te voltooien. Daarnaast kunt u ook contact opnemen met ons team op `llmo-at-edge@adobe.com` voor verdere assistentie bij het instappen.

Voorwaarden voor optimalisatie aan boord in Edge:

* Voltooi het instapproces naar LLM Optimizer.
* Voltooi het logboek door:sturen proces voor uw CDN logboeken.

Vereisten voor uw IT/CDN-team:

* Een API-sleutel genereren.
* Voeg Optimize bij Edge toe die regels in CDN verplettert.
* Door de gebruiker gedefinieerde paden of het hele domein Lijsten van gewenste personen.
* Voeg een user-defined lijst van gebruikersagenten LLM aan doel toe.
* Zorg ervoor dat `robots.txt` geen gebruikersagents blokkeert die zijn bedoeld als doel.
* Bevestig Optimaliseren bij Edge-routering in de LLM Optimizer-interface.

Om het installatieproces te begeleiden, hieronder voorgesteld, zijn steekproefconfiguratie voor een aantal montages CDN. Deze voorbeelden moeten worden aangepast aan uw werkelijke live configuratie. We raden u aan eerst wijzigingen toe te passen in de lagere omgevingen.

>[!NOTE]
>In de onderstaande codevoorbeelden ziet u verwijzingen naar &quot;tokowaka&quot;, de naam van het werkende project voor Optimize in Edge. Deze id&#39;s blijven voor compatibiliteitsdoeleinden in de code en verwijzen naar dezelfde mogelijkheden die in deze documentatie worden beschreven.

>[!BEGINTABS]

>[!TAB  Adobe beheerde CDN ]

**Adobe beheerde CDN**

Het doel van deze configuratie is verzoeken met agentische gebruikersagenten te vormen die aan de Optimizer dienst (`edge.tokowaka.now` backend) zullen worden verpletterd. Als u de configuratie wilt testen, zoekt u na de installatie naar de header `x-tokowaka-request-id` in de reactie.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-tokowaka-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

De verpletterende configuratie wordt gedaan door een [&#x200B; originSelector CDN regel &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors) te gebruiken. De voorwaarden zijn als volgt:

* beslissen welk domein moet worden verpletterd
* bepalen welke paden moeten worden gerouteerd
* beslissen de gebruikersagenten om worden verpletterd (geadviseerde regex)

Om de regel op te stellen, moet u:

* creeer de pijpleiding van de a [&#x200B; configuratie &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* het configuratiebestand van `cdn.yaml` toewijzen in uw opslagplaats
* de configuratiepijplijn uitvoeren


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
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"
```

Voer een krulling uit en verwacht het volgende om de instelling te testen:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-tokowaka-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

<!-- >>[!TAB Akamai (BYOCDN)]

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

Important considerations:

* Tokowaka Rule will be ON based on User-Agent + Path + x-tokowaka-request (if not present) + TOKOWAKA_DISABLE variable (to allow switch off using a single variable toggle)
* Set up rules to **Modify Incoming Request Headers** rule to set custom headers
* Set cache-key in Akamai using user defined variable through Cache-ID modification mechanism. Only a single user defined variable is allowed, so create a separate variable for cache_key and set it accordingly.
* Lang: extracted from Accept-Language header using "regex": "^([a-zA-Z]{2}).*"
* With Cache ID Modification within a match on User Agent, the content can't be purged by URL (just FYI)
* Site failover mechanism: With the match on User-Agent rule, Akamai does not allows to failover based on health check, but only only basis of origin response/connectivity per request. Set **x-tokowaka-fo:true**  resp header in case of failover response.
* SWR is not supported by Akamai. So, only TTL based caching is there. So, configure a rule in Akamai to strip Age header from origin response else TTL based caching would not work.
* Ensure that the Tokowaka rule is the bottom most rule in the rule hierarchy (so that it overrides all other rules).-->

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

>[!NOTE]
>Neem voor andere CDN-providers contact op met `llmo-at-edge@adobe.com` om uw IT/CDN-teams te helpen bij het instappen. Zodra de installatieconfiguraties zijn voltooid, kunt u suggesties voor Optimize bij de kansen van Edge in LLM Optimizer opstellen.

## Kansen

Deze tabel vindt u in de volgende tabel met mogelijkheden die de taalkundige webervaring kunnen verbeteren en die worden ondersteund met Optimaliseren in Edge.

| Opportunity | Type | Automatisch identificeren | Automatisch voorstellen | Automatisch optimaliseren |
|---------|----------|----------|----------|----------|
| Zichtbaarheid van inhoud herstellen | Technische GEO | Detecteert pagina&#39;s waarop kritieke inhoud van AI-agents wordt verborgen. Hiermee worden beïnvloede URL&#39;s en verwachte inhoud weergegeven die kunnen worden hersteld. | Hiermee wordt de inhoud gemarkeerd die beschikbaar kan worden gemaakt voor AI-agents en wordt aangeraden om pre-rendering voor deze pagina&#39;s in te schakelen. | Serveert een volledig teruggegeven, AI-vriendschappelijke momentopname van HTML aan zinloos verkeer dat de eerder verborgen inhoud terugkrijgt. |
| Koppen voor LLM&#39;s optimaliseren | Inhoud optimaliseren | Scant koppen om lege, dubbele, ontbrekende of dubbelzinnige koppen te detecteren die de leesbaarheid van de machine kunnen verminderen. | Stelt een duidelijkere koptekshiërarchie en verbeterde labels voor en toont een voorvertoning van de bijgewerkte structuur voor elke pagina. | Hiermee wordt de verbeterde kopstructuur voor AI-agents geïnjecteerd, zodat uw visuele ontwerp behouden blijft en de pagina beter leesbaar wordt voor LLM&#39;s. |
| LLM-vriendelijke samenvattingen toevoegen | Inhoud optimaliseren | Hiermee worden lange of complexe pagina&#39;s aangegeven waarvoor geen beknopte overzichten op pagina- of sectieniveau beschikbaar zijn, waardoor het voor AI moeilijker wordt om snel te scannen en te begrijpen. | Hiermee raadt u korte, door AI gegenereerde samenvattingen op pagina- en sectieniveau aan die de belangrijkste inhoud vastleggen. | Hiermee voegt u de samenvattingen in de desbetreffende HTML-secties in, waardoor modellen de pagina-inhoud beter kunnen interpreteren en beschrijven. |
| Relevante veelgestelde vragen toevoegen | Inhoud optimaliseren | Hiermee worden gaten in de intentie in de bestaande pagina-inhoud gedetecteerd die baat kunnen hebben bij veelgestelde vragen. | Stelt door AI gegenereerde veelgestelde vragen-inhoud voor die is uitgelijnd op de gebruikersinstelling en bestaande onderwerpen. | Hiermee wordt veelgestelde vragen-inhoud in de HTML geïnjecteerd, waardoor pagina&#39;s beter te ontdekken en relevanter worden in door AI gestuurde antwoorden. |
| Complexe inhoud vereenvoudigen | Inhoud optimaliseren | Hiermee markeert u pagina&#39;s met complexe tekst die AI-begrip kan belemmeren. | Biedt door AI gegenereerde vereenvoudigde versies van complexe tekst met behoud van de oorspronkelijke betekenis. | Hiermee herschrijft u complexe secties op de pagina en verbetert u de leesbaarheid van AI. |

### Extra gereedschappen

De [&#x200B; Adobe LLM Optimizer: Is uw webpagina citeerbaar?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Met de Chrome-extensie kunt u precies zien hoeveel van uw webpagina-inhoud LLM&#39;s kunnen benaderen en wat verborgen blijft. Deze software is ontworpen als een gratis, standalone diagnoseprogramma en vereist geen productlicentie of installatie.

Met één klik kunt u de gereedschapsleesbaarheid van elke site evalueren. U kunt een vergelijking naast elkaar bekijken van wat AI agenten tegenover zien wat menselijke gebruikers zien, en schatten hoeveel inhoud door LLM Optimizer kon worden teruggekregen. Zie [&#x200B; AI uw website lezen?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) voor meer informatie.

## Gedetailleerde mogelijkheden

In de volgende secties kunt u aanvullende details bekijken voor elke opportuniteit die wordt ondersteund bij Optimaliseren in Edge.

### Zichtbaarheid van inhoud herstellen

Deze kans geeft pagina&#39;s weer waar de belangrijkste inhoud verborgen is voor AI-agents vanwege renderen op de client. Voor elke geïdentificeerde pagina wordt precies weergegeven welke inhoud ontbreekt in de AI-agentweergave, worden de zichtbaarheidsverschillen gemarkeerd en kunt u direct wijzigingen toepassen om de verborgen inhoud te herstellen. Wanneer u deze kans met Optimize in Edge opstelt, wordt een pre-teruggegeven, AI-geoptimaliseerde versie van de pagina aan gebruikersagenten LLM getoond zodat kunnen zij tot de volledige context toegang hebben zonder JavaScript uit te voeren.
Dit zorgt ervoor dat de pagina voor het eerst volledig zichtbaar is voor AI-agents. Er worden aanvullende verbeteringen toegepast op die vooraf gerenderde HTML.

>[!IMPORTANT]
>Deze pre-renderfunctie is automatisch van toepassing op alle hieronder weergegeven mogelijkheden bij Optimaliseren in Edge om ervoor te zorgen dat de pagina volledig zichtbaar is voor AI-agents.

### Koppen voor LLM&#39;s optimaliseren

Deze kans detecteert pagina&#39;s waar de kopstructuur het voor AI-agents moeilijk maakt de pagina te begrijpen vanwege lege, dubbele, ontbrekende of dubbelzinnige koppen. Voor elke betrokken pagina wordt met deze optie de suboptimale koppen weergegeven en wordt een duidelijkere hiërarchie aanbevolen. Wanneer opgesteld met Optimize in Edge, worden de betere rubrieken toegepast in HTML die aan agentic verkeer wordt gediend. Hierdoor is de machine beter leesbaar en blijft de persoonlijke lay-out ongewijzigd.

### LLM-vriendelijke samenvattingen toevoegen

Deze kans identificeert pagina&#39;s die van beknopte samenvattingen kunnen profiteren om LLM&#39;s te helpen snel begrijpen waar de pagina-inhoud over gaat. Voor elke pagina, ontdekt de kans waar een samenvatting het meest nodig is en leidt tot AI-geproduceerde samenvattingen of op paginaniveau of sectieniveau. Wanneer u met Optimize bij Edge opstelt worden deze samenvattingen opgenomen in de HTML die AI agenten terugwinnen, verbeterend de kansen om uw inhoud te hebben nauwkeuriger worden beschreven.

### Relevante veelgestelde vragen toevoegen

Met deze mogelijkheid worden pagina&#39;s gemarkeerd waar extra inhoud van Vragen en antwoorden beter kan overeenkomen met de gebruikerintentie en aanwijzingen voor detectie met een AI-basis. Voor elke pagina worden door AI gegenereerde blokken FAQ voorgesteld die zijn gekoppeld aan de gebruikersinhoud en -inhoud op de pagina. Met Optimize in Edge worden deze veelgestelde vragen in de HTML geïnjecteerd, waardoor uw pagina AI-vriendelijker wordt en de kans groter wordt dat de AI-antwoorden direct uw richtlijnen weerspiegelen.

### Complexe inhoud vereenvoudigen

Deze kans vindt pagina&#39;s met lange, complexe alinea&#39;s die AI-begrip kunnen verminderen. Voor elke pagina die de leesbaarheidsdrempels overschrijdt, wordt door AI gegenereerde inhoud gemaakt die eenvoudiger en gemakkelijker te scannen is, terwijl de oorspronkelijke betekenis behouden blijft. Wanneer opgesteld bij de rand, de vereenvoudigde inhoud die aan agentic verkeer wordt geleverd helpt LLMs uw inhoud interpreteren en nauwkeuriger samenvatten.

## Automatisch optimaliseren bij Edge

Voor elke gelegenheid, kunt u voorproef, uitgeven, opstellen, levende bekijken, en de optimalisaties bij de rand terugdraaien.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Voorvertoning

**Voorproef** laat u het effect van een suggestie zien alvorens het live gaat. Er wordt een verschil tussen de huidige pagina en de voor AI geoptimaliseerde versie verwacht na het toepassen van de suggestie. In deze weergave wordt dezelfde functie Optimaliseren bij Edge gebruikt die live verkeer, maar in een geïsoleerde voorvertoningsmodus, mogelijk maakt. Dit beïnvloedt levend verkeer niet aangezien het een read-only simulatie voor overzicht is.

![&#x200B; Voorproef &#x200B;](/help/assets/optimize-at-edge/preview.png)

### Bewerken

**geeft** uit staat u toe om de auto-geproduceerde suggestie te verfijnen of geheel te herschrijven alvorens het op te stellen. In plaats van de suggestie te accepteren, kunt u de volledige controle behouden via de bewerkingsworkflow. In de weergave worden voorgestelde wijzigingen weergegeven in een gestructureerde editor, waar u de tekst kunt wijzigen zodat deze beter aansluit bij uw oorspronkelijke intentie. De bewerkte versie wordt vervolgens aan AI-agents geleverd zodra deze zijn geïmplementeerd.

![&#x200B; geeft &#x200B;](/help/assets/optimize-at-edge/edit.png) uit

### Implementeren

**stelt** op publiceert de geselecteerde suggesties zodat kunnen de geoptimaliseerde ervaringen van de rand aan AI agenten worden gediend. Als CDN volledig wordt verpletterd, gaan alle pagina&#39;s in het domein gewoonlijk met de nieuwe veranderingen binnen notulen. Als het verpletteren voor uitgezochte wegen slechts is gevormd, slechts gaan de gevoegde op lijst van gewenste personen pagina&#39;s met de optimalisaties.

![&#x200B; opstellen &#x200B;](/help/assets/optimize-at-edge/deploy.png)

### Live weergeven

**Levende Mening** laat u verifiëren dat de optimalisering levend is en zich zoals verwacht voor agentisch verkeer gedraagt, een mening die anders moeilijk zou zijn om toegang te hebben. U kunt de actieve pagina weergeven onder Vaste suggesties, waardoor de pagina wordt weergegeven zoals deze wordt weergegeven bij AI-agents.

![&#x200B; Levende Mening &#x200B;](/help/assets/optimize-at-edge/view-live.png)

### Terugdraaien

Met Terugdraaien wordt een eerder geïmplementeerde optimalisatie veilig hersteld. De alleen-AI versie van de pagina wordt doorgaans binnen enkele minuten teruggezet naar de vorige staat, zodat u indien nodig veilig met optimalisaties kunt experimenteren.

![&#x200B; Terugkeer &#x200B;](/help/assets/optimize-at-edge/rollback.png)

## Veelgestelde vragen

V. Welk soort LLMs richt u met Optimize bij Edge?

De lijst van gebruikersagenten aan doel wordt bepaald door u tijdens het aan boord gaan proces.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

V. Wat gebeurt er als ik nog niet aan boord ben om te optimaliseren in Edge?

Als u **klikt stel optimalisaties** op alvorens de vereiste opstelling te voltooien, zal niets op uw plaats worden toegepast. In plaats daarvan wordt u in een pop-updialoogvenster gevraagd contact op te nemen met ons team op `llmo-at-edge@adobe.com` voor hulp bij het instappen. Totdat het instappen volledig is, kunt u nog de ontdekte kansen en de suggesties onderzoeken, maar de één-klik plaatsingswerkschema zal inactief blijven.

V: Wat gebeurt er als de inhoud bij de bron wordt bijgewerkt?

Wij dienen de geoptimaliseerde versie van de pagina van geheim voorgeheugen zolang de onderliggende bronpagina niet is veranderd. Wanneer de bron echter wel verandert, wordt ons systeem automatisch vernieuwd, zodat AI-agents altijd de meest actuele inhoud ontvangen. Dit komt doordat we de FLV-instellingen (in volgorde van minuten) gebruiken om een lage cache op te slaan, zodat bij elke update van de inhoud op uw site een nieuwe optimalisatie binnen dat venster wordt geactiveerd. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

V. Is Optimize bij Edge alleen voor sites die gebruikmaken van Adobe Edge Delivery Service (EDS)?

Nee. Optimaliseren in Edge is niet alleen CDN-agnostisch en werkt met elke front-end architectuur, maar ook met de architectuur die op Adobe EDS Stack wordt geïmplementeerd.

V. Hoe wordt Optimaliseren bij Edge-pre-rendering anders dan bij traditionele rendering op de server?

Beide problemen lossen verschillende problemen op en kunnen samenwerken. Traditionele SSR rendert inhoud aan serverzijde maar omvat geen inhoud die later in browser wordt geladen. Optimaliseren bij voorrendering van Edge legt de pagina vast nadat JavaScript en client-side gegevens zijn geladen, waardoor de volledig geassembleerde versie aan de CDN-rand wordt geproduceerd. SSR richt zich op het verbeteren van de menselijke ervaring en Optimize in Edge verbetert de webervaring voor LLMs.
