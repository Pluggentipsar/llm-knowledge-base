---
name: ingest
description: Konvertera dokument (PDF, Word, PowerPoint, HTML, Excel) till markdown via MarkItDown och spara i kunskapsbasen.
user_invocable: true
---

# Ingest-agent

Du konverterar dokument till markdown och laggar in dem i kunskapsbasen.

## Lage: specifik fil vs. alla filer

- **Med argument** (t.ex. `/ingest rapport.pdf`): konvertera bara den filen.
- **Utan argument eller med `alla`**: kör batch-lage (se nedan).

### Batch-lage (`/ingest` eller `/ingest alla`)

1. **Skanna** alla filer i `raw/` rekursivt med filtillagen: `.pdf`, `.docx`, `.pptx`, `.xlsx`, `.html`, `.htm`
2. **Las** `wiki/log.md` och extrahera alla filnamn som redan forkommit i en `[INGEST]`-rad
3. **Filtrera** bort redan ingestade filer — bearbeta bara nya
4. **Rapportera** vilka filer som hittades, vilka som skippas (redan ingestade) och vilka som processas
5. Fortsatt med vanliga instruktioner nedan for varje ny fil
6. **Avsluta** med en summering: X filer ingestade, Y skippade

---

## Instruktioner (per fil)

1. **Konvertera** med markitdown:

```bash
export PATH="$PATH:$APPDATA/Python/Python314/Scripts:$APPDATA/Python/Python3*/Scripts"
markitdown "{filsokvag}" -o "{output_sokvag}"
```

2. **Bestam ratt mapp for .md-filen:**

| Typ | Mapp |
|-----|------|
| Vetenskapligt paper | `raw/forskning/` |
| Rapport | `raw/rapporter/` |
| Artikel/blogginlagg | `raw/artiklar/` |
| Presentation/ovrigt | `raw/inspiration/` |

3. **Flytta originalfilen** till `raw/originals/` (skapa mappen om den inte finns):

```bash
mv "{original_filsokvag}" "raw/originals/{filnamn}"
```

Detta gor att filer i `raw/originals/` ar konverterade, medan filer kvar i `raw/` annu inte bearbetats.

4. **Lagg till metadata** overst:

```markdown
---
kalla: [URL eller filnamn]
typ: paper/rapport/artikel
datum_publicerad: YYYY-MM-DD
datum_inmatad: YYYY-MM-DD
tags:
  - raw
  - [typ]
---
```

4. **Fraga anvandaren** om de vill kora `/wiki kompilera` for att integrera materialet.

5. **Logga** i `wiki/log.md`: `[DATUM] [INGEST] Konverterat: {filnamn}`
