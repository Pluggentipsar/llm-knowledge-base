# Verktyg - Installation

## Obligatoriska

### Git
Versionshantering och synk med GitHub.

```bash
winget install Git.Git
```
Eller ladda ner fran https://git-scm.com/download/win

### Python 3.10+
Kravs for markitdown.

```bash
winget install Python.Python.3
```
**Viktigt:** Kryssa i "Add Python to PATH" under installationen.

### markitdown
Konverterar PDF, Word, PowerPoint, Excel, HTML till markdown.

```bash
pip install "markitdown[all]"
```

## Rekommenderade

### Pandoc
Export fran markdown till Word-dokument.

```bash
winget install JohnMacFarlane.Pandoc
```

### GitHub CLI
Interagera med GitHub fran terminalen.

```bash
winget install GitHub.cli
gh auth login
```

### Zotero (for akademiska projekt)
Referenshantering for vetenskapliga kallor.

```bash
winget install DigitalScholar.Zotero
```

Installera aven:
1. [BetterBibTeX](https://retorque.re/zotero-better-bibtex/installation/) - battre citekeys
2. [Zotero Connector](https://www.zotero.org/download/connectors) - spara papers fran webblasaren

## Verifiera

```bash
git --version          # git version X.X.X
py --version           # Python 3.XX
pandoc --version       # pandoc X.X.X
```
