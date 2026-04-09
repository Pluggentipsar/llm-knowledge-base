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

### 2. Installera verktyg (5 min)

```bash
# markitdown - konverterar PDF, Word, PowerPoint, Excel, HTML till markdown
pip install "markitdown[all]"

# Pandoc - exportera markdown till Word (.docx)
winget install JohnMacFarlane.Pandoc
```

### 3. Öppna i Obsidian (1 min)

1. [Ladda ner Obsidian](https://obsidian.md) om du inte har det
2. Klicka "Open folder as vault" och välj projektmappen
3. Du ser Dashboard.md som startsida

### 4. Börja samla material

Lägg filer i `raw/` - PDF:er, Word-dokument, artiklar. Sedan i Claude Code:

```
/wiki kompilera                          # AI organiserar allt till kunskapsbasen
/research "ditt ämne"                    # Sök i vetenskapliga databaser
/capture https://youtube.com/watch?v=... # Fånga en video
/ingest rapport.pdf                      # Konvertera PDF till markdown
```

---

## Dokumentkonvertering med markitdown

[markitdown](https://github.com/microsoft/markitdown) (Microsoft) konverterar dokument till markdown så att AI:n kan läsa dem.

### Stödda format

| Format | Exempel |
|--------|---------|
| PDF | Forskningsrapporter, myndighetsrapporter |
| Word (.docx) | Anteckningar, utkast, mötesprotokoll |
| PowerPoint (.pptx) | Presentationer |
| Excel (.xlsx/.csv) | Statistik, data |
| HTML | Webbsidor |
| Bilder | OCR av text i screenshots/foton |
| YouTube-URL:er | Hämtar transkript automatiskt |

### Användning

```bash
# Konvertera en PDF
markitdown rapport.pdf -o raw/rapporter/rapport.md

# Konvertera en Word-fil
markitdown anteckningar.docx -o raw/inspiration/anteckningar.md

# Konvertera en YouTube-video (hämtar transkript)
markitdown "https://www.youtube.com/watch?v=abc123" -o raw/inspiration/video.md

# Batch-konvertera alla PDF:er i en mapp
for f in /sökväg/till/*.pdf; do
  markitdown "$f" -o "raw/forskning/$(basename "${f%.*}").md"
done
```

### I Claude Code

Skillen `/ingest` använder markitdown automatiskt:

```
/ingest rapport.pdf              # Konverterar och sparar i rätt mapp
/ingest presentation.pptx        # Fungerar med alla format
```

---

## Vetenskapliga databaser

Skillen `/research` söker i fem öppna akademiska databaser. Inga API-nycklar behövs.

### OpenAlex

Största öppna databasen för akademisk forskning. 250M+ verk.

```bash
# Sök efter forskning
curl -s "https://api.openalex.org/works?search=digital+resilience+education&per_page=5&sort=relevance_score:desc"

# Filtrera på år
curl -s "https://api.openalex.org/works?search=AI+literacy&filter=from_publication_date:2023-01-01&per_page=10"

# Filtrera på språk
curl -s "https://api.openalex.org/works?search=källkritik&filter=language:sv&per_page=10"
```

**Dokumentation:** https://docs.openalex.org

### CrossRef

Metadata för 150M+ akademiska publikationer via DOI.

```bash
# Sök efter böcker
curl -s "https://api.crossref.org/works?query=media+literacy+AI&rows=5&sort=relevance"

# Filtrera på typ (bok, artikel, etc.)
curl -s "https://api.crossref.org/works?query=critical+thinking&filter=type:book&rows=5"
```

**Dokumentation:** https://www.crossref.org/documentation/

### arXiv

Preprints inom datavetenskap, AI, matematik m.m.

```bash
curl -s "https://export.arxiv.org/api/query?search_query=all:AI+sycophancy&start=0&max_results=5&sortBy=relevance"
```

**Dokumentation:** https://info.arxiv.org/help/api/

### Semantic Scholar

AI-fokuserad akademisk sökmotor (Allen Institute for AI).

```bash
curl -s "https://api.semanticscholar.org/graph/v1/paper/search?query=metacognition+AI+education&limit=5&fields=title,year,abstract,citationCount,authors"
```

**Dokumentation:** https://api.semanticscholar.org

### DIVA Portal (svensk forskning)

Svensk forskningsdatabas - avhandlingar, rapporter, artiklar från svenska lärosäten.

```bash
curl -s "https://diva-portal.org/smash/export.jsf?format=csv&searchType=RESEARCH&query=källkritik"
```

**Dokumentation:** https://www.diva-portal.org

### Exempel: `/research` i praktiken

```
> /research "digital resilience children education"

Söker i OpenAlex, CrossRef, arXiv...

Resultat (topp 5):

1. Orben (2020) - "Adolescent mental health in the digital age"
   930 citeringar | DOI: 10.1111/jcpp.13190
   Beskrivning: Omfattande forskningsöversikt om sambandet digital
   medieanvändning och ungdomars psykiska hälsa.

2. ...

Sparat till: outputs/research-2026-04-09-digital-resilience.md
```

---

## Capture: Fånga material från webben

Skillen `/capture` hanterar innehåll från olika plattformar med minimal friktion.

```
/capture https://youtube.com/watch?v=abc123
→ Hämtar transkript, sammanfattar, sparar till raw/inbox/

/capture https://linkedin.com/posts/nagon-intressant-post
→ Hämtar innehållet, sammanfattar, kategoriserar

/capture Intressant tanke: elever litar mer på AI som ger emojis
→ Sparar tanken med datum och föreslår wiki-kopplingar

/capture https://example.com/article Relevant för mitt projekt
→ Hämtar artikeln, sammanfattar, taggar med din kommentar
```

### Integration med MCP-server (valfritt)

Om du har en extern capture-tjänst (t.ex. en MCP-server kopplad till Supabase) kan du sätta upp automatisk synk. Tagga items med ett projektspecifikt tag, och schemalägg en daglig synk:

```
Dag 1: Du hittar en artikel → sparar i din capture-tjänst med tag "mitt-projekt"
Dag 2: Schemalagd synk hämtar nya items → sparar till raw/inbox/
       /wiki kompilerar nytt material → integreras i kunskapsbasen
```

Detta kan konfigureras som en schemalagd uppgift i Claude Code med `mcp__scheduled-tasks__create_scheduled_task`.

---

## Mappstruktur

```
raw/                # Källmaterial - rör aldrig dessa filer
  inbox/            # Snabbfångat material (bearbetas av /capture)
  artiklar/         # Nedladdade artiklar (Web Clipper sparar hit)
  forskning/        # Vetenskapliga papers
  rapporter/        # Myndighetsrapporter, policydokument
  inspiration/      # Idéer, videos, poddar, etc.

wiki/               # AI-kompilerad kunskapsbas
  INDEX.md          # Huvudindex med alla artiklar (AI underhåller)
  log.md            # Kronologisk logg (append-only)
  begrepp/          # Begreppsartiklar
  forskning/        # Forskningssammanfattningar
  personer/         # Relevanta personer

outputs/            # Genererade rapporter och analyser
templates/          # Obsidian-mallar
```

### Regler

- **raw/** - Immutable. AI läser men ändrar aldrig dessa filer.
- **wiki/** - AI:ns domän. AI skriver, underhåller och kopplar samman artiklar med `[[wiki-länkar]]`.
- **outputs/** - Genererade svar, rapporter, analyser. Kan filas tillbaka i wikin.
- **log.md** - Append-only kronologisk logg. Allt som händer loggas med format: `[DATUM] [TYP] Beskrivning`

---

## Skills (Claude Code)

| Kommando | Funktion |
|----------|----------|
| `/research "sökord"` | Sök i OpenAlex, CrossRef, arXiv, Semantic Scholar, DIVA Portal |
| `/ingest fil.pdf` | Konvertera PDF/Word/PPT till markdown via markitdown |
| `/capture URL eller tanke` | Fånga YouTube, LinkedIn, artiklar, snabba idéer |
| `/wiki kompilera` | Kompilera raw-material till wiki-artiklar |
| `/halsokontroll` | Hitta brutna länkar, orphans, luckor, inkonsekvenser |

---

## Obsidian

Se [docs/setup-obsidian.md](docs/setup-obsidian.md) for fullständig guide.

### Rekommenderade plugins

| Plugin | Funktion |
|--------|----------|
| Obsidian Git | Auto-synk med GitHub (var 5:e minut) |
| Dataview | Dynamiska tabeller och queries |
| Excalidraw | Rita diagram och begreppskartor |
| Templater | Kraftfullare templates med auto-datum |
| Enhancing Export | Exportera till Word (.docx) via Pandoc |
| Marp Slides | Presentationer direkt från markdown |

### Web Clipper

[Obsidian Web Clipper](https://obsidian.md/clipper) sparar webbartiklar direkt till `raw/artiklar/` med ett klick. Finns för Chrome, Firefox, Safari, Edge och mobil.

### Graph View

Tryck `Ctrl+G` i Obsidian för att se hur alla begrepp och artiklar hänger ihop visuellt. Ju fler `[[wiki-länkar]]` desto rikare graf.

---

## Anpassa för ditt projekt

### 1. Redigera CLAUDE.md

Fyll i:
- Projektbeskrivning
- Centrala ämnesområden
- Relevanta söktermer (svenska och engelska)

### 2. Lägg till egna skills

Skapa nya `.md`-filer i `.claude/skills/` för projektspecifika behov. Exempel:
- `/skribent` - för skrivprojekt
- `/faktakoll` - för journalistik
- `/sammanfatta` - för studier

### 3. Lägg till material

Dumpa allt du har i `raw/` - PDF:er, anteckningar, artiklar, presentationer. Kör sedan `/wiki kompilera` för att låta AI:n organisera det.

---

## Verktyg

| Verktyg | Syfte | Installation |
|---------|-------|-------------|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) | AI-motor (kör skills, kompilerar wiki) | Se Anthropics guide |
| [Obsidian](https://obsidian.md) | Läsa, navigera och visualisera kunskapsbasen | Ladda ner från obsidian.md |
| [Python 3.10+](https://python.org) | Krävs för markitdown | `winget install Python.Python.3` |
| [markitdown](https://github.com/microsoft/markitdown) | Konvertera PDF/Word/PPT/YouTube till markdown | `pip install "markitdown[all]"` |
| [Pandoc](https://pandoc.org) | Export till Word (.docx) | `winget install JohnMacFarlane.Pandoc` |
| [Git](https://git-scm.com) | Versionshantering + synk | `winget install Git.Git` |
| [Zotero](https://www.zotero.org) | Referenshantering (valfritt, för akademiska projekt) | `winget install DigitalScholar.Zotero` |

Se [docs/setup-verktyg.md](docs/setup-verktyg.md) för detaljerad installationsguide.

---

## Dagligt arbetsflöde

```
Morgon:
  Öppna Obsidian → allt synkas från GitHub
  Kolla Dashboard → översikt
  Kolla raw/inbox/ → nytt material att bearbeta?

Under dagen:
  Hittar artikel     → Web Clipper → raw/artiklar/
  Hittar paper       → Zotero Connector → Zotero
  Ser YouTube-video  → /capture URL
  Har en idé         → /capture "min idé"
  Får en PDF         → /ingest rapport.pdf

I Claude Code:
  /research "mitt ämne"   → söker 5 vetenskapliga databaser
  /wiki kompilera         → integrerar nytt material
  /halsokontroll          → kvalitetskontroll

Kvall:
  Allt pushas automatiskt till GitHub
  → synkas till andra datorer och mobilen
```

---

## Inspiration och bakgrund

Systemet bygger på Andrej Karpathys koncept "LLM Knowledge Bases" (april 2026) - att använda LLM:er för att bygga och underhålla personliga kunskapsbaser i markdown:

> Rådata från ett antal källor samlas in, kompileras sedan av en LLM till en markdown-wiki, och opereras sedan på av LLM:en för Q&A och för att stegvis förbättra wikin. Allt visas i Obsidian. Du redigerar sällan wikin manuellt - det är LLM:ens domän.

- [Karpathys originalinlägg (X)](https://x.com/karpathy/status/2039805659525644595)
- [AGENTS.md Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [VentureBeat: LLM Knowledge Base Architecture](https://venturebeat.com/data/karpathy-shares-llm-knowledge-base-architecture-that-bypasses-rag-with-an)

---

## Skapare

Byggt av [Joel Rangsjö](https://github.com/Pluggentipsar) med hjälp av Claude Code.

Ursprungligen utvecklat som stödsystem för ett bokprojekt, sedan generaliserat till ett template som alla kan använda.

## Licens

MIT
