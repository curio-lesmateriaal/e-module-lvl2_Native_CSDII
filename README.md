# E-module Template

Een startpunt voor interactieve e-modules, gebouwd met [`curio-team/e-module-builder`](https://github.com/curio-team/e-module-builder).

Dit template bevat een volledig uitgewerkt voorbeeld over **CSS Grid**
in de `content/` map. Verwijder of vervang die inhoud om je eigen module
te maken.

## Snel starten

1. Gebruik dit repository als template (klik **Use this template** op GitHub).
    * Kies de [`curio-lesmateriaal` organisatie](https://github.com/curio-lesmateriaal)
    als eigenaar.
    * Kies een naam als: `e-module-lvl{level}_p{periode}_{Naam}`, bijv.: `e-module-lvl1_p2_Inlogsystemen`.

2. Deze e-modules werken met GitHub Pages. Ga in de instellingen van je nieuwe
    repository naar **Settings → Pages** en stel de **Source** in op **GitHub Actions**.

> [!NOTE]
> De eerste GitHub workflow run zal falen, omdat GitHub Pages nog niet is ingesteld.

3. Installeer de afhankelijkheden:

   ```bash
   npm install
   npm run dev
   ```

4. Open [http://localhost:5173](http://localhost:5173) in je browser.

5. Pas de inhoud in de `content/` map aan — zie [Content bewerken](#content-bewerken).

6. Als laatste stap is het netjes om de README aan te passen. Haal alles omtrent de template weg en leg kort uit waar de e-module over gaat.

## E-module schrijven met AI

Zodra je repository klaarstaat, kun je een AI-agent (zoals Claude Code, GitHub Copilot of Cursor) de `content/` map laten vullen. Voeg je bronbestanden toe aan de repository (of sleep ze in de chat) en gebruik een van de onderstaande prompts als startpunt. Pas de cursieve onderdelen aan voor jouw situatie.

> [!TIP]
> Gebruik bij voorkeur de **Plan Mode** van de AI-agent voordat deze aan het werk gaat. In Plan Mode stelt de agent eerst een plan op dat jij kunt controleren en bijsturen — zonder dat er al bestanden worden aangemaakt of gewijzigd. In Claude Code schakel je dit in met `/plan`. Zo voorkom je dat de agent een verkeerde richting inslaat die je daarna moet terugdraaien.

### Scenario 1 — Bestaand Word document omzetten (module met weken)

Gebruik dit als je één Word-document hebt met de module-inhoud en dat wilt omzetten naar het e-module formaat met genummerde weken.

> Please help rewrite our current Word document (*lvl1_p2_module_Inlogsystemen_v1.docx*) into our `content/` folder as a **week-based module** for '*Inlogsystemen (in PHP)*', which is a Dutch e-module. The module should be structured into numbered weeks (`week1/`, `week2/`, …), each with at least a `theory.md`. Add `quiz.md`, `assignment.md`, and `exercises/` to a week wherever the source material supports it. The current `content/` is just an example (CSS Grid), which can go. The README explains more on how to write this e-module. The Word document might be missing elements that are required for the e-module — write those. Ensure the e-module works independently. For turning in assignments you may direct to Itslearning, which is where students turn in assignments for feedback by the teacher.

### Scenario 2 — Meerdere bronbestanden samenvoegen (module met weken)

Gebruik dit als je meerdere versies of gerelateerde documenten hebt (bijv. een oud Word-document, een conceptversie, slides of aantekeningen) en daar één nieuwe e-module van wilt maken met genummerde weken.

> Please create a new Dutch e-module for '*Inlogsystemen (in PHP)*' in our `content/` folder. I'm providing multiple source documents: *module_v1.docx (original), module_v2_draft.docx (partial rewrite), slides_week3.pdf*. The current `content/` is just an example (CSS Grid) and can be removed. Use the README for the required file structure and frontmatter fields. Structure the content into numbered weeks (`week1/`, `week2/`, …). Merge the best parts from all sources, resolve any contradictions by keeping the most recent or most complete version, and fill in any gaps required by the e-module format. Every week must have theory; quiz, exercises, and assignment are optional but include them where the source material supports it. Students submit assignments via Itslearning.

### Scenario 3 — Masterclass (één les, geen weken)

Gebruik dit als je een kortere, op zichzelf staande les hebt die geen wekelijkse opdrachten of meetmomenten nodig heeft.

> Please help rewrite our current document (*masterclass_APIs_v1.docx*) into our `content/` folder as a **masterclass** for '*APIs en JSON*', which is a Dutch e-module. A masterclass has no numbered weeks — instead it uses a single arbitrarily named folder (e.g. `masterclass/`) containing only a `theory.md` with `sort: 1` in its frontmatter. There are no quizzes, assignments, exercises, or assessments. The current `content/` is just an example (CSS Grid), which can go. The README explains more on how to write this e-module. Ensure the e-module works independently.

## Commando's

| Commando | Omschrijving |
| --- | --- |
| `npm run dev` | Start de ontwikkelserver op `localhost:5173` |
| `npm run build` | Productie-build naar `dist/` |
| `npm run preview` | Preview van de `dist/` build lokaal |

## Content bewerken

Alleen de `content/` map hoef je te bewerken. De rest wordt automatisch gegenereerd.

```text
content/
  module.md             ← module-metadata (naam, weken, taal, oefenmodus)
  week1/
    theory.md           ← theorie (YAML frontmatter + Markdown)
    quiz.md             ← quiz meetmoment (optioneel)
    assignment.md       ← inleveropdracht (optioneel)
    exercises/          ← oefeningen (optioneel)
      _meta.md          ← oefening-metadata (week, titel, kleur)
      #.md              ← oefening 1, 2, 3, ...
  week2/ … weekN/       ← zelfde structuur; mapnaam bepaalt navigatielabel
  extra/                ← willekeurige map — alleen theory.md vereist (zie hieronder)
    theory.md
  assessments/
    theory-assessment.md      ← meetmoment theorie (optioneel)
    practical-assessment.md   ← meetmoment praktijk (optioneel)
```

### Voorbeelden

#### Modules — duren doorgaans 4 weken

Een module heeft meerdere genummerde weken met theorie, oefeningen, een quiz en een inleveropdracht. De afronding bevat beide meetmomenten, waardoor de navigatie onder **Afronding** een checklist, een theorie-meetmoment én een praktijk-meetmoment toont.

```text
content/
  module.md
  week1/
    theory.md
    quiz.md
    assignment.md
    exercises/
      _meta.md
      1.md
      2.md
  week2/
    theory.md
    quiz.md
    assignment.md
    exercises/
      _meta.md
      1.md
  week3/
    theory.md
    quiz.md
    assignment.md
    exercises/
      _meta.md
      1.md
  week4/
    theory.md
    quiz.md
    assignment.md
    exercises/
      _meta.md
      1.md
  assessments/
    theory-assessment.md
    practical-assessment.md
```

Navigatieresultaat:

```text
Week 1  →  Theorie · Oefeningen · Quiz · Inleveropdracht
Week 2  →  Theorie · Oefeningen · Quiz · Inleveropdracht
Week 3  →  Theorie · Oefeningen · Quiz · Inleveropdracht
Week 4  →  Theorie · Oefeningen · Quiz · Inleveropdracht
Afronding  →  Checklist · Theorie-meetmoment · Praktijk-meetmoment
```

---

#### Masterclass — duurt doorgaans 1 les

Een masterclass bestaat uit één willekeurige map met alleen theorie. Er zijn geen meetmomenten, dus de navigatie toont onder **Afronding** alleen de checklist.

```text
content/
  module.md
  masterclass/
    theory.md    ← bevat sort: 1
    # Optionally you can also still use these components:
    # quiz.md
    # assignment.md
    # exercises/
    #  _meta.md
    #  1.md
```

Navigatieresultaat:

```text
Masterclass  →  Theorie
Afronding    →  Checklist
```

---

### Genummerde secties (`week1`, `week2`, …)

Mappen waarvan de naam overeenkomt met het patroon `<prefix><nummer>` (bijv. `week1`, `mod2`) worden behandeld als **genummerde secties**. Het nummer bepaalt de sorteervolgorde in de navigatie. Het veld `weeks` in `module.md` beperkt hoeveel secties worden verwerkt.

Elke genummerde sectie kan een willekeurige combinatie van `theory.md`, `quiz.md`, `assignment.md` en `exercises/` bevatten. Alleen `theory.md` is verplicht — de andere zijn allemaal optioneel:

* **`quiz.md`** — als afwezig, wordt er geen quizpagina of navigatielink gegenereerd voor die sectie.
* **`assignment.md`** — als afwezig, wordt er geen opdrachtpagina of navigatielink gegenereerd.
* **`exercises/`** — als afwezig, wordt er geen oefeningenpagina of navigatielink gegenereerd.

### Willekeurige secties (`extra/`, `appendix/`, …)

Elke map die **niet** overeenkomt met het `<prefix><nummer>` patroon en een `theory.md` bevat, wordt behandeld als een **willekeurige sectie** (alleen theorie). Deze mappen:

* Verschijnen in de navigatie als een inklapbare groep met één **Theorie**-link.
* Worden gesorteerd ten opzichte van genummerde secties via het veld `sort:` in hun `theory.md` frontmatter (bijv. `sort: 4` plaatst de sectie na week 3).
* Ondersteunen **geen** quiz-, opdracht- of oefeningenpagina's.
* Hebben hun `leeruitkomsten` opgenomen in de Checklist.

```text
content/
  extra/
    theory.md    ← moet sort: <nummer> bevatten om de positie in de nav te bepalen
```

### `content/module.md`

```yaml
---
name: Naam van je module
subtitle: E-module
weeks: 4
language: nl
exerciseMode: interactive   # of: external
description: Korte omschrijving van de module.
youtube: https://www.youtube.com/watch?v=...
youtubeTitle: Crash Course   # optioneel, standaard "Crash Course"
logoAlt: Alternatieve tekst voor het module-logo
algemeen:
  - Ik kan ...
---
```

| Veld | Verplicht | Omschrijving |
| ---- | --------- | ------------ |
| `name` | ja | Naam van de module |
| `weeks` | nee | Hoeveel genummerde secties worden verwerkt. Standaard alle gevonden. Stel in op `0` of laat weg om alle te includeren. |
| `exerciseMode` | ja | `interactive` (Monaco editor) of `external` (link naar extern) |
| `language` | nee | Taal van de UI, standaard `nl` |
| `subtitle` | nee | Getoond onder de titel |
| `description` | nee | Korte omschrijving van de module |
| `youtube` | nee | URL van een intro-video |
| `youtubeTitle` | nee | Label voor de YouTube-knop; standaard `"Crash Course"` |
| `logoAlt` | nee | Alternatieve tekst voor het module-logo |
| `algemeen` | nee | Algemene leeruitkomsten toegevoegd aan de checklist |

### `content/weekN/theory.md`

YAML frontmatter + Markdown body. De body ondersteunt standaard Markdown,
syntax-highlighted codeblokken en custom elementen (zie
[Custom elementen in Markdown](#custom-elementen-in-markdown)).

```yaml
---
week: 1
title: Titel van de week
goal: Wat de student aan het einde van deze week kan.
accent: indigo
summary: Korte samenvatting getoond op de startpagina.
leeruitkomsten:
  - Ik kan ...
---

Markdown-inhoud hier...
```

Voor **willekeurige secties** (niet-genummerde mappen) vervang je `week:` door `sort:` om de positie in de navigatie te bepalen:

```yaml
---
sort: 4                 # verschijnt na week 3 in de navigatie
title: Extra materiaal
goal: Je verkent aanvullende onderwerpen.
accent: slate
summary: Aanvullende inhoud buiten de weekstructuur.
leeruitkomsten:
  - Ik ben bekend met het extra materiaal
---
```

### `content/weekN/quiz.md` *(optioneel)*

```yaml
---
title: Quiz Week 1
passScore: 70
questions:
  - id: q1
    question: Vraag?
    options:
      - Antwoord A
      - Antwoord B
    correct: 1
    explanation: Uitleg waarom dit correct is.
---
```

The `correct` field determines the correct answer, 0-indexed. Be sure to vary this and not have a predictable pattern.

### `content/weekN/assignment.md` *(optioneel)*

De Markdown **body** wordt gesplitst op een lege regel: de eerste alinea
wordt de `case`, de rest de opdrachtomschrijving.

```yaml
---
week: 1
title: Bouw een pagina-layout
subtitle: Praktische opdracht
deliverables:
  - Een werkende HTML/CSS pagina
criteria:
  - Grid wordt gebruikt voor de totale layout
maxPoints: 10
tips:
  - Begin met de grid-container
---

Beschrijving van de case.

Instructies voor de opdracht.
```

### `content/weekN/exercises/_meta.md` *(optioneel)*

```yaml
---
week: 1
title: CSS Grid oefeningen
color: indigo
mode: interactive   # optioneel, overschrijft exerciseMode voor deze set
---
```

### `content/weekN/exercises/N.md`

Elk bestand is één oefening. Het YAML-frontmatter bevat de metadata;
de Markdown **body** wordt gebruikt als oefeninhoud.

**Tekst-oefening met Markdown body (aanbevolen voor rijke inhoud):**

```markdown
---
id: 1
difficulty: 1
title: Kolommen
type: text
---

Maak een grid met **twee gelijke kolommen** met `grid-template-columns`.

## Tips

- Gebruik `repeat(2, 1fr)` voor gelijke kolommen.
- `fr` staat voor _fractional unit_.
```

**Verkorte vorm (voor zeer korte oefeningen):**

```yaml
---
type: text
title: Kolommen
description: Maak een grid met twee gelijke kolommen.
---
```

Als zowel een body als een `description`-veld aanwezig zijn, heeft de body voorrang.

**Tekst-oefening gekoppeld aan theoriepagina's (optioneel):**

Gebruik `linked_theory` om theoriepagina's te koppelen. Een uitschuifbaar paneel
verschijnt rechts met een tabblad per week, zodat studenten de theorie kunnen
raadplegen zonder de oefening te verlaten.

```yaml
---
id: 3
type: text
title: Kolommen
linked_theory:
  - week1
  - week2
---
```

| Veld | Verplicht | Omschrijving |
| ---- | --------- | ------------ |
| `linked_theory` | nee | Lijst van week-id's (bijv. `week1`). Toont een uitschuifbaar paneel rechts met tabbladen per week, als iframes. Zonder dit veld wordt geen paneel of knop getoond. Theoriepagina's worden geladen zonder eigen navigatiebalk. |

---

Het `type`-veld bepaalt welk oefeningtype wordt gerenderd:

| Type | Wat wordt gerenderd |
| ---- | -------------------- |
| `css-playground` | Monaco CSS-editor met live preview en geautomatiseerde checks |
| `areas` | Drag-and-drop builder voor grid-template-areas |
| `responsive` | Monaco CSS-editor met resizable viewport preview |
| `js-playground` | Monaco JS-editor, sandboxed uitvoering (iframe, geen same-origin), console-output + geautomatiseerde checks |
| `external` | Link-out kaart met een URL |
| `text` | Alleen-omschrijving kaart (geen interactief element) |

**CSS-playground oefening:**

```yaml
---
type: css-playground
title: Voeg een gap toe
starterCss: ".grid { display: grid; }"
previewHtml: "<!DOCTYPE html><html>…<div class='grid'>…</div>…</html>"
solution: ".grid { display: grid; gap: 16px; }"
checks:
  - type: includes
    value: gap
    msg: 'display: gap'
---
```

**Areas-oefening (grid-template-areas builder):**

```yaml
---
type: areas
title: Header over volledige breedte
areaItems: [header, main, sidebar]
areaOptions: [header, main, sidebar]
gridColumns: 1fr 1fr
expected:
  container: |-
    "header header"
    "main sidebar"
  items:
    header: header
    main: main
    sidebar: sidebar
---
```

**Responsive oefening (resizable viewport preview):**

```yaml
---
type: responsive
title: Mobiele layout
starterCss: ".grid { grid-template-columns: repeat(2, 1fr); }"
previewHtml: "<!DOCTYPE html><html>…</html>"
solution: "@media (max-width: 600px) { .grid { grid-template-columns: 1fr; } }"
checks:
  - type: mediaQuery
    values: ['600px', '1fr']
    msg: media query met 1 kolom bij 600px
---
```

**JS-playground oefening (sandboxed uitvoering):**

```yaml
---
type: js-playground
title: Haal een to-do item op
starterJs: "// TODO: gebruik fetch() en console.log()"
solution: |-
  fetch('https://jsonplaceholder.typicode.com/todos/1')
    .then((response) => response.json())
    .then((data) => console.log(data.title))
checks:
  - type: sourceIncludesAll
    values: [fetch]
    msg: 'gebruikt fetch() om de API aan te roepen'
  - type: consoleIncludes
    value: delectus aut autem
    msg: 'logt de titel van de todo naar de console'
---
```

**Externe oefening (link naar extern):**

```yaml
---
type: external
title: Grid Garden
url: https://cssgridgarden.com
---
```

### `content/assessments/theory-assessment.md`

Zelfde structuur als `quiz.md`.

---

### `content/assessments/practical-assessment.md`

Bevat vrije Markdown-inhoud. Dit bestand is bedoeld om in te leveren via het leerplatform Itslearning en wordt niet weergegeven als een quiz of interactief meetmoment.

## Custom elementen in Markdown

Theoriepagina's ondersteunen de volgende custom blok-elementen in Markdown:

| Element | Doel |
| ------- | ---- |
| `<x-callout>` | Notitieblok. Gebruik `type="warning"` voor waarschuwingen, `type="tip"` voor tips, `type="danger"` voor gevaren, `type="info"` voor informatie, of `type="note"` voor algemene notities. |
| `<x-card title="…">` | Inhoudskaart met een titel. |
| `<x-compare>` / `<x-compare-item title="…">` | Kolommen naast elkaar. |
| `<x-nav label="…">` | Navigatielinks onderaan (één Markdown-link per regel). |
| `<x-browser>` | Browserscherm met titelbalk en niet-functionele knoppen voor minimaliseren, maximaliseren en sluiten. Voeg `title="…"` toe om een aangepaste label voor de titelbalk in te stellen (standaard: `Browser`). |

Voorbeeld:

```markdown
<x-callout type="warning">
Let op: alleen **directe kinderen** van de grid-container worden grid-items.
</x-callout>

<x-compare>
<x-compare-item title="Flexbox — één richting">

Gebruik voor componenten: navigatiebalken, knoprijen.

</x-compare-item>
<x-compare-item title="Grid — twee richtingen">

Gebruik voor volledige pagina-layouts.

</x-compare-item>
</x-compare>

<x-browser>

![Screenshot of the result](../assets/result.png)

</x-browser>

<x-browser title="https://example.com">

This is how the page looks after applying the CSS.

</x-browser>
```

## Voorbeeld: CSS Grid

De `content/` map in dit template bevat een uitgewerkt voorbeeld van een
4-weken module over CSS Grid. Je kunt dit gebruiken als referentie voor
de structuur en opmaak van je eigen content.

## Wat wordt gegenereerd

De build-pipeline draait vóór Vite en produceert de volgende bestanden:

| Uitvoer | Bron |
| ------- | ---- |
| `src/data/manifest.json` | `module.md` + frontmatter van alle secties |
| `src/data/theory-weekN.json` | `weekN/theory.md` |
| `src/data/theory-<map>.json` | `<map>/theory.md` (willekeurige secties) |
| `src/data/meetmoment-quiz-weekN.json` | `weekN/quiz.md` *(indien aanwezig)* |
| `src/data/exercises/weekN.json` | `weekN/exercises/` *(indien aanwezig)* |
| `src/data/inleveropdracht-weekN.json` | `weekN/assignment.md` *(indien aanwezig)* |
| `src/data/checklist.json` | `leeruitkomsten` uit alle secties |
| `src/data/meetmoment-theorie.json` | `assessments/theory-assessment.md` *(indien aanwezig)* |
| `src/data/meetmoment-praktijk.json` | `assessments/practical-assessment.md` *(indien aanwezig)* |
| `pages/weekN-theorie.html` | gegenereerd vanuit template |
| `pages/weekN-oefeningen.html` | gegenereerd vanuit template |
| `pages/weekN-meetmoment.html` | gegenereerd vanuit template *(alleen als `quiz.md` bestaat)* |
| `pages/weekN-oefening.html` | gegenereerd vanuit template |
| `pages/weekN-inleveropdracht.html` | gegenereerd vanuit template *(alleen als `assignment.md` bestaat)* |
| `pages/<map>-theorie.html` | gegenereerd vanuit template (willekeurige secties) |
| `pages/checklist.html` | gegenereerd vanuit template |
| `pages/meetmoment-theorie.html` | gegenereerd vanuit template *(alleen als assessment-bestand bestaat)* |
| `pages/meetmoment-praktijk.html` | gegenereerd vanuit template *(alleen als assessment-bestand bestaat)* |
| `index.html` | gegenereerd vanuit template |

In `dev`-modus worden wijzigingen in `content/` automatisch herbouwd en herladen in de browser.

## Publiceren (GitHub Pages)

Push naar `main` — de GitHub Actions workflow bouwt automatisch en publiceert naar GitHub Pages.

Zorg dat je in de repo-instellingen **Settings → Pages → Source: GitHub Actions** hebt ingesteld.
