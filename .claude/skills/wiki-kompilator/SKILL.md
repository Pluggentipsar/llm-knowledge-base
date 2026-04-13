---
name: wiki
description: Kompilera och underhall kunskapsbasen (wiki/). Skapa artiklar fran raw-material, underhall INDEX.md, hitta kopplingar.
user_invocable: true
---

# Wiki-kompilator

Du underhaller kunskapsbasen i `wiki/`.

## Kommandon

### `/wiki kompilera` (eller utan argument)

Stodjer flaggor:
- `/wiki kompilera --citat 5` — andrar antal citat per kalla (standard: 2-3)
- `/wiki kompilera --inga-citat` — stanger av citat helt for denna korning

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

- [Insikt som parafras eller syntes]
  > "Exakt originaltext som belagger insikten."
  > — *[Kallnamn], [raw/fil.md]*

- [Nasta insikt]
  > "Another supporting quote."
  > — *[Kallnamn], [raw/fil.md]*

## Kopplingar
- Relaterat: [[annat-amne]]

## Kallor
- [Kalla med referens till raw/-fil]

---
*Senast uppdaterad: {datum}*
```

**Regler for citat:**
- Om `--inga-citat` angavs: utelam citat helt, skriv bara insikterna som punkter
- Annars: lyft 2-3 citat per kalla som standard, eller det antal som angavs med `--citat N`
- Bara for de viktigaste insikterna (faktapastaenden, karnargument, exakta formuleringar med hog informationstathet)
- Svenska/engelska kallor: citera i originalsprak
- Ovriga sprak: oversatt till engelska, ange kallsprak: `[finska, oversatt]`
- Citaten ska vara exakta — ingen parafrasering inuti citattecken

4. **Uppdatera INDEX.md** med nya artiklar
5. **Logga** i `wiki/log.md`: `[DATUM] [COMPILE] Kompilerat X nya artiklar fran raw/`

### `/wiki halsokontroll`

Se separat skill: `/halsokontroll`

### `/wiki sok {fraga}`

Sok genom wikin och presentera relevant information.
