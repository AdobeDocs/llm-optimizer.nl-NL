---
title: Optimaliseren bij Edge - Cloudflare (BYOCDN)
description: Leer hoe u Cloudflare BYOCDN configureert voor optimaliseren bij Edge in LLM Optimizer.
feature: Opportunities
source-git-commit: 23752b30294c3d467ca477b085aa521cad0f72ca
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---


# Cloudflare (BYOCDN)

Deze configuratie leidt verwerpelijk verkeer (verzoeken van AI bots en gebruikersagenten LLM) aan de Edge Optimize backend dienst (`live.edgeoptimize.net`). Menselijke bezoekers en SEO-bots worden nog steeds van je herkomst bediend zoals gewoonlijk. Als u de configuratie wilt testen nadat de installatie is voltooid, zoekt u naar de koptekst `x-edgeoptimize-request-id` in de reactie.

**Eerste vereisten**

Voordat u de Cloudflare Worker instelt die regels routeert, moet u ervoor zorgen dat:

* Een Cloudflare-account met workers die op uw domein zijn ingeschakeld.
* Toegang tot DNS-instellingen van uw domein in Cloudflare.
* Voltooid het LLM Optimizer-instapproces.
* Voltooid het logboek CDN door:sturen aan LLM Optimizer.
* Een Edge Optimize API-sleutel die is opgehaald uit de gebruikersinterface van LLM Optimizer.

{{retrieve-byocdn-api-key}}

**hoe het verpletteren van werken**

Wanneer correct gevormd, wordt een verzoek aan uw domein (bijvoorbeeld, `www.example.com/page.html`) van een agentische gebruikersagent onderschept door de Arbeider van de Vormgeving van de Wolk en verpletterd aan het Edge Optimize achtereind. Het achterste verzoek omvat de vereiste kopballen.

**het Testen van het achterste eindverzoek**

U kunt het verpletteren verifiëren door een direct verzoek aan Edge te richten optimaliseert achtereind.

```
curl -svo /dev/null https://live.edgeoptimize.net/page.html \
  -H 'x-forwarded-host: www.example.com' \
  -H 'x-edgeoptimize-url: /page.html' \
  -H 'x-edgeoptimize-api-key: $EDGE_OPTIMIZE_API_KEY' \
  -H 'x-edgeoptimize-config: LLMCLIENT=TRUE;'
```

**Vereiste Kopballen**

Bij aanvragen naar de Edge Optimize-backend moeten de volgende headers worden ingesteld:

| Koptekst | Beschrijving | Voorbeeld |
|--------|-------------|---------|
| `x-forwarded-host` | De oorspronkelijke host van de aanvraag. Vereist voor identificatie van het sitedomein. | `www.example.com` |
| `x-edgeoptimize-url` | Het oorspronkelijke URL-pad en de queryreeks van de aanvraag. | `/page.html` of `/products?id=123` |
| `x-edgeoptimize-api-key` | De API-sleutel die Adobe voor uw domein biedt. | `your-api-key-here` |
| `x-edgeoptimize-config` | De koord van de configuratie voor geheim voorgeheugenzeer belangrijke differentiatie. | `LLMCLIENT=TRUE;` |

**Stap 1: Creeer de Worker van de Veldarm**

1. Meld u aan bij het dashboard Cloudflare.
2. Navigeer aan **Arbeiders &amp; Pagina&#39;s** in sidebar.
3. Klik **creëren toepassing** en dan **creëren de Arbeider**.
4. Geef de worker een naam (bijvoorbeeld `edge-optimize-router` ).
5. Klik **opstellen** om de worker met de standaardcode tot stand te brengen.

![ dashboard van de Werknemers van de Wolk ](/help/assets/optimize-at-edge/cloudflare-workers-dashboard.png)

**Stap 2: Voeg de code van de Arbeider** toe

Na het creëren van de arbeider, geeft de klik **code** uit en vervangt de standaardcode met het volgende:

