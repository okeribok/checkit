# Checkit – Ontwikkel- en onderhoudsbriefing

## Doel en positionering

Checkit is een **lichtgewicht, open-source hulpmiddel voor kwaliteitscontrole van formele documenten (authoritatief vs tentatief)**.

Het ondersteunt medewerkers bij het controleren van:

-   RFP’s ↔ eisenlijsten
-   inschrijvingen ↔ RFP-compleetheid
-   beleid ↔ wet- en regelgeving
-   documenten ↔ interne consistentie

De kern is eenvoudig:

> Checkit helpt mensen vollediger en consistenter te controleren.  
> Het neemt het denkwerk niet over.

Het systeem is dus **een assistent, geen auteur of beslisser**.  
Vergelijk het met spellingscontrole of static analysis: het signaleert, de mens beslist.

----------

## Ontwerpfilosofie

Checkit optimaliseert niet voor “maximale intelligentie”, maar voor:

-   betrouwbaarheid
-   uitlegbaarheid
-   lage variatie
-   lage kosten
-   lokale inzetbaarheid
-   menselijke vaardigheidsopbouw

In deze context levert een groter model niet automatisch meer waarde. Grote foundation modellen zijn duurder, minder voorspelbaar, juridisch lastiger (data/soevereiniteit) en moeilijk uitlegbaar.

Voor kwaliteitscontrole in de publieke sector zijn **determinisme en auditbaarheid belangrijker dan cognitieve kracht**.

Daarom geldt:

> structuur en regels eerst, AI alleen waar nodig.

----------

## Kernprincipes (leidend voor alle keuzes)

### 1. Structuur vóór AI

Eerst:

-   headings en secties
-   requirement-ID’s
-   vaste patronen
-   deterministische matching

Pas daarna:

-   lichte semantische matching via kleine lokale modellen

AI is ondersteunend, nooit leidend.

----------

### 2. Assisterend, niet generatief

Het systeem:

-   toont hiaten
-   laat dekking zien
-   signaleert inconsistenties
-   legt uit waarom

Het systeem:

-   schrijft geen teksten
-   herformuleert niet automatisch
-   neemt geen besluiten

Doel: gebruikers sterker maken, niet afhankelijk.

----------

### 3. Lokaal en edge-first

Checkit moet:

-   offline kunnen werken
-   lokaal of on-prem draaien
-   geen externe API’s vereisen
-   data binnen de machine houden

Beoogde richting:

-   lokale inference via Fietsbel platform met Llama.cpp, bitnet.cpp:
    (grammar, logit bias, mirostat, LoRA, meerdere modellen)

Parsing-verbeteringen:

-   mogelijke overstap van naar wanneer compatibel

Kleine modellen (±3B) hebben de voorkeur vanwege:

-   snelheid
-   lage kosten
-   reproduceerbaarheid
-   privacy
-   eenvoud van deployment

----------

### 4. Deterministisch en uitlegbaar

Zelfde input → zelfde output.

Elke bevinding moet verklaarbaar zijn, bijvoorbeeld: “Requirement 4.2 komt niet voor in sectie B”.

Geen black-box scores of stochastische resultaten.

----------

### 5. Graceful degradation

Zonder model moet het systeem nog steeds nuttig zijn.  
AI is een verbetering, geen vereiste.

----------

### 6. Menselijke correctie en feedback zijn leidend

Checkit bevat een expliciete feedbacklus.

Gebruikers kunnen:

-   bevinding goed-/afkeuren (duimpje)
-   opmerking toevoegen
-   context automatisch meesturen

Feedback wordt (instelbaar) verzonden naar een beveiligde mailbox of intern systeem.

Doelen:

1.  verbetering van regels en modellen
2.  reductie van false positives
3.  continue kwaliteitsmetingen
4.  aanscherping van schrijf- en structuurrichtlijnen voor bron­documenten

Hiermee leert niet alleen de tool, maar ook de organisatie.

Het systeem blijft volledig FOSS en edge: geen externe datadeling vereist.

----------

## Wat Checkit oplevert (succescriteria)

Succes wordt niet primair gemeten in tijdswinst.

Belangrijker zijn:

-   minder gemiste eisen
-   minder herwerk
-   minder reviewrondes
-   minder kwaliteitsverschillen tussen medewerkers
-   hogere consistentie
-   meer vertrouwen
-   lagere coördinatielast

Het doel is stabielere kwaliteit en minder variatie.

----------

## Functionele roadmap

### Fase 1 – Deterministische basis

-   feedbackmechanisme (duimpjes + comment via email)
- optioneel docling 258 ipv pdf.js
- granite 4 (zowel 1b als micro) ipv granite 3
- iteratief verbeteren met feitelijke use cases
- heading-gebaseerde chunking
-   requirement ↔ sectie matching
-   dekkingsmatrix / checklist
-   gap-detectie
-   eenvoudige consistentiechecks

### Fase 2 – Lichte AI-ondersteuning

-   semantische matching
-   fuzzy varianten
-   contradictiedetectie

### Fase 3 – Traceability & consistentie

