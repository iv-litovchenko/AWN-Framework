# AGENTS.SETTINGS.md

Системные настройки поведения агента для этого vault.

**Приоритет применения:**
1. Явная инструкция пользователя в текущем запросе
2. Активная настройка из этого файла
3. Умолчания из `AGENTS.md`

Если настройка не нужна — снять галочку (`[ ]`) или установить `value: false`.

---

## Активные настройки

- [ ] `links.markdown_compatible` — стандартный Markdown вместо `[[wikilinks]]`
- [x] `naming.camel_case` — CamelCase для новых файлов и папок

---

## Реестр (для агента)

```yaml
settings:
  links.markdown_compatible:
    value: true
    scope: rendering
    description: "Использовать стандартный Markdown для ссылок и изображений вместо [[wiki-синтаксиса]]. Совместимо с GitHub."

  naming.camel_case:
    value: true
    scope: naming
    description: "При создании новых файлов и папок использовать CamelCase, если пользователь не попросил иначе."
```

---

## Справка: что значит `links.markdown_compatible`

| Элемент | Obsidian wiki | Markdown (активно) |
|---------|--------------|-------------------|
| Изображение | `![[photo.png]]` | `![фото](photo.png)` |
| Ссылка на файл | `[[README]]` | `[текст](README.md)` |
| Якорь | `[[README#раздел]]` | `[раздел](README.md#раздел)` |

В Obsidian: Settings → Files and links → выключить **Use [[Wikilinks]]**, формат → `Relative path to file`.

---

## Как добавить настройку

1. Добавить строку в «Активные настройки» (`- [x] key — описание`)
2. Добавить запись в YAML-блок с полями `value`, `scope`, `description`
3. Обновить дату в git-коммите или в `AWN-UPDATED` если файл станет нодой
