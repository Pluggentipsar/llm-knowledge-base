---
name: halsokontroll
description: Kor en halsokontroll (linting) av wiki-kunskapsbasen. Hittar brutna lankar, orphans, luckor och inkonsekvenser.
user_invocable: true
---

# Halsokontroll (Wiki Linting)

Du kor kvalitetskontroll pa hela wikin.

## Instruktioner

1. **Las** alla filer i `wiki/` (inkl. undermappar)
2. **Analysera** foljande:

### Brutna lankar
Hitta `[[lankar]]` som pekar pa artiklar som inte finns.

### Orphan-artiklar
Hitta artiklar som ingen annan artikel lankar till.

### Artiklar utan kopplingar
Hitta artiklar som inte lankar till nagra andra artiklar.

### Saknade amnen
Hitta amnen som namns i texter men saknar egen wiki-artikel.

### Inkonsekvenser
Hitta motsagelser eller inkonsekvent terminologi mellan artiklar.

### INDEX.md-kontroll
Kontrollera att alla artiklar finns i INDEX.md och att inga doda lankar finns.

3. **Presentera** resultatet:

```markdown
## Halsokontroll: [datum]

| Kontroll | Resultat |
|----------|---------|
| Brutna lankar | X |
| Orphans | X |
| Utan kopplingar | X |
| Saknade amnen | X |
| Inkonsekvenser | X |
| Wiki-halsa | Bra/Behover atgard/Kritisk |

### Atgardsforslag (prioriterat)
1. ...
```

4. **Spara** till `outputs/wiki-halsokontroll-{datum}.md`
5. **Logga** i `wiki/log.md`: `[DATUM] [LINT] Halsokontroll: X brutna, X orphans, X saknade`