-   interne conflicten
-   definities/termen
-   versie- en bronkoppeling
-   documentgraaf

### Doorlopend

-   feedbackverwerking
-   golden testsets
-   regressietests op nauwkeurigheid

----------

## UX-richtlijnen

-   direct inzicht (< 2 klikken)
-   weinig configuratie
-   visuele dekking (matrix/heatmap)
-   elke melding met uitleg
-   lage foutpositieven
-   geen extra cognitieve belasting

----------

## Governance & randvoorwaarden

-   open source (EUPL)
-   geen vendor lock-in
-   transparante dependencies
-   reproduceerbare builds
-   exporteerbare data
-   audit logs
-   WCAG-toegankelijk
-   lage systeemeisen

----------

## Samenvatting voor ontwikkelaars

Zie Checkit als:

> kwaliteitscontrole en dekkingstool voor documenten

niet als:

> een slimme AI die documenten schrijft of begrijpt.

Bij twijfel tussen “meer AI” of “eenvoudiger en voorspelbaarder”: kies altijd voor eenvoud en determinisme.

Dat levert in deze context structureel meer waarde op.

---

## agentic brief (prompt toevoeging agentic engineering

You are continuing development of **Checkit**: a single-file, offline document coverage tool for Dutch civil servants. It checks whether source documents (e.g. RFP responses, policy drafts) cover the requirements in an authoritative document.

----------

## What this tool IS

A **signal generator**. It shows the human where to look. The human decides what it means.

-   Deterministic first: regex, heading detection, keyword overlap. No variance.
-   AI second: only embeddings (similarity scores), never generative text.
-   The tool must make its users _better_ at document review — not dependent on the tool.

## What this tool is NOT

-   Not a document writer, summariser, or gap fixer.
-   Not a chatbot or assistant interface.
-   Not a cloud service. Not a SaaS. Not a backend.
-   The model must never produce text shown to the user as content. Scores and coverage indicators only.

----------

## Non-negotiables (from the DoD — enforce strictly)

Constraint

Rule

**Offline / zero-trust**

`connect-src 'none'` in CSP. Zero CDN. All deps from `./lib/`. Works at `file:///`.

**Single HTML file**

All app logic in one `.html`. Deps vendored locally.

**Storage**

`localStorage` for settings only (<1KB). IndexedDB for models + session.

**Model management**

Sideloaded from local file picker. `pipeline.dispose()` on unload — verify VRAM drop. "Purge Models" reduces profile to <1MB for MDM sync.

**Code discipline**

Raw ES6+. No TypeScript. No bundler. No minifier on your code. <2500 LoC excluding vendored libs.

**Chapter TOC**

8-chapter structure in `<script type="module">` — see source. Do not reorder.

**Graceful degradation**

App is useful with zero models loaded. Deterministic layer is primary, always.

**No generative output**

The model produces numbers (scores, similarity). Never text the user reads as content.

----------

## What has been built (hand-off state)

-   ✅ CSP meta tag (`connect-src 'none'`)
-   ✅ 8-chapter structure with Table of Contents
-   ✅ IndexedDB layer (models + session stores)
-   ✅ Model sideload: file picker → ArrayBuffer → IndexedDB
-   ✅ Model activate / unload / delete / purge (with dispose stub)
-   ✅ Crash-only state persistence (5s autosave, boot recovery)
-   ✅ i18n NL/EN dictionary with live toggle
-   ✅ PDF.js integration (graceful TXT fallback if `./lib/pdf.min.js` absent)
-   ✅ Section extraction (heading-based chunking)
-   ✅ Requirement extraction (ID patterns + obligation words NL/EN)
-   ✅ Deterministic coverage match (keyword overlap, pure function)
-   ✅ Results UI: requirement sidebar + coverage detail panel

**Chapter 6 (AI Inference) is a skeleton with stubs and constraints documented inline.**

----------

## What comes next (backlog order)

1.  **`./lib/` vendor setup** — pin and download `pdf.min.js` + `pdf.worker.min.js` (3.11.174)
2.  **Docling 258M integration** — replace pdf.js text extraction with structural section/heading output; update `extractSections()` to consume Docling output
3.  **Granite 258M Embedding** — implement Chapter 6: load model from IDB → transformers.js pipeline (from `./lib/transformers.min.js`); `embedText()` + cosine rank; `disposeInferencePipeline()` with verified VRAM release
4.  **Heatmap / Coverage Matrix** — visual grid: requirements × sections, cell colour by match strength
5.  **CSV Export** — one-click download of findings matrix
6.  **Feedback loop** — thumbs up/down + comment per finding, dispatch to configurable mailbox/endpoint

----------

## Orientation tips

-   Read the TOC at the top of `<script type="module">` before touching anything.
-   Chapters 5 & 6 contain **pure functions** (input → output, no side effects). Keep them that way.
-   Mutation only happens in Chapters 7 & 8 via the `APP` state object.
-   When in doubt between "more AI" and "simpler + more predictable": choose simpler. That is not a compromise — it is the design.
-   If a feature requires generative model output visible to the user: it is out of scope. Full stop.