```javascript
/**
 * Edge Optimize BYOCDN - Cloudflare Worker
 *
 * This worker routes requests from agentic bots (AI/LLM user agents) to the
 * Edge Optimize backend service for optimized content delivery.
 *
 * Features:
 * - Routes agentic bot traffic to Edge Optimize backend
 * - Failover to origin on Edge Optimize errors (any 4XX or 5XX errors)
 * - Loop protection to prevent infinite redirects
 * - Human visitors and SEO bots are served from the origin as usual
 */

// List of agentic bot user agents to route to Edge Optimize
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User'
];

// Targeted paths for Edge Optimize routing
// Set to null to route all HTML pages, or specify an array of paths
const TARGETED_PATHS = null; // e.g., ['/', '/page.html', '/products']

// Failover configuration
// Failover on any 4XX client error or 5XX server error from Edge Optimize
const FAILOVER_ON_4XX = true; // Failover on any 4XX error (400-499)
const FAILOVER_ON_5XX = true; // Failover on any 5XX error (500-599)

export default {
  async fetch(request, env, ctx) {
    return await handleRequest(request, env, ctx);
  },
};

async function handleRequest(request, env, ctx) {
  const url = new URL(request.url);
  const userAgent = request.headers.get("user-agent")?.toLowerCase() || "";

  // Check if request is already processed (loop protection)
  const isEdgeOptimizeRequest = !!request.headers.get("x-edgeoptimize-request");

  // Construct the original path and query string
  const pathAndQuery = `${url.pathname}${url.search}`;

  // Check if the path matches HTML pages (no extension or .html extension)
  const isHtmlPage = /(?:\/[^./]+|\.html|\/)$/.test(url.pathname);

  // Check if path is in targeted paths (if specified)
  const isTargetedPath = TARGETED_PATHS === null
    ? isHtmlPage
    : (isHtmlPage && TARGETED_PATHS.includes(url.pathname));

  // Check if user agent is an agentic bot
  const isAgenticBot = AGENTIC_BOTS.some((ua) => userAgent.includes(ua.toLowerCase()));

  // Route to Edge Optimize if:
  // 1. Request is NOT already from Edge Optimize (prevents infinite loops)
  // 2. User agent matches one of the agentic bots
  // 3. Path is targeted for optimization
  if (!isEdgeOptimizeRequest && isAgenticBot && isTargetedPath) {

    // Build the Edge Optimize request URL
    const edgeOptimizeURL = `https://live.edgeoptimize.net${pathAndQuery}`;

    // Clone and modify headers for the Edge Optimize request
    const edgeOptimizeHeaders = new Headers(request.headers);

    // Remove any existing Edge Optimize headers for security
    edgeOptimizeHeaders.delete("x-edgeoptimize-api-key");
    edgeOptimizeHeaders.delete("x-edgeoptimize-url");
    edgeOptimizeHeaders.delete("x-edgeoptimize-config");

    // x-forwarded-host: The original site domain
    // Use environment variable if set, otherwise use the request host
    edgeOptimizeHeaders.set("x-forwarded-host", env.EDGE_OPTIMIZE_TARGET_HOST ?? url.host);

    // x-edgeoptimize-api-key: Your Adobe-provided API key
    edgeOptimizeHeaders.set("x-edgeoptimize-api-key", env.EDGE_OPTIMIZE_API_KEY);

    // x-edgeoptimize-url: The original request URL path and query
    edgeOptimizeHeaders.set("x-edgeoptimize-url", pathAndQuery);

    // x-edgeoptimize-config: Configuration for cache key differentiation
    edgeOptimizeHeaders.set("x-edgeoptimize-config", "LLMCLIENT=TRUE;");

    try {
      // Send request to Edge Optimize backend
      const edgeOptimizeResponse = await fetch(new Request(edgeOptimizeURL, {
        headers: edgeOptimizeHeaders,
        redirect: "manual", // Preserve redirect responses from Edge Optimize
      }), {
        cf: {
          cacheEverything: true, // Enable caching based on origin's cache-control headers
        },
      });

      // Check if we need to failover to origin
      const status = edgeOptimizeResponse.status;
      const is4xxError = FAILOVER_ON_4XX && status >= 400 && status < 500;
      const is5xxError = FAILOVER_ON_5XX && status >= 500 && status < 600;

      if (is4xxError || is5xxError) {
        console.log(`Edge Optimize returned ${status}, failing over to origin`);
        return await failoverToOrigin(request, env, url);
      }

      // Return the Edge Optimize response
      return edgeOptimizeResponse;

    } catch (error) {
      // Network error or timeout - failover to origin
      console.log(`Edge Optimize request failed: ${error.message}, failing over to origin`);
      return await failoverToOrigin(request, env, url);
    }
  }

  // For all other requests (human users, SEO bots), pass through unchanged
  return fetch(request);
}

