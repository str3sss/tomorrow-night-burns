# План: VS Code тема-расширение «Tomorrow Night Burns»

## Context

Тема «Tomorrow Night Burns» отсутствует в Marketplace как расширение для VS Code —
существует только как iTerm2-схема (mbadolato/iTerm2-Color-Schemes). Пользователь
хочет получить именованную тему, которую видно в списке **Color Theme**, можно
переустановить и (опционально) опубликовать. Решение — собственное маленькое
расширение-тема: `package.json` c `contributes.themes` + один JSON с цветами.

Источник палитры (iTerm terminator .config):
- `palette` (ANSI 0–15): `#252525:#832e31:#a63c40:#d3494e:#fc595f:#df9395:#ba8586:#f5f5f5:#5d6f71:#832e31:#a63c40:#d2494e:#fc595f:#df9395:#ba8586:#f5f5f5`
- `background_color = #151515`, `foreground_color = #a1b0b8`, `cursor_color = #ff443e`

Решения из вопросов: **полноценное расширение** с прицелом на публикацию, но публикация
опциональна (аккаунт под вопросом); лицензия **MIT**; проект в
`~/Development/localDevelopment/tomorrow-night-burns-theme`.

## Расположение и структура проекта

Каталог: `~/Development/localDevelopment/tomorrow-night-burns-theme/`

```
tomorrow-night-burns-theme/
├── package.json
├── themes/
│   └── tomorrow-night-burns-color-theme.json
├── README.md
├── CHANGELOG.md
├── LICENSE                 # MIT
├── icon.png                # опц., 128x128 (нужен для красивой публикации)
├── .vscodeignore
└── .gitignore
```

## Шаг 1. package.json (манифест расширения)

Ключевые поля (версия engines взять пониже для совместимости):

```jsonc
{
  "name": "tomorrow-night-burns",
  "displayName": "Tomorrow Night Burns",
  "description": "Dark crimson VS Code theme ported from the iTerm2 'Tomorrow Night Burns' scheme.",
  "version": "0.0.1",
  "publisher": "PLACEHOLDER",          // для локального .vsix сойдёт любой; для публикации — реальный id
  "license": "MIT",
  "engines": { "vscode": "^1.70.0" },
  "categories": ["Themes"],
  "keywords": ["theme", "dark", "tomorrow", "red", "crimson"],
  "contributes": {
    "themes": [
      {
        "label": "Tomorrow Night Burns",
        "uiTheme": "vs-dark",
        "path": "./themes/tomorrow-night-burns-color-theme.json"
      }
    ]
  }
}
```

## Шаг 2. themes/tomorrow-night-burns-color-theme.json

Структура: `{ name, type: "dark", colors: {...}, tokenColors: [...] }`.
Остальные UI-ключи наследуются от `type: "dark"` — задаём только ядро.

### 2a. `colors` — workbench/UI (ядро)

```jsonc
{
  "editor.background": "#151515",
  "editor.foreground": "#a1b0b8",
  "editorCursor.foreground": "#ff443e",
  "editor.selectionBackground": "#832e3166",
  "editor.lineHighlightBackground": "#1f1f1f",
  "editorLineNumber.foreground": "#5d6f71",
  "editorLineNumber.activeForeground": "#d3494e",
  "editorWhitespace.foreground": "#2a2a2a",
  "editorIndentGuide.background1": "#252525",
  "editorIndentGuide.activeBackground1": "#5d6f71",

  "focusBorder": "#a63c40",
  "foreground": "#a1b0b8",
  "errorForeground": "#fc595f",

  "activityBar.background": "#101010",
  "activityBar.foreground": "#d3494e",
  "activityBarBadge.background": "#d3494e",
  "activityBarBadge.foreground": "#f5f5f5",

  "sideBar.background": "#181818",
  "sideBar.foreground": "#a1b0b8",
  "sideBarSectionHeader.background": "#101010",

  "list.activeSelectionBackground": "#832e31",
  "list.activeSelectionForeground": "#f5f5f5",
  "list.hoverBackground": "#252525",
  "list.inactiveSelectionBackground": "#252525",

  "statusBar.background": "#832e31",
  "statusBar.foreground": "#f5f5f5",
  "statusBar.noFolderBackground": "#101010",

  "titleBar.activeBackground": "#101010",
  "titleBar.activeForeground": "#a1b0b8",

  "editorGroupHeader.tabsBackground": "#1a1a1a",
  "tab.activeBackground": "#151515",
  "tab.inactiveBackground": "#1a1a1a",
  "tab.activeForeground": "#f5f5f5",
  "tab.inactiveForeground": "#5d6f71",
  "tab.activeBorderTop": "#d3494e",

  "panel.background": "#151515",
  "panelTitle.activeForeground": "#d3494e",

  "button.background": "#a63c40",
  "button.foreground": "#f5f5f5",
  "button.hoverBackground": "#d3494e",

  "input.background": "#1f1f1f",
  "input.border": "#5d6f71",
  "badge.background": "#d3494e",
  "badge.foreground": "#f5f5f5",
  "progressBar.background": "#d3494e",
  "scrollbarSlider.background": "#5d6f7133",
  "scrollbarSlider.hoverBackground": "#5d6f7155",

  // Терминал — здесь iTerm-палитра ложится 1:1
  "terminal.background": "#151515",
  "terminal.foreground": "#a1b0b8",
  "terminalCursor.foreground": "#ff443e",
  "terminal.ansiBlack": "#252525",
  "terminal.ansiRed": "#832e31",
  "terminal.ansiGreen": "#a63c40",
  "terminal.ansiYellow": "#d3494e",
  "terminal.ansiBlue": "#fc595f",
  "terminal.ansiMagenta": "#df9395",
  "terminal.ansiCyan": "#ba8586",
  "terminal.ansiWhite": "#f5f5f5",
  "terminal.ansiBrightBlack": "#5d6f71",
  "terminal.ansiBrightRed": "#832e31",
  "terminal.ansiBrightGreen": "#a63c40",
  "terminal.ansiBrightYellow": "#d2494e",
  "terminal.ansiBrightBlue": "#fc595f",
  "terminal.ansiBrightMagenta": "#df9395",
  "terminal.ansiBrightCyan": "#ba8586",
  "terminal.ansiBrightWhite": "#f5f5f5"
}
```

