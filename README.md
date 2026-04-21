# Zed + Codex workaround (apply/revert fix)

Фикс для проблемы, когда в Zed агент Codex не показывает/не применяет `Keep/Reject` (или не откатывает правки).

## Что работает

Пин на `@zed-industries/codex-acp@0.10.0`.

## Вариант 1: быстро через npx

```json
{
  "agent_servers": {
    "Codex-CLI": {
      "type": "custom",
      "command": "npx",
      "args": ["-y", "@zed-industries/codex-acp@0.10.0"]
    }
  }
}
```

## Вариант 2: стабильный локальный пин (рекомендуется)

1. Установить пакет локально:

```bash
mkdir -p ~/.local/codex-acp-0.10.0
cd ~/.local/codex-acp-0.10.0
npm init -y
npm i --save-exact @zed-industries/codex-acp@0.10.0
```

2. Прописать абсолютный путь к бинарнику в Zed `settings.json`:

```json
{
  "agent_servers": {
    "Codex-CLI": {
      "type": "custom",
      "command": "/Users/<you>/.local/codex-acp-0.10.0/node_modules/.bin/codex-acp-darwin-arm64",
      "args": []
    }
  }
}
```

## Где править настройки Zed

- macOS/Linux: `~/.config/zed/settings.json`

## Проверка

- Перезапустить Zed (или `Reload Window`).
- Открыть правку агента и убедиться, что доступны действия `Keep/Reject`.

## Troubleshooting

- Симптом: `keep/reject` не появляются.
  Фикс: проверь, что используется именно `Codex-CLI` с `@zed-industries/codex-acp@0.10.0` или локальный бинарник `0.10.0`, затем перезапусти Zed.
- Симптом: `command not found: gh`.
  Фикс: установить GitHub CLI (`brew install gh`) и войти (`gh auth login`).
- Симптом: `current directory is not a git repository`.
  Фикс: в папке проекта выполнить `git init -b main`, затем `git add . && git commit -m "init"`.
- Симптом: путь к локальному бинарнику не работает.
  Фикс: проверить наличие файла `~/.local/codex-acp-0.10.0/node_modules/.bin/codex-acp-darwin-arm64` и права на запуск (`chmod +x` при необходимости).
- Симптом: после правки `settings.json` ничего не изменилось.
  Фикс: убедиться, что редактируется активный файл `~/.config/zed/settings.json` и нет конкурирующей записи в другом профиле/инстансе Zed.
- Симптом: `args` остались от `npx` при локальном `command`.
  Фикс: для локального бинарника ставить `\"args\": []`, иначе конфиг смешивает два режима запуска.

## Примечание

Это временный workaround до фикса в новых версиях `codex-acp`.
