---
source-git-commit: da789100d814004687de2f46e18a295671dec4b8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---
# Fragmenten

## Ophaalstappen voor API-sleutel {#retrieve-byocdn-api-key}

**Stappen om uw productie Edge terug te winnen optimaliseren API sleutel:**

1. In LLM Optimizer, open **configuratie van de Klant** en selecteer de **CDN configuratie** tabel.

   ![&#x200B; ga aan de Configuratie van de Klant &#x200B;](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Bepaal de plaats van **optimalisaties aan AI agenten** sectie. Tik **toelaten optimaliseringsmotor** checkbox.

   ![&#x200B; stelt optimalisaties aan AI agenten op — hangende &#x200B;](/help/assets/optimize-at-edge/byocdn-deploy-optimizations-pending.png)

3. In de bevestigingsdialoog, laat de uitgezochte **&#x200B;**&#x200B;toe.

   ![&#x200B; laat de bevestigingsdialoog van de optimaliseringsmotor &#x200B;](/help/assets/optimize-at-edge/byocdn-enable-optimization-engine-dialog.png) toe

4. Selecteer **details van de Mening**. In **stel optimaliseringsdetails** dialoog op, kopieer de **productie API sleutel** (gebruik **Exemplaar** naast het gebied).

   ![&#x200B; de sleutel van productie API in stelt optimalisatiedetails &#x200B;](/help/assets/optimize-at-edge/byocdn-production-api-key-details.png) op

   >[!NOTE]
   >Uit het dialoogvenster kan blijken dat de installatie niet is voltooid. Dit wordt verwacht tot het verpletteren wordt geverifieerd — u kunt nog de API sleutel kopiëren zodat kan uw team van IT of CDN de configuratie beëindigen.

Als u bovendien hulp nodig hebt bij de bovenstaande stappen, neemt u contact op met uw Adobe-accountteam of `llmo-at-edge@adobe.com` .

## Domein-API-sleutel opslaan (optioneel) {#retrieve-staging-edge-optimize-api-key}

Gebruik het opvoeren hostname wanneer u Optimize bij Edge in een lagere milieu wilt testen alvorens het productieverkeer de verpletterende regels gebruikt.

**Eerste vereisten**

* Het opvoeren hostname moet tot het **zelfde registreerbare domein** behoren zoals uw productiesite (bijvoorbeeld, `https://staging.example.com` wanneer de productie `https://www.example.com` is).
* Slechts **één** het opvoeren domein kan voor de plaats worden gevormd. Nadat het wordt bewaard, kan het niet zonder hulp worden veranderd.

**Stappen**

1. In LLM Optimizer, open **configuratie van de Klant** en selecteer de **CDN configuratie** tabel.

2. In **stel optimalisaties aan AI agenten** sectie op, uitgezocht **voeg werkgebieddomein** toe (of **domein van het Stadium** als een het opvoeren domein reeds wordt gevormd).

3. In de **dialoog van het Domein 0&rbrace; van het Stadium &lbrace;, ga volledige het opvoeren URL met inbegrip van `https://` in en selecteer** Vastgesteld Domein **.**

   ![&#x200B; de inputdialoog van het Domein van het Stadium &#x200B;](/help/assets/optimize-at-edge/byocdn-staging-domain-input.png)

4. Bevestig het domein in de volgende herinnering. Wanneer het werkschema voltooit, toont de **dialoog van de Domeinen van het 0&rbrace; Stadium het gevormde domein en zijn** API sleutel **.** Selecteer **Exemplaar** om de het opvoeren API sleutel te kopiëren.

   ![&#x200B; het Staging domein API sleutel &#x200B;](/help/assets/optimize-at-edge/byocdn-staging-domain-api-key.png)

Neem contact op met `llmo-at-edge@adobe.com` als u hulp nodig hebt.

## De verpletterende status van de controle in LLM Optimizer {#verify-routing-status-in-ui}

De status van het verkeer dat verplettert kan ook in LLM Optimizer UI worden gecontroleerd. Navigeer aan **configuratie van de Klant** en selecteer de **CDN configuratie** tabel.

![&#x200B; stelt optimalisaties aan AI agenten op — voltooide &#x200B;](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Terug naar overzicht {#return-to-overview}

Meer leren over Optimaliseren bij Edge, met inbegrip van beschikbare kansen, auto-optimaliseringswerkschema&#39;s, en FAQs, terugkeer aan [&#x200B; optimaliseren bij het overzicht van Edge &#x200B;](/help/dashboards/optimize-at-edge/overview.md).
