---
title: Meetmoment Praktisch — CSS Grid
navLabel: Meetmoment Praktisch
description: Bouw een werkende pagina-layout met CSS Grid en lever het in bij je docent ter beoordeling.
---

## Startpunt

Download het startpunt **[portfolio-startpunt.zip](./assets/portfolio-startpunt.zip)** en pak het uit. Je krijgt een werkende **Portfolio**-pagina — een persoonlijke overzichtspagina met projecten — zonder layout.
Jouw taak is om de layout toe te voegen door de `/* TODO */`-commentaren in de
bestanden in te vullen.

De bestanden die jij aanvult zijn:

- `css/layout.css` — grid-container en plaatsing van de hoofdgebieden
- `css/projects.css` — responsief projectenraster
- `css/header.css` — navigatiebalk met grid of flexbox
- `index.html` — ontbrekende grid-klassen en wrapper-elementen toevoegen

Gebruik uitsluitend CSS Grid voor de paginaopbouw — geen kant-en-klare frameworks zoals Bootstrap.

## Opdracht

Bouw de volgende layout op met CSS Grid:

- Een **header** die de volledige breedte beslaat
- Een **sidebar** links (navigatie) en een **main content**-gebied rechts, naast elkaar
- Een **footer** die de volledige breedte beslaat
- Binnen het content-gebied: een **projectenraster** dat op een breed scherm drie kolommen toont, op een tablet twee kolommen en op mobiel één kolom

## Wat wordt beoordeeld

### Grid-container & gebieden

- `layout.css` definieert een grid-container met `display: grid`
- De rijen en kolommen zijn ingesteld met `grid-template-columns` en `grid-template-rows`
- De vier hoofdgebieden (header, sidebar, main, footer) zijn benoemd met `grid-template-areas`
- Elk gebied is geplaatst via `grid-area` op het bijbehorende element

### Projectenraster

- Het projectenraster gebruikt een aparte grid-container
- Kolombreedte is ingesteld met `repeat()` en `minmax()` of een vaste eenheid
- `gap` of `column-gap` / `row-gap` is gebruikt voor de tussenruimte
- Projectkaarten vullen hun cel netjes op (geen overflow, geen vreemde hoogtes)

### Responsive gedrag

- Op een breed scherm (≥ 1024 px) worden drie projectkolommen getoond
- Op een tablet (768 px – 1023 px) worden twee projectkolommen getoond
- Op mobiel (< 768 px) wordt één projectkolom getoond en schuift de sidebar boven de main content
- Media queries staan in de juiste bestanden en overschrijven alleen wat nodig is

### Afwerking

- De pagina is visueel verzorgd: gelijke marges, leesbare lettergrootte, zichtbare kaartranden
- Er zijn geen horizontale scrollbalken op geen enkel schermformaat
- De HTML is valide (gecontroleerd met de W3C Validator); geen foutmeldingen
- De CSS bevat geen ongebruikte of conflicterende regels die de layout breken

## Inleveren

Lever de volgende bestanden in via Itslearning, onder de map "Module: CSS Grid":

- Het volledige project (inclusief alle ingevulde `/* TODO */`-bestanden) als `.zip`-bestand
- Ten minste vier screenshots:
  1. De pagina op een breed scherm (≥ 1024 px) met drie projectkolommen zichtbaar
  2. De pagina op tabletbreedte (768 px) met twee projectkolommen zichtbaar
  3. De pagina op mobiel (< 768 px) met één kolom en de sidebar bovenaan
  4. De W3C Validator-uitvoer voor `index.html` zonder fouten
