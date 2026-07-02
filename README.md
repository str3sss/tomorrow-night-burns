# Tomorrow Night Burns

Тёмная кримсоновая тема для VS Code, портированная из iTerm2-схемы
[**Tomorrow Night Burns**](https://github.com/mbadolato/iTerm2-Color-Schemes/blob/master/terminator/Tomorrow%20Night%20Burns.config)
(коллекция [mbadolato/iTerm2-Color-Schemes](https://github.com/mbadolato/iTerm2-Color-Schemes)).

Почти монохромная палитра в оттенках красного/угольного с прохладно-серым текстом.
Цвета ANSI-терминала совпадают 1:1 с исходной iTerm-схемой.

## Палитра

| Роль | Hex |
|---|---|
| Фон | `#151515` |
| Текст | `#a1b0b8` |
| Курсор | `#ff443e` |
| Комментарии / muted | `#5d6f71` |
| Keywords / акценты | `#d3494e` |
| Числа / типы / ошибки | `#fc595f` |
| Функции / атрибуты | `#df9395` |
| Строки | `#ba8586` |

## Установка (локально)

```bash
pnpm dlx @vscode/vsce package
code --install-extension tomorrow-night-burns-0.0.1.vsix
```

Либо: `Cmd+Shift+P` → **Extensions: Install from VSIX…**.

## Активация

`Cmd+K Cmd+T` → **Tomorrow Night Burns**.

## Разработка

Открыть папку в VS Code, нажать **F5** → в *Extension Development Host*
выбрать тему через `Cmd+K Cmd+T`. Правки JSON применяются на лету.

## Лицензия

MIT.
