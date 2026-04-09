# Kunskapsbas: [DITT PROJEKT]

## Om projektet

<!-- Fyll i en kort beskrivning av ditt projekt -->
Beskriv ditt projekt har. Vad handlar det om? Vad ar syftet?

## Amnesomraden

<!-- Lista de amnen och teman som ar centrala for ditt projekt -->
1. **Amne 1** - Kort beskrivning
2. **Amne 2** - Kort beskrivning
3. **Amne 3** - Kort beskrivning

## Mappstruktur

```
raw/           # Obearbetat kallmaterial (ror ej dessa filer)
  inbox/       # Snabbfangat material (YouTube, LinkedIn, tankar)
  artiklar/    # Nedladdade artiklar
  forskning/   # Vetenskapliga papers
  rapporter/   # Rapporter
  inspiration/ # Ideer, videos, poddar

wiki/          # AI-kompilerad kunskapsbas (AI underhaller)
  INDEX.md     # Huvudindex
  log.md       # Kronologisk logg
  begrepp/     # Begreppsartiklar
  forskning/   # Forskningssammanfattningar
  personer/    # Relevanta personer

outputs/       # Genererade analyser och material
```

## Wiki-regler

- Varje amne far en egen .md-fil
- Varje wiki-fil borjar med en sammanfattning (1-2 stycken)
- Relaterade amnen lankas med `[[amnesnamn]]`
- INDEX.md listar alla artiklar med en enrads-beskrivning
- Nar nytt raw-material laggs till, uppdateras relevant wiki-artikel
- **log.md** ar en append-only kronologisk logg - alla andringar loggas
- Varje loggrad: `[DATUM] [TYP] Beskrivning`
- Typer: INGEST, COMPILE, RESEARCH, UPDATE, LINK, LINT, NOTE, QUESTION
- Kor LINT (halsokontroll) regelbundet for att hitta inkonsekvenser och luckor

## Vetenskapliga databaser (oppna API:er)

```
OpenAlex:          https://api.openalex.org/works?search={query}
arXiv:             https://export.arxiv.org/api/query?search_query={query}
Semantic Scholar:  https://api.semanticscholar.org/graph/v1/paper/search?query={query}
CrossRef:          https://api.crossref.org/works?query={query}
DIVA Portal:       https://diva-portal.org/smash/export.jsf?format=csv&searchType=RESEARCH&query={query}
```

## Soktermer

<!-- Lagg till soktermer relevanta for ditt projekt, pa bade svenska och engelska -->
- "term 1", "term 2", "term 3"

## Verktyg

- `markitdown` - konverterar PDF/Word/PPT till markdown (for /ingest)
