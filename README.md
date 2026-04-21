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

## Примечание

Это временный workaround до фикса в новых версиях `codex-acp`.
