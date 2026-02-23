---
title: Klantconfiguratie
description: Gebruik de configuratie van de klant om te bepalen hoe uw merk binnen het optimaliseringsplatform LLM wordt gecontroleerd en geanalyseerd.
feature: Customer Configuration
source-git-commit: 3fab5f21311a741e51e7a31cd3a26de79fcbff95
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 0%

---


# Klantconfiguratie {#customer-configuration}

Het Klantconfiguratiedashboard is een krachtig hulpmiddel dat inzicht biedt in de zichtbaarheid van uw merk in LLM&#39;s. Door categorieën, onderwerpen en herinneringen correct op te zetten, kunt u ervoor zorgen dat uw merk goed gepositioneerd is om in LLM-Gegenereerde reacties te verschijnen. Deze opstelling verzekert het platform inzicht in uw bedrijfscontext, toelatend nauwkeurige zicht, verkeer, en opportuniteitsanalyse.

![&#x200B; Dashboard van de Configuratie van de Klant &#x200B;](/help/dashboards/assets/customer-config.png)

Als u wilt configureren hoe LLM Optimizer uw aanwezigheid van uw merk controleert en analyseert op verschillende markten en in concurrerende landschappen, hebt u toegang tot de volgende tabbladen:

* [Vragen](#prompts-brand)
* [Categorieën](#categories)
* [Andere merken](#other-brands)
* [Merkaliassen](#brand-aliases)
* [CDN-configuratie](#agentic-cdn)
* [Google-zoekconsole](#google-console)

>[!IMPORTANT]
>
> Voor meer details op hoe te opstelling zien uw categorieën, onderwerpen, herinneringen de [&#x200B; Beste praktijken voor het vormen van categorieën, onderwerpen, herinneringen &#x200B;](/help/overview/best-practices-topics-prompts.md) pagina.

## Vragen {#prompts-brand}

Op dit tabblad kunt u vragen controleren, beheren en aanpassen. U kunt de analyse van de Aanwezigheid van het a [&#x200B; &#x200B;](/help/dashboards/brand-presence.md) .csv uploaden en de lijst zal met herinneringen en onderwerpen van die analyse worden bevolkt of [&#x200B; download een Bibliotheek van Vragen &#x200B;](/help/overview/best-practices-topics-prompts.md) die door Adobe wordt gecreeerd. U kunt onderwerpen en hun bijbehorende herinneringen ook schrappen wijzigen en toevoegen zoals nodig.

Als u een CSV-bestand met gegevensinzichten wilt importeren, moet u eerst een bestand exporteren vanaf het dashboard Handaanwezigheid. Zie de [&#x200B; gegevensinzichten &#x200B;](/help/dashboards/brand-presence.md#data-insights) sectie leren hoe te om dat te doen. Zodra u het bestand hebt:

1. Op het dashboard, klik **uploadt CSV**.
2. In het venster Gegevens importeren sleept u het bestand en zet u het neer of kiest u het bestand handmatig.
3. Klik **uploadt Gegevens**.

U kunt een nieuw Csv- dossier ook tot stand brengen door het malplaatje van het **venster van de Inzichten van Gegevens van de Invoer** te downloaden. Zodra u het malplaatje hebt, open het en input uw onderwerpen samen met hun bijbehorende herinneringen, categorieën, en gebieden elk in een nieuwe lijn.

Om te leren hoe te om de Bibliotheek van de Vragen van de Industrie te downloaden en te gebruiken die door Adobe wordt gecreeerd zie de sectie van de Bibliotheek van de Vragen van de Industrie op [&#x200B; deze pagina &#x200B;](/help/overview/best-practices-topics-prompts.md)

Bovendien kunt u onderwerpen/herinneringen aan de lijst onafhankelijk van een Csv- dossier of snelle bibliotheek ook toevoegen. Hiervoor moet u op het dashboard:

1. Klik **toevoegen Onderwerp** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Voer de onderwerpnaam in.
4. Voeg de snelle tekst toe.
5. Selecteer het gebied.
6. Klik **toevoegen Vragen** en het onderwerp met de herinnering zal op de lijst verschijnen.

>[!NOTE]
>Nieuw toegevoegde herinneringen zullen niet in MerkAanwezigheid verschijnen tot de verwerking volledig is.

Voor de lijst, kunt u elk onderwerp klikken en de bijbehorende herinnering(en) zullen verschijnen, om het onderwerp en zijn bijbehorende herinneringen te schrappen, klik het schrappingspictogram van de lijst.

## Categorieën {#categories}

Vanuit het tabblad Categorieën kunt u bedrijfscategorieën of productlijnen definiëren die u wilt bijhouden en deze aan specifieke gebieden koppelen. Over het geheel genomen heeft het tabblad Categorieën betrekking op bijna elke andere aanpassing op deze pagina, omdat categorieën in het categorieveld worden weergegeven voor de andere aanpassingen (andere bijhouden, aliassen enzovoort). Een nieuwe categorie toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, voeg de **Naam van de Categorie** toe.
3. Pas het **Verwante Gebied** aan waar de categorie zal worden gecontroleerd.
4. Klik **sparen** en de nieuwe categorie zal op de categorielijst verschijnen.

Het toevoegen van nieuwe categorieën zal automatisch geen onderwerpen en herinneringen produceren - deze zullen manueel van de [&#x200B; Inzichten van Gegevens &#x200B;](#data-insights) tabel moeten worden toegevoegd.

Als u een categorie wilt verwijderen, klikt u op het pictogram Verwijderen in de categorielijst. Wees voorzichtig, omdat **het schrappen van een categorie ook de bijbehorende punten** als merkaliassen zal schrappen die met die specifieke categorie verbonden zijn.

## Andere merken {#others-tracking}

Op dit tabblad kunt u bijhouden hoe uw andere namen worden vermeld ten opzichte van uw merk in verschillende categorieën en regio&#39;s. Controleer hun aanwezigheid en prestaties in uw marktsegmenten. Tekstspatiëring aanpassen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Voeg de naam van de ander toe.
4. Pas indien nodig de andere alias en domeinen aan.
5. Klik **sparen**.

Als u een item uit de lijst wilt verwijderen, klikt u op het pictogram Verwijderen.

## Merkaliassen {#brand-aliases}

Door merkaliassen te gebruiken, kunt u alternatieve namen en variaties van uw merk vormen die over verschillende categorieën en gebieden zouden moeten worden gevolgd. Dit zorgt voor een uitgebreide controle op alle merkvermeldingen. Een merkalias toevoegen:

1. Klik **toevoegen** knoop.
2. In het nieuwe configuratievenster, selecteer de **Categorie**. Eerder gemaakte categorieën worden hier weergegeven.
3. Selecteer het **Gebied** waar alias zal worden gecontroleerd.
4. Voeg de merkalias toe.
5. Klik **sparen** en merkalias zal op de lijst verschijnen.

Om een merkalias te schrappen, klik het **Schrapping** pictogram van de alias lijst.

## CDN-configuratie {#cdn-configuration}

Vanuit dit tabblad kunt u uw CDN-streams configureren, zodat Adobe LLM Optimizer uw CDN-gegevens kan analyseren. Deze gegevens worden gebruikt om dashboards (zoals het Verkeer van de Agentica), die inzicht in verkeerspatronen, prestatiesmetriek, en optimaliseringskansen verstrekken te aandrijven. Aan boord van uw leverancier CDN, klik **Op boord CDN**.

![&#x200B; Klantenconfiguratie CDN &#x200B;](/help/overview/assets/cc-cdn.png)

Op het **Aan boord CDN Providervenster**:

1. Selecteer uw CDN-provider.
2. Klik **Onboard** om logboek toe te laten door:sturen.

Als u **Andere** selecteert, zult u uit aan llmo-now@adobe.com voor hulp moeten bereiken.

## Google-zoekconsole {#google-console}

Met Adobe LLM Optimizer kunt u uw Google Search Console-account integreren, zodat echte zoekopdrachten rechtstreeks in de interface worden geplaatst. Door te surfen op echte vragen van Google Search Console, kunt u snelle reeksen bouwen die in daadwerkelijke onderzoeksgedrag en high-intent ontdekkingspatronen worden gegrond. Hierdoor kunt u op basis van bewezen vraag voorrang geven aan vragen en LLM-optimalisatie-inspanningen afstemmen op de manier waarop gebruikers momenteel zoeken. Bovendien, blijft u in volledige controle omdat de vragen nooit automatisch worden toegevoegd en uitdrukkelijk moeten worden geselecteerd alvorens actieve herinneringen te worden.

### Hoe werkt het {#how-it-works}

Het belangrijkste ding om over de integratie tussen LLM Optimizer met de Console van het Onderzoek van Google te herinneren is het volgende: in plaats van manueel te veronderstellen welke klanten een AI medewerker zouden kunnen vragen, bekijken wij wat zij **reeds** zoeken en die echte vragen omzetten in natuurlijke, gespreksherinneringen. Dit proces om van onderzoeksvragen aan AI herinneringen over te gaan wordt geïllustreerd in het diagram hieronder.

![&#x200B; Stroom van het Proces &#x200B;](/help/dashboards/assets/diagram-flow.png)

In het algemeen bestaat het proces uit vijf stappen:

#### Stap 1 — Verzamel uw echte onderzoeksgegevens {#gsc-one}

Het proces begint met de trefwoorden die uw publiek daadwerkelijk gebruikt wanneer het uw website via Google vindt. Deze ruwe dataset (vaak duizenden unieke vragen) is de stichting voor alles dat volgt.

#### Stap 2 — De betekenis en het filter voor de veiligheid analyseren {#gsc-two}

Elke query wordt geanalyseerd op semantische betekenis (waar de gebruiker echt om vraagt) en gerasterd door een veiligheidsfilter dat onjuiste of niet-merkinhoud verwijdert. Hierdoor worden alleen schone, relevante trefwoorden vooruit gezet.

#### Stap 3 — Groeperen in categorieën en onderwerpen {#gsc-three}

De verwante vragen worden automatisch gegroepeerd in **categorieën** (brede bedrijfsthema&#39;s) en **onderwerpen** (geconcentreerde subtopics binnen elke categorie). Het systeem geeft prioriteit aan categorieën die al zijn geconfigureerd in uw LLM Optimizer-configuratie. Bovendien kan het ook nieuwe categorieën weergeven die uw zoekgegevens onthullen, maar worden deze nog niet gecontroleerd. Het volgende diagram is een voorbeeld van categorieën en onderwerpen voor een meubelmerk:

![&#x200B; Meubelmerk van Meubilair &#x200B;](/help/dashboards/assets/diagram-example.png)

#### Stap 4 — Genereer herinneringen die in echte sleutelwoorden worden gegrond {#gsc-four}

Voor elk onderwerp, produceert het systeem herinneringen die aan gelijkaardig zijn hoe de echte mensen met medewerkers AI spreken. Elke vraag wordt rechtstreeks beïnvloed door eigenlijke zoektrefwoorden uit uw Google Search Console, waardoor trefwoordintentie wordt omgezet in natuurlijke gespreksvragen.

Deze aanpak (geaard in trefwoorden) betekent:

* Prompts weerspiegelen de reële vraag, niet hypothetische vragen.
* De taal weerspiegelt hoe uw klanten dingen eigenlijk formuleren.
* Dekking omvat de volledige breedte van wat mensen zoeken op uw site.

De snelle generatie houdt ook rekening met uw merkprofiel — inclusief producten, concurrenten, de positie van de industrie en het doelpubliek — om ervoor te zorgen dat de aanwijzingen contextafhankelijk correct zijn.

#### Stap 5 - Kwaliteitsborging en -levering {#gsc-five}

Vóór levering, gaat elke herinnering door verscheidene geautomatiseerde kwaliteitscontroles:

* Deduplicatie — bijna identieke aanwijzingen worden verwijderd.
* Balansverhouding branding — zorgt voor een realistische mix (~75% zonder branding, ~25% branded).
* Taalkwaliteit — strips robotische frasering veroorzaakt natuurlijk geluid.
* Consistentiecontroles — valideert datums, verwijdert vulzinnen en zorgt voor een korte lengte.

Bovendien, wordt elke herinnering geëtiketteerd met zijn categorie, onderwerp, intenttype, en branded/unbranded classificatie, klaar voor LLM Optimizer beginnen controle.

#### Vragen om anatomie {#prompt-anatomy}

Nadat het bovenstaande proces is voltooid, heeft elke vraag die aan LLM Optimizer wordt geleverd de volgende kenmerken:

| Veld | Beschrijving |
|---------|----------|
| Tekst | De herinnering, gelijkend op hoe een gebruiker het in een AI medewerker zou typen |
| Categorie | Het brede bedrijfsthema dat aan deze herinnering wordt toegewezen. |
| Onderwerp | Het specifieke subonderwerp binnen de categorie. |
| Regio | De doelmarkt (bijvoorbeeld de VS, het Verenigd Koninkrijk, enzovoort). |
| Intentie | De gebruikersidee: informatie, vergelijkend, transactie, instructies, planning, of delegatie. |
| Type | Het type kan van merknaam (het merk/de producten) of zonder merknaam (de generieke vraag van de industrie) worden genoemd. |

### Hoe wordt het gebruikt {#how-to-use}

Volg de onderstaande stappen om de zoekconsolequery&#39;s van Google te integreren en te gebruiken met LLM Optimizer.

#### Verbinding maken met de Google-zoekconsole {#connect-console}

Voordat u deze functie kunt gebruiken, moet u uw Google Search Console-account integreren met LLM optimizer.

1. Open het dashboard Configuratie van de Klant.
1. Navigeer aan het lusje van de Console van het Onderzoek van Google en klik **Connect Rekening**.
   ![&#x200B; Google de Console van het Onderzoek &#x200B;](/help/dashboards/assets/google-console.png)
1. Meld u aan met een Google-account dat toegang heeft tot de gewenste eigenschap voor de zoekconsole.
   ![&#x200B; Google- Rekening &#x200B;](/help/dashboards/assets/google-account.png)
1. Kies de eigenschap waarmee u verbinding wilt maken.
   ![&#x200B; het Bezit van de Console &#x200B;](/help/dashboards/assets/console-property.png)
1. Nadat de verbinding is voltooid, begint LLM Optimizer relevante zoekopdrachten op te halen.
   ![&#x200B; het Ophalen Gegevens &#x200B;](/help/dashboards/assets/console-complete.png)

#### Zoekopdrachten controleren en doorzoeken {#search-query}

Nadat u het Google-account voor de zoekconsole hebt geïntegreerd met LLM-optimalisator, kunt u de lijst met onderwerpen en vragen die zijn opgehaald vanuit de zoekconsole bekijken en de aanwijzingen toevoegen uit de lijst.

1. Controleer op het tabblad Zoekconsole van Google de lijst met onderwerpen en vragen die u hebt opgehaald uit de zoekconsole.
   ![&#x200B; Prompts Lijst &#x200B;](/help/dashboards/assets/prompts-list.png)
1. Klik op het gewenste onderwerp/de vraagcategorie om de lijst uit te breiden.
1. Gebruik **toevoegen** knoop om herinneringen van de lijst toe te voegen. U kunt ook bulksgewijs herinneringen en categorieën toevoegen door **te gebruiken voeg allen** toe.
   ![&#x200B; voeg Herinneringen &#x200B;](/help/dashboards/assets/add-prompts.png) toe
1. Zodra u met de selectie wordt tevredengesteld, klik **sparen** op het berichtbericht.

#### Toegevoegde query&#39;s weergeven in de lijst met vragen {#prompts-list}

Nadat een vraag wordt toegevoegd, verschijnt het in het [&#x200B; Prompts &#x200B;](#prompts-brand) lusje binnen het dashboard van de Configuratie van de Klant. De herinneringen die van de Console van het Onderzoek van Google worden betrokken zijn duidelijk met een pictogram van de Console van het Onderzoek van Google in de **kolom van de Oorsprong**. Met dit pictogram kunt u een onderscheid maken tussen aanwijzingen die in het werkelijke zoekgedrag van de gebruiker zijn geaard en de aanwijzingen die handmatig of vanuit andere bronnen zijn toegevoegd.

### Veelgestelde vragen {#gsc-faq}

V: Hoe vaak worden berichten bijgewerkt op het dashboard van de Google-zoekconsole?

Vragen die afkomstig zijn uit de Google Search Console worden meestal één keer per maand vernieuwd. Elke vernieuwt trekt de recentste gegevens van de onderzoeksvraag van uw Console van het Onderzoek van Google, stelt de generatiepijplijn opnieuw in werking, en werkt uw vraagreeks bij. Zo blijven uw aanwijzingen op de huidige zoektrends en seizoensverschuivingen in het gebruikersgedrag afgestemd.

V: Hoeveel herinneringen worden gewoonlijk afkomstig uit de Google Search Console?

Het aantal hangt van de grootte van uw plaatsing en het aantal getraceerde categorieën af. Bijvoorbeeld:

| Categorieën | Totaal aantal onderwerpen | Opgeleverde vragen |
|---------|----------|----------|
| 1-2 | 3-8 | ~65-180 |
| 4-5 | 12-20 | ~270-450 |
| 10 | 30-40 | ~675-900 |

Wij streven ernaar snelle reeksen te leveren die voldoen aan de kwaliteitsdoelstellingen die tijdens proef en aan boord worden meegedeeld: minstens 20 herinneringen per onderwerp, met 3-4 onderwerpen per categorie, en een gezonde branded/zonder merknaam balans.

V: Hoe snel zal ik de berichten zien die afkomstig zijn van de Google Search Console nadat ik verbinding heb gemaakt met de Google Search Console?

De herinneringen zijn typisch beschikbaar **binnen een paar uren** nadat uw verbinding van de Console van het Onderzoek van Google wordt gevestigd. De pijpleiding trekt automatisch uw onderzoeksgegevens, verwerkt het door de generatie en de stappen van de kwaliteitsverzekering en levert de definitieve herinnering die aan LLM Optimizer wordt geplaatst.

V: Wie kan verbinding maken met de Google Search Console?

Iedereen met **Eigenaar** of **Volledige Toestemming** op het bezit van de Console van het Onderzoek van Google kan de verbinding machtigen. Dit zijn de toestemmingsniveaus die lees toegang tot onderzoeksvraaggegevens verlenen. Als u over uw toestemmingsniveau onzeker bent, kunt u het controleren onder **Montages>Gebruikers** en toestemmingen in uw Console van het Onderzoek van Google.

Q: Kan ik herinneringen als genegeerd of overgeslagen merken zodat ik niet hen in de de herinneringenlijst van de Console van het Onderzoek van Google zie?

Ja, u kunt om het even welke herinnering schrappen u niet wilt controleren. Verwijderde herinneringen worden verwijderd uit uw actieve vraaglijst en zullen niet in toekomstige rapportering verschijnen. Als een verwijderde herinnering opnieuw wordt gegenereerd in een volgende maandelijkse vernieuwing, kunt u deze opnieuw verwijderen.

V: Zodra ik herinneringen van de Console van het Onderzoek van Google aan mijn herinneringslijst toevoegt, hoe snel zal ik merkaanwezigheidsgegevens voor die herinneringen zien?

De gegevens van de Aanwezigheid van het merk voor onlangs toegevoegde herinneringen zullen tijdens de volgende geplande gegevens verschijnen verfrissen zich, die typisch aan het begin van elke week loopt. Afhankelijk van het tijdstip waarop u de aanwijzingen toevoegt, ziet u de resultaten binnen een paar dagen.