### 2b. `tokenColors` — синтаксис (раскладка по красному градиенту)

| Scope | Цвет | fontStyle |
|---|---|---|
| `comment`, `punctuation.definition.comment` | `#5d6f71` | italic |
| `string`, `punctuation.definition.string` | `#ba8586` | — |
| `constant.numeric`, `constant.language`, `constant.character` | `#fc595f` | — |
| `keyword`, `storage`, `storage.type`, `keyword.control` | `#d3494e` | — |
| `entity.name.function`, `support.function`, `meta.function-call` | `#df9395` | — |
| `entity.name.type`, `entity.name.class`, `support.type`, `support.class` | `#fc595f` | — |
| `variable`, `variable.other`, `meta.definition.variable` | `#a1b0b8` | — |
| `variable.parameter` | `#ba8586` | italic |
| `entity.name.tag` (HTML/JSX) | `#d3494e` | — |
| `entity.other.attribute-name` | `#df9395` | italic |
| `keyword.operator`, `punctuation` | `#8a9a9c` | — |
| `markup.heading` | `#fc595f` | bold |
| `invalid`, `invalid.illegal` | `#ff443e` | — |

(Опц.) добавить `"semanticHighlighting": true` без `semanticTokenColors` — тогда
семантика подсветит поверх TextMate по типам, оставаясь в тех же цветах.

## Шаг 3. Сопутствующие файлы

- **LICENSE** — MIT, автор из git-конфига (Dmitry Shmelev), год 2026.
- **README.md** — скриншот/описание, откуда портирована палитра (ссылка на iTerm2-Color-Schemes), как ставить.
- **CHANGELOG.md** — `## 0.0.1 — Initial release`.
- **.vscodeignore** — исключить `.gitignore`, исходники скриншотов и пр. из пакета.
- **.gitignore** — `node_modules`, `*.vsix`.
- `git init` в каталоге темы (отдельный репозиторий, не трогаем underwriters).

## Шаг 4. Проверка (dev-loop)

1. Открыть каталог темы в VS Code, нажать **F5** → откроется *Extension Development Host*.
2. В нём: `Cmd+K Cmd+T` → выбрать **Tomorrow Night Burns**.
3. Открыть файлы разных языков (TS/TSX, JSON, Markdown, shell) + встроенный терминал —
   проверить читаемость и что ANSI-цвета терминала совпадают с iTerm.
4. Правки JSON применяются на лету (или `Developer: Reload Window` в dev-хосте).

Быстрая валидация JSON без запуска: `npx --yes jsonlint themes/*.json` или
`node -e "require('./themes/tomorrow-night-burns-color-theme.json')"`.

## Шаг 5. Локальная установка (.vsix)

```bash
cd ~/Development/localDevelopment/tomorrow-night-burns-theme
pnpm dlx @vscode/vsce package        # → tomorrow-night-burns-0.0.1.vsix
```
Затем в VS Code: `Cmd+Shift+P` → **Extensions: Install from VSIX…** → выбрать файл.
Либо CLI: `code --install-extension tomorrow-night-burns-0.0.1.vsix`.

> `vsce package` предупредит про отсутствие `repository`/иконки — это warnings, сборка
> проходит. Для локального `.vsix` `publisher` может быть плейсхолдером.

## Шаг 6. Публикация (опционально, отложено)

Требует реального `publisher`:
- **VS Code Marketplace**: publisher через Azure DevOps + PAT → `vsce login <publisher>` → `vsce publish`.
- **Open VSX** (для VSCodium/Cursor): `ovsx publish` c токеном.
Обновить в `package.json`: `publisher`, `repository`, добавить `icon.png`. Лицензия MIT — ок.
Делать только когда пользователь заведёт аккаунт.

## Заметки / риски

- Палитра почти монохромная (красный градиент), поэтому синтаксис по умолчанию
  низкоконтрастный — это соответствует эстетике «burns», но при желании поднять
  различимость можно развести keywords/strings/functions по светлоте (правится в 2b).
- Все правки — вне репозитория `underwriters`; текущий проект не затрагивается.
