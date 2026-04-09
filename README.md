# LLM Knowledge Base

En AI-driven kunskapsbas inspirerad av [Andrej Karpathys LLM Knowledge Base-arkitektur](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f). Designad att användas med [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) och [Obsidian](https://obsidian.md).

## Vad är detta?

Ett system där du samlar källmaterial (artiklar, papers, rapporter, YouTube-videos, tankar) och låter en AI kompilera, organisera och underhålla en kunskapsbas i markdown. Du läser och navigerar i Obsidian - AI:n skriver och underhåller.

**Grundprincip:** Du redigerar sällan wikin manuellt. Det är AI:ns domän.

### Systemets delar

```
Du hittar material  →  raw/ (immutable källmaterial)
                            ↓
                       AI kompilerar
                            ↓
                       wiki/ (organiserad kunskapsbas)
                            ↓
                       Du ställer frågor, AI genererar
                            ↓
                       outputs/ (rapporter, analyser, svar)
                            ↓
                       Filas tillbaka i wikin (kunskapen växer)
```

## Snabbstart

### 1. Klona och anpassa (2 min)

```bash
git clone https://github.com/Pluggentipsar/llm-knowledge-base.git mitt-projekt
cd mitt-projekt
```

Redigera `CLAUDE.md` - fyll i ditt projekts beskrivning, syfte och ämnesord.

### 2. Öppna i Obsidian (1 min)

1. [Ladda ner Obsidian](https://obsidian.md) om du inte har det
2. Klicka "Open folder as vault" och välj projektmappen
3. Du ser Dashboard.md som startsida

### 3. Börja samla material (direkt)

Lägg filer i `raw/` - PDF:er, Word-dokument, artiklar, anteckningar. Sedan i Claude Code:

```
/wiki kompilera     # AI organiserar allt till kunskapsbasen
/research "ditt ämne"  # Sök i vetenskapliga databaser
/capture https://youtube.com/watch?v=...  # Fånga en video
```

## Mappstruktur

```
raw/                # Källmaterial - rör aldrig dessa filer
  inbox/            # Snabbfångat material (bearbetas av /capture)
  artiklar/         # Nedladdade artiklar
  forskning/        # Vetenskapliga papers
  rapporter/        # Rapporter
  inspiration/      # Ideer, videos, poddar, etc.

wiki/               # AI-kompilerad kunskapsbas
  INDEX.md          # Huvudindex (AI underhåller)
  log.md            # Kronologisk logg (append-only)
  begrepp/          # Begreppsartiklar
  forskning/        # Forskningssammanfattningar
  personer/         # Relevanta personer

outputs/            # Genererade rapporter och analyser
templates/          # Obsidian-mallar
```

### Regler

- **raw/** - Immutable. AI läser men ändrar aldrig dessa filer.
- **wiki/** - AI:ns domän. AI skriver, underhåller och kopplar samman artiklar.
- **outputs/** - Genererade svar, rapporter, analyser. Kan filas tillbaka i wikin.
- **log.md** - Append-only kronologisk logg. Allt som händer loggas.

## Skills (Claude Code)

| Kommando | Funktion |
|----------|----------|
| `/research "sökord"` | Sök i OpenAlex, CrossRef, arXiv, Semantic Scholar, DIVA Portal |
| `/ingest fil.pdf` | Konvertera PDF/Word/PPT till markdown via markitdown |
| `/capture URL eller tanke` | Fånga YouTube, LinkedIn, artiklar, snabba ideer |
| `/wiki kompilera` | Kompilera raw-material till wiki-artiklar |
| `/wiki hälsokontroll` | Hitta brutna länkar, orphans, luckor, inkonsekvenser |

## Obsidian-setup

Se [docs/setup-obsidian.md](docs/setup-obsidian.md) for fullständig guide.

### Rekommenderade plugins

| Plugin | Funktion |
|--------|----------|
| Obsidian Git | Auto-synk med GitHub |
| Dataview | Dynamiska tabeller |
| Excalidraw | Rita diagram och begreppskartor |
| Templater | Kraftfulla templates |
| Enhancing Export | Exportera till Word (.docx) |
| Marp Slides | Presentationer fran markdown |

### Web Clipper

Installera [Obsidian Web Clipper](https://obsidian.md/clipper) i din webblasare for att spara artiklar direkt till `raw/artiklar/`.

## Anpassa for ditt projekt

1. **Redigera `CLAUDE.md`** - Fyll i projektbeskrivning, syfte och relevanta amnesord
2. **Lagg till material** i `raw/` - Allt du redan har: PDF:er, anteckningar, artiklar
3. **Kor `/wiki kompilera`** - AI:n organiserar allt
4. **Stall fragor** - AI:n svarar baserat pa kunskapsbasen

## Verktyg som behovs

| Verktyg | Syfte | Installation |
|---------|-------|-------------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) | AI-motor | Se Anthropics guide |
| [Obsidian](https://obsidian.md) | Lasa/navigera kunskapsbasen | Ladda ner fran obsidian.md |
| [Python 3.10+](https://python.org) | Kravs for markitdown | `winget install Python.Python.3` |
| [markitdown](https://github.com/microsoft/markitdown) | PDF/Word till markdown | `pip install "markitdown[all]"` |
| [Pandoc](https://pandoc.org) | Export till Word | `winget install JohnMacFarlane.Pandoc` |
| [Git](https://git-scm.com) | Versionshantering + synk | `winget install Git.Git` |

Se [docs/setup-verktyg.md](docs/setup-verktyg.md) for detaljerad installationsguide.

## Dagligt arbetsflode

```
Morgon:
  Oppna Obsidian → allt synkas fran GitHub
  Kolla Dashboard → oversikt

Under dagen:
  Hittar artikel → Web Clipper → raw/artiklar/
  Hittar paper → Zotero Connector → Zotero
  Har en ide → /capture "min ide"

I Claude Code:
  /research "mitt amne"      → soker databaser
  /wiki kompilera            → uppdaterar kunskapsbasen
  /wiki halsokontroll        → kvalitetskontroll

Kvall:
  Allt pushas automatiskt till GitHub
```

## Inspiration

- [Andrej Karpathys LLM Knowledge Base](https://x.com/karpathy/status/2039805659525644595) - Originalkonceptet
- [Karpathys AGENTS.md Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) - Abstrakt arkitektur
- [VentureBeat: LLM Knowledge Base Architecture](https://venturebeat.com/data/karpathy-shares-llm-knowledge-base-architecture-that-bypasses-rag-with-an) - Artikeln som forklarar konceptet

## Skapare

Byggt av [Joel Rangsjo](https://github.com/Pluggentipsar) med hjalp av Claude Code.

## Licens

MIT
