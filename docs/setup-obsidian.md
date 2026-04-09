# Obsidian-setup

## Installera Obsidian

1. Ladda ner fran https://obsidian.md
2. Installera och starta

## Oppna projektet som vault

1. Klicka **"Open folder as vault"**
2. Navigera till din projektmapp
3. Klicka **"Open"**
4. Om Obsidian fragar om tillagg: **"Trust author and enable plugins"**

Du bor nu se Dashboard.md som startsida.

## Rekommenderade community plugins

Ga till **Settings -> Community plugins -> Browse** och installera:

| Plugin | Sok efter | Funktion |
|--------|-----------|----------|
| Obsidian Git | "Git" | Auto-synk med GitHub |
| Dataview | "Dataview" | Dynamiska tabeller |
| Excalidraw | "Excalidraw" | Rita diagram och begreppskartor |
| Templater | "Templater" | Kraftfullare templates |
| Enhancing Export | "Enhancing Export" | Exportera till Word (.docx) |
| Marp Slides | "Marp" | Presentationer fran markdown |

**Aktivera** varje plugin efter installation.

## Konfigurera Obsidian Git

Ga till **Settings -> Obsidian Git**:
- Auto pull interval: `5` (minuter)
- Auto push interval: `5`
- Pull on boot: **On**
- Push on backup: **On**

## Obsidian Web Clipper

Installera i din webblasare for att spara artiklar direkt till `raw/artiklar/`:
- [Chrome/Edge](https://chromewebstore.google.com/detail/obsidian-web-clipper/cnjifjpddelmedmihgijeibhnjfabmlf)
- [Firefox](https://addons.mozilla.org/en-US/firefox/addon/web-clipper-obsidian/)
- [Safari/iOS](https://apps.apple.com/us/app/obsidian-web-clipper/id6720708363)

## Kortkommandon

| Kortkommando | Funktion |
|-------------|----------|
| `Ctrl+O` | Snabbvaxla till fil |
| `Ctrl+P` | Kommandopalett |
| `Ctrl+G` | Graph View (se kopplingar) |
| `Ctrl+E` | Vaxla las/redigera-lage |
| `Ctrl+Shift+F` | Sok i alla filer |
| `[[` | Borja skriva en wiki-lank |

## Mobilsynk

1. Installera Obsidian fran App Store / Google Play
2. Installera Obsidian Git-plugin
3. Clone repot med din GitHub PAT (Personal Access Token)
4. Allt synkar automatiskt