/**
 * Failover to origin server when Edge Optimize returns an error
 * @param {Request} request - The original request
 * @param {Object} env - Environment variables
 * @param {URL} url - Parsed URL object
 */
async function failoverToOrigin(request, env, url) {
  // Build origin URL
  const originURL = `${url.protocol}//${env.EDGE_OPTIMIZE_TARGET_HOST}${url.pathname}${url.search}`;

  // Prepare headers - clean Edge Optimize headers and add loop protection
  const originHeaders = new Headers(request.headers);
  originHeaders.set("Host", env.EDGE_OPTIMIZE_TARGET_HOST);
  originHeaders.delete("x-edgeoptimize-api-key");
  originHeaders.delete("x-edgeoptimize-url");
  originHeaders.delete("x-edgeoptimize-config");
  originHeaders.delete("x-forwarded-host");
  originHeaders.set("x-edgeoptimize-request", "fo");

  // Create and send origin request
  const originRequest = new Request(originURL, {
    method: request.method,
    headers: originHeaders,
    body: request.body,
    redirect: "manual",
  });

  const originResponse = await fetch(originRequest);

  // Add failover marker header to response
  const modifiedResponse = new Response(originResponse.body, {
    status: originResponse.status,
    statusText: originResponse.statusText,
    headers: originResponse.headers,
  });
  modifiedResponse.headers.set("x-edgeoptimize-fo", "1");
  return modifiedResponse;
}
```

Klik **sparen en stel** op om de worker te publiceren.

![ de coderedacteur van de Arbeider van de Wolk ](/help/assets/optimize-at-edge/cloudflare-worker-editor.png)

**Stap 3: Vorm omgevingsvariabelen**

Omgevingsvariabelen slaan gevoelige configuratie als de API-sleutel veilig op.

1. In de montages van uw worker, navigeer aan **Montages** > **Variabelen**.
2. Onder **Variabelen van het Milieu**, klik **veranderlijke** toevoegen.
3. Voeg de volgende variabelen toe:

   | Naam variabele | Beschrijving | Vereist |
   |---------------|-------------|----------|
   | `EDGE_OPTIMIZE_API_KEY` | De door Adobe verschafte Edge Optimize API-sleutel. | Ja |
   | `EDGE_OPTIMIZE_TARGET_HOST` | De doelhost voor Edge Optimize-aanvragen (verzonden als `x-forwarded-host` header) en het oorspronkelijke domein voor failover. Dit moet alleen het domein zijn zonder protocol (bijvoorbeeld `www.example.com` , niet `https://www.example.com` ). | Ja |

4. Voor de API sleutel, klik **Coderen** om het veilig op te slaan.
5. Klik **sparen en stel** op.

![ Cloudflare milieu variabelen ](/help/assets/optimize-at-edge/cloudflare-env-variables.png)

**Stap 4: Voeg een route aan uw domein** toe

De worker op uw domein activeren:

1. Ga naar de Montages van uw arbeider **** > **Trekkers**.
2. Onder **Routes**, klik **route** toevoegen.
3. Voer uw domeinpatroon in (bijvoorbeeld `www.example.com/*` of `example.com/*` ).
4. Selecteer de zone in het vervolgkeuzemenu.
5. Klik **sparen**.

Alternatief, kunt u routes op het streekniveau vormen:

1. Navigeer naar uw domein in Cloudflare.
2. Ga naar **Routes van de Arbeiders**.
3. Klik **toevoegen route** en specificeer het patroon en de arbeider.

![ de routes van de Arbeider van de Wolk ](/help/assets/optimize-at-edge/cloudflare-worker-routes.png)

**het verifiëren van failovergedrag**

Als Edge Optimize niet beschikbaar is of een fout retourneert, mislukt de worker automatisch naar de oorsprong. Voorbeelden van failover-reacties zijn de header `x-edgeoptimize-fo` :

```
< HTTP/2 200
< x-edgeoptimize-fo: 1
```

U kunt de gebeurtenissen van failover in de logboeken van de Werknemers van de Wolk controleren om kwesties problemen op te lossen.

**Begrijpend de logica van de Arbeider**

De Cloudflare Worker implementeert de volgende logica:

