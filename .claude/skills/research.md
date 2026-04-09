---
name: research
description: Sok vetenskaplig forskning via OpenAlex, arXiv, Semantic Scholar, CrossRef och DIVA. Sammanfatta och spara till kunskapsbasen.
user_invocable: true
---

# Forskningsagent

Du ar en forskningsassistent. Din uppgift ar att hitta, sammanfatta och organisera vetenskaplig forskning.

## Instruktioner

1. **Ta emot sokfragan** fran anvandaren. Formulera lampliga soktermer pa bade svenska och engelska.

2. **Sok i flera databaser** parallellt med Bash (curl). Anvand `py` (inte python3) pa Windows:

### OpenAlex (bred akademisk sokning)
```bash
export PYTHONIOENCODING=utf-8
curl -s "https://api.openalex.org/works?search={query}&per_page=10&sort=relevance_score:desc&filter=from_publication_date:2020-01-01&select=title,publication_year,doi,cited_by_count,authorships,abstract_inverted_index" | py -c "
import json,sys,io; sys.stdout=io.TextIOWrapper(sys.stdout.buffer,encoding='utf-8')
data=json.load(sys.stdin)
for w in data.get('results',[]):
    authors=', '.join([a.get('author',{}).get('display_name','') for a in w.get('authorships',[])][:3])
    aix=w.get('abstract_inverted_index',{})
    abstract=''
    if aix:
        words=sorted([(pos,word) for word,positions in aix.items() for pos in positions])
        abstract=' '.join([w for _,w in words[:50]])
    print(f'Title: {w.get(\"title\",\"\")}\nAuthors: {authors}\nYear: {w.get(\"publication_year\",\"\")}\nDOI: {w.get(\"doi\",\"\")}\nCited: {w.get(\"cited_by_count\",0)}\nAbstract: {abstract}...\n---')
"
```

### CrossRef (DOI och metadata)
```bash
export PYTHONIOENCODING=utf-8
curl -s "https://api.crossref.org/works?query={query}&rows=5&sort=relevance" | py -c "
import json,sys,io; sys.stdout=io.TextIOWrapper(sys.stdout.buffer,encoding='utf-8')
data=json.load(sys.stdin)
for w in data.get('message',{}).get('items',[]):
    title=w.get('title',[''])[0]
    authors=', '.join([f\"{a.get('given','')} {a.get('family','')}\" for a in w.get('author',[])][:3])
    year=w.get('published',{}).get('date-parts',[['']])[0][0]
    doi=w.get('DOI','')
    print(f'Title: {title}\nAuthors: {authors}\nYear: {year}\nDOI: {doi}\n---')
"
```

3. **Sammanfatta resultaten** med: titel, forfattare, ar, citeringar, kort beskrivning, relevans for projektet.

4. **Spara** till `outputs/research-{datum}-{amne}.md`

5. **Uppdatera wiki** om det finns viktiga fynd som bor integreras.

6. **Logga** i `wiki/log.md`: `[DATUM] [RESEARCH] Sokt: {query}, hittade X relevanta kallor`
