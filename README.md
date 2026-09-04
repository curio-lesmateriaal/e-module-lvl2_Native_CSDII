# E-module Native (in C#) — CSD-II

Interactieve e-module bij het vak **NATIVE** (module CSD-II, C# Development II) van
de opleiding Software Developer, blok C. Gebouwd met
[`curio-team/e-module-builder`](https://github.com/curio-team/e-module-builder).

De inhoud staat in [`content/`](content/) en is de herschrijving van het
moduleboekje *Moduleboekje_CSDII_v1.3* naar een e-module met genummerde weken.

## Waar gaat deze module over?

In deze module leer je werken met **Objectgeoriënteerd Programmeren (OOP)**,
**WinUI**, **Entity Framework Core (EF Core)** en **API's** binnen C#. Er worden
ook enkele basisprincipes uit eerdere modules herhaald.

* **OOP** — je leert hoe je klassen en objecten gebruikt, en hoe je je code
  schoon en overzichtelijk houdt.
* **WinUI** — hiermee bouw je moderne desktopinterfaces voor
  Windows-toepassingen. WinUI wordt in de lessen en praktijkopdrachten geoefend;
  deze e-module richt zich op de C#-kant.
* **EF Core** — een ORM waarmee je eenvoudig met databases werkt via C#-code,
  zonder handmatig SQL te schrijven.
* **API's** — je leert hoe je REST API's maakt en gebruikt om gegevens uit te
  wisselen tussen applicaties.

### Samenhang met andere onderdelen

Deze module is de ondersteuning bij de praktijkopdrachten van dit blok. Als
voorkennis is CSD-I vereist; je hebt een basis van C# nodig.

### Werkwijze

Bij deze module horen een aantal meetmomenten. Je dient voor deze meetmomenten
samen een gemiddelde boven de 5,5 te hebben. Je gemiddelde en je cijfers zijn te
vinden op SmartPoints. Deze cijfers worden gegeven voor een toets of een CGI.

Inleveropdrachten lever je in via **Itslearning**, onder de map
"Module: Native (C#)". Je docent geeft daar feedback.

### Opbouw (7 weken)

| Week | Onderwerp |
| ---- | --------- |
| 1 | OOP in C# — classes, objecten, referenties, value- vs reference-types |
| 2 | Accessibility & static — public, private, internal, protected, static |
| 3 | EF Core — opzet & model — packages, migrations, DbContext, DbSet |
| 4 | EF Core — CRUD in een console-app — invoeren, ophalen, wijzigen, verwijderen |
| 5 | API — concept & consumeren — HttpClient, JSON, deserialiseren |
| 6 | API — zelf bouwen — HttpListener, request/response, routing |
| 7 | API + EF Core — data serveren & valideren — validatie, Data Annotations, regex |

De weken 13 t/m 16 uit de oorspronkelijke studiewijzer zijn buffer- en
toetsweken: het project uit week 7 is de basis voor de eindopdracht.

## Lokaal draaien

```bash
npm install
npm run dev
```

Open [http://localhost:5173](http://localhost:5173).

| Commando | Omschrijving |
| --- | --- |
| `npm run dev` | Ontwikkelserver op `localhost:5173` (herbouwt bij wijzigingen in `content/`) |
| `npm run build` | Productie-build naar `dist/` |
| `npm run preview` | Preview van de `dist/`-build lokaal |

## Content bewerken

Alleen de [`content/`](content/)-map hoef je te bewerken; de rest wordt
automatisch gegenereerd. Zie de
[e-module-builder-documentatie](https://github.com/curio-team/e-module-builder)
voor de mapstructuur, de frontmatter-velden en de custom Markdown-elementen
(`<x-callout>`, `<x-card>`, `<x-compare>`, `<x-keuzevraag>`, `<x-invul>`,
`<x-vind-de-fout>`, `<x-koppelvraag>`, …).

Elke week heeft een `theory.md`, een `quiz.md`, een `assignment.md` en een
`exercises/`-map. De oefeningen zijn van het type `external` of `text`: je maakt
ze in Visual Studio en markeert ze daarna als voltooid.

De bronafbeeldingen komen uit het moduleboekje en staan per week in
`content/weekN/assets/`.

## Publiceren (GitHub Pages)

Push naar `main` — de GitHub Actions-workflow bouwt automatisch en publiceert
naar GitHub Pages. Zorg dat in de repo-instellingen
**Settings → Pages → Source: GitHub Actions** is ingesteld.

## Versiebeheer moduleboekje

| Versie | Datum | Auteur | Aanpassingen |
| --- | --- | --- | --- |
| 1.0 | 23-06-2025 | B. Kouwenberg, N. Pieter, Q. Norbert | Nieuwe opzet CSD-II. Samenvoegen vorige CSD-III en CSD-IV |
| 1.1 | 28-08-2025 | T. Lutt | Versienummer EF Core-packages gekoppeld aan versie .NET |
| 1.2 | 04-11-2025 | T. Lutt | Hoofdstuk API + EF Core met uitleg over validatie toegevoegd |
| 1.3 | 31-08-2026 | N. Pieter | Tekst over relaties verwijderd uit H3 EF Core en tekst over ORM toegevoegd |
| e-module | 09-2026 | — | Moduleboekje v1.3 herschreven naar week-gebaseerde e-module (7 weken) |
