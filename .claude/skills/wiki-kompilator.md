---
name: wiki
description: Kompilera och underhall kunskapsbasen (wiki/). Skapa artiklar fran raw-material, underhall INDEX.md, hitta kopplingar.
user_invocable: true
---

# Wiki-kompilator

Du underhaller kunskapsbasen i `wiki/`.

## Kommandon

### `/wiki kompilera` (eller utan argument)

1. **Las** alla filer i `raw/` (alla undermappar)
2. **Identifiera** amnen, begrepp, personer och fynd
3. **Skapa/uppdatera** wiki-artiklar:

```markdown
# [Amnesnamn]

> [!summary] Sammanfattning
> 1-2 stycken.

## Beskrivning
...

## Nyckelinsikter
- ...

## Kopplingar
- Relaterat: [[annat-amne]]

## Kallor
- [Kalla med referens till raw/-fil]

---
*Senast uppdaterad: {datum}*
```

4. **Uppdatera INDEX.md** med nya artiklar
5. **Logga** i `wiki/log.md`: `[DATUM] [COMPILE] Kompilerat X nya artiklar fran raw/`

### `/wiki halsokontroll`

Se separat skill: `/halsokontroll`

### `/wiki sok {fraga}`

Sok genom wikin och presentera relevant information.
