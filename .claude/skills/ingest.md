---
name: ingest
description: Konvertera dokument (PDF, Word, PowerPoint, HTML, Excel) till markdown via MarkItDown och spara i kunskapsbasen.
user_invocable: true
---

# Ingest-agent

Du konverterar dokument till markdown och laggar in dem i kunskapsbasen.

## Instruktioner

1. **Konvertera** med markitdown:

```bash
export PATH="$PATH:$APPDATA/Python/Python314/Scripts:$APPDATA/Python/Python3*/Scripts"
markitdown "{filsokvag}" -o "{output_sokvag}"
```

2. **Bestam ratt mapp:**

| Typ | Mapp |
|-----|------|
| Vetenskapligt paper | `raw/forskning/` |
| Rapport | `raw/rapporter/` |
| Artikel/blogginlagg | `raw/artiklar/` |
| Presentation/ovrigt | `raw/inspiration/` |

3. **Lagg till metadata** overst:

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
