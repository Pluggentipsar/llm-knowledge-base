---
name: capture
description: Fanga innehall fran YouTube, LinkedIn, webbartiklar och snabba ideer. Sammanfattar, kategoriserar och sparar till kunskapsbasen.
user_invocable: true
---

# Capture-agent

Du fangar innehall fran olika kallor med lag friktion.

## Anvandning

```
/capture https://youtube.com/watch?v=...
/capture https://linkedin.com/posts/...
/capture https://example.com/article
/capture Intressant tanke om...
```

## Instruktioner

### 1. Identifiera typen

| Typ | Kannetecken | Atgard |
|-----|-------------|--------|
| YouTube | youtube.com, youtu.be | Hamta transkript via markitdown eller WebFetch |
| LinkedIn | linkedin.com | Hamta via WebFetch |
| Webbsida | Alla andra URL:er | Hamta via WebFetch eller markitdown |
| Tanke/ide | Ingen URL | Spara direkt med metadata |

### 2. Hamta innehall

**YouTube:**
```bash
export PATH="$PATH:$APPDATA/Python/Python314/Scripts:$APPDATA/Python/Python3*/Scripts"
export PYTHONIOENCODING=utf-8
markitdown "{url}" -o /tmp/capture.md
```

**Webbsidor:** Anvand WebFetch.

### 3. Spara strukturerat

```markdown
---
tags:
  - raw
  - capture
  - {typ}
kalla: {URL eller "egen tanke"}
datum_fangad: {datum}
---

# {Beskrivande titel}

> [!summary] Sammanfattning
> {2-4 meningar}

## Nyckelpoanger
- ...

## Relevans
- Kopplingar: [[relaterade wiki-artiklar]]

## Originalinnehall
{Transkript/text om tillgangligt}
```

4. **Spara till** `raw/inbox/{datum}-{slug}.md`

5. **Logga** i `wiki/log.md`: `[DATUM] [INGEST] Fangat: {titel} ({typ})`
