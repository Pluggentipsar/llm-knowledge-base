# Dagligt arbetsflode

## Morgon

1. Oppna Obsidian - allt synkas automatiskt fran GitHub
2. Kolla Dashboard for oversikt
3. Kolla `raw/inbox/` for nytt material som behover bearbetas

## Under dagen

### Nar du hittar nagot intressant

| Vad | Hur |
|-----|-----|
| Webbartikel | Obsidian Web Clipper -> `raw/artiklar/` |
| Vetenskapligt paper | Zotero Connector -> Zotero |
| YouTube-video | `/capture https://youtube.com/...` |
| LinkedIn-inlagg | `/capture https://linkedin.com/...` |
| Snabb tanke | `/capture Min tanke om...` |
| PDF/Word-dokument | `/ingest dokument.pdf` |

### Nar du vill fordjupa dig

```
/research "ditt sokord"      # Sok i vetenskapliga databaser
/wiki kompilera              # Integrera nytt material i kunskapsbasen
/halsokontroll               # Kolla wiki-kvalitet
```

## Kvall

Obsidian Git pushar automatiskt till GitHub. Allt ar synkat.

## Veckovis

Kor `/halsokontroll` for att hitta:
- Brutna lankar
- Artiklar utan kopplingar
- Saknade amnen
- Inkonsekvenser

## Tips

1. **Dumpa forst, organisera sedan.** Lagg allt i `raw/` utan att tanka pa struktur. AI:n organiserar.
2. **Lat AI:n skota wikin.** Du laser och navigerar i Obsidian, AI:n skriver.
3. **Stall fragor mot wikin.** Nar du har 10+ artiklar, borja fraga: "Vad vet vi om X?"
4. **Fila tillbaka outputs.** Bra svar fran `/research` kan integreras tillbaka i wikin.
5. **Graph View ar din van.** Ctrl+G i Obsidian visar hur allt hanger ihop.