1. {de opsporing van de Agent van 0} Gebruiker:**controleert als de de gebruikersagent van het inkomende verzoek om het even welke bepaalde agentic bots (case-insensitive) aanpast.**

2. **Weg richtend:** naar keuze filters verzoeken die op gerichte wegen worden gebaseerd. Standaard worden alle HTML-pagina&#39;s (URL&#39;s die eindigen met `/` , geen extensie of `.html` ) gerouteerd. U kunt specifieke paden opgeven met de array `TARGETED_PATHS` .

3. **bescherming van de Lijn:** de `x-edgeoptimize-request` kopbal verhindert oneindige lijnen. Wanneer Edge Optimize aanvragen terugstuurt naar uw oorsprong, wordt deze header ingesteld op `"1"` en geeft de worker de aanvraag door zonder deze terug te sturen naar Edge Optimize.

4. **veiligheid van de Kopbal:** alvorens Edge te plaatsen optimaliseert kopballen, verwijdert de worker om het even welke bestaande `x-edgeoptimize-*` kopballen van het inkomende verzoek om de aanvallen van de kopbalinjectie te verhinderen.

5. **afbeelding van de Kopbal:** de arbeider plaatst de vereiste kopballen voor Edge optimaliseren:
   * `x-forwarded-host` - Identificeert het oorspronkelijke sitedomein.
   * `x-edgeoptimize-url` - Behoudt het oorspronkelijke aanvraagpad en de oorspronkelijke queryreeks.
   * `x-edgeoptimize-api-key` - Hiermee wordt de aanvraag geverifieerd met Edge Optimize.
   * `x-edgeoptimize-config` - Biedt een configuratie voor de cachemleutel.

6. **logica Failover:** als Edge optimaliseert om het even welke code van de foutenstatus terugkeert (4XX cliëntfouten of 5XX serverfouten) of het verzoek wegens een netwerkfout ontbreekt, ontbreekt de worker automatisch over aan uw oorsprong gebruikend `EDGE_OPTIMIZE_TARGET_HOST`. De failoverreactie omvat `x-edgeoptimize-fo: 1` kopbal om erop te wijzen dat failover voorkwam.

7. **Redirect behandeling:** de `redirect: "manual"` optie zorgt ervoor dat de omleidingsreacties van Edge optimaliseren door aan de cliënt zonder de worker worden overgegaan die hen volgt.

**het Aanpassen van de configuratie**

U kunt het arbeidersgedrag aanpassen door de configuratieconstanten bij de bovenkant van de code te wijzigen:

**Agentic bot list**

Wijzig de array `AGENTIC_BOTS` om gebruikersagents toe te voegen of te verwijderen:

```javascript
const AGENTIC_BOTS = [
  'AdobeEdgeOptimize-AI',
  'ChatGPT-User',
  'GPTBot',
  'OAI-SearchBot',
  'PerplexityBot',
  'Perplexity-User',
  // Add additional user agents as needed
  'ClaudeBot',
  'Anthropic-AI'
];
```

**gerichte wegen**

Standaard worden alle HTML-pagina&#39;s gerouteerd naar Edge Optimize. Als u het routeren wilt beperken tot specifieke paden, wijzigt u de array `TARGETED_PATHS` :

```javascript
// Route all HTML pages (default)
const TARGETED_PATHS = null;

// Or specify exact paths to route
const TARGETED_PATHS = ['/', '/page.html', '/products', '/about-us'];
```

**configuratie Failover**

Standaard mislukt de worker op een 4XX- of 5XX-fout in Edge Optimize. Pas dit gedrag aan:

```javascript
// Default: failover on any 4XX or 5XX error
const FAILOVER_ON_4XX = true;
const FAILOVER_ON_5XX = true;

// Failover only on 5XX server errors (not 4XX client errors)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = true;

// Disable automatic failover (not recommended)
const FAILOVER_ON_4XX = false;
const FAILOVER_ON_5XX = false;
```

**Belangrijke overwegingen**

* **gedrag Failover:** De worker ontbreekt automatisch over aan uw oorsprong als Edge optimaliseert om het even welke fout (4XX of 5XX statuscodes) terugkeert of als het verzoek wegens een netwerkfout ontbreekt. Failover gebruikt `EDGE_OPTIMIZE_TARGET_HOST` als het oorspronkelijke domein (vergelijkbaar met het `F_Default_Origin` of CloudFront `Default_Origin` van Fastly). De antwoorden van Failover omvatten de `x-edgeoptimize-fo: 1` kopbal, die u voor controle en het zuiveren kunt gebruiken.

* **Caching:** de geheime voorgeheugenreacties van de Wolk die op URL door gebrek worden gebaseerd. Omdat het agentische verkeer verschillende inhoud dan menselijk verkeer ontvangt, zorg uw rekeningen van de geheim voorgeheugenconfiguratie voor dit voor. U kunt de cache-API of cachekoppen gebruiken om de cacheinhoud te onderscheiden. De header `x-edgeoptimize-config` moet in de cachemoets worden opgenomen.

* **het Beperken van het Tarief:** monitor uw Edge optimaliseert gebruik en overweegt het uitvoeren van tarief dat voor agentic verkeer indien nodig beperkt.

* **het Testen:** test altijd de configuratie in een het opvoeren milieu alvorens aan productie op te stellen. Verifieer dat zowel agentisch als menselijk verkeer zich zoals verwacht gedragen. Het gedrag van de failover van de test door Edge te simuleren optimaliseert fouten.

* **Logging:** laat het registreren van de Werknemers van de Wolk toe Cloudflare om verzoeken te controleren en kwesties problemen op te lossen. Navigeer aan **Arbeiders** > **uw arbeider** > **Logboeken** om logboeken in real time te bekijken. De worker registreert failover-gebeurtenissen voor foutopsporingsdoeleinden.

**Problemen oplossen**

| Probleem | Mogelijke oorzaak | Oplossing |
|-------|----------------|----------|
| Geen `x-edgeoptimize-request-id` header in reactie | De route van de arbeider niet, of gebruikersagent niet in de agentic bots lijst. | Verifieer uw routepatroon de verzoek URL aanpast. Controleer of de gebruikersagent zich in de array `AGENTIC_BOTS` bevindt. |
| 401 of 403 fouten van Edge Optimize | Ongeldige of ontbrekende API-sleutel. | Controleer of `EDGE_OPTIMIZE_API_KEY` correct is ingesteld in omgevingsvariabelen. Neem contact op met Adobe om te bevestigen dat uw API-sleutel actief is. |
| Oneindige omleidingen of lussen | Koptekst voor lusbeveiliging wordt niet op de juiste wijze ingesteld of gecontroleerd. | Controleer of de `x-edgeoptimize-request` -headercontrole is uitgevoerd. |
| Beïnvloed menselijk verkeer | Worker die logica verplettert is te breed. | Verifieer de gebruikersagent passende logica correct en case-insensitive is. Controleer of `TARGETED_PATHS` correct is geconfigureerd. |
| Trage responstijden | Netwerkvertraging naar Edge Optimize backend. | Dit wordt verwacht voor het eerste verzoek; volgende aanvragen worden in de cache geplaatst bij Edge Optimize. |
| `x-edgeoptimize-fo: 1` header in reactie | Edge Optimize heeft een fout en failover naar de oorsprong geretourneerd. | Controleer de logboeken van de Werknemers van de Wolk voor de specifieke foutencode. Controleer de servicestatus Edge Optimize met Adobe. |
| Failover werkt niet | De vlaggen van Failover gehandicapt, of fout in failoverlogica. | Verifiëren `FAILOVER_ON_4XX` en `FAILOVER_ON_5XX` worden ingesteld op `true` . Controleren of workers zich aanmelden voor foutberichten. |
| Bepaalde paden zijn niet geoptimaliseerd | Pad komt niet overeen met het doelpad of het HTML-paginapatroon. | Controleer of het pad zich in `TARGETED_PATHS` (indien opgegeven) bevindt en of het overeenkomt met het HTML-pagina regex-patroon. |
| Verzoeken mislukken met ongeldige host | `EDGE_OPTIMIZE_TARGET_HOST` bevat een protocol (bijvoorbeeld `https://` ). | Gebruik alleen de domeinnaam zonder protocol (bijvoorbeeld `example.com` en niet `https://example.com` ). |
| 530-fout tijdens failover | Cloudflare kan geen verbinding maken met de oorsprong of failover-aanvraag heeft ongeldige headers. | Controleer of de functie failover de koppen voor Edge Optimize verwijdert. Verifieer uw oorsprong toegankelijk is en DNS correct wordt gevormd. |

{{verify-setup-byocdn}}

{{return-to-overview}}
