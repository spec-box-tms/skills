# SpecBox skills

Набор специализированных Codex skills для работы со спецификациями
[SpecBoxTMS](https://github.com/spec-box-tms).

Репозиторий оформлен как плагин `specbox`, поэтому skills доступны
с пространством имён `specbox:`.

## Skills

| Skill | Назначение |
| --- | --- |
| `specbox:create` | Инициализировать SpecBox в проекте |
| `specbox:extract` | Извлечь реализованные спецификации из кода |
| `specbox:validate` | Проверить формат спецификаций и показать покрытие тестами |
| `specbox:write-tests` | Написать совместимые со SpecBox автотесты |
| `specbox:review` | Проверить качество требований |
| `specbox:propose` | Описать планируемое поведение как `propose` |
| `specbox:apply` | Реализовать `propose` и преобразовать его в `assert` |

`propose` описывает черновик планируемого поведения и не связывается с
автотестами. После принятия `propose` становится `assert`, для него пишется
падающий тест, реализуется поведение и подтверждается проходящим тестом:

```text
propose → assert → RED-test → implement → GREEN-test → completed
```

`completed` — завершение workflow, а не отдельный ключ YAML. `assert` также
используется для уже существующего поведения, извлечённого из приложения.

Архитектурные решения и контракты skills описаны в
[docs/design.md](docs/design.md).

## Установка

Нужен Codex CLI. Плагин устанавливается напрямую из GitHub marketplace.

1. Добавьте marketplace:

   ```sh
   codex plugin marketplace add spec-box-tms/skills --ref main
   ```

2. Установите плагин и откройте новый task:

   ```sh
   codex plugin add specbox@specbox-tms
   codex plugin list
   ```

   В новом task будут доступны `specbox:create`,
   `specbox:extract` и остальные skills.

Для обновления marketplace после нового коммита:

```sh
codex plugin marketplace upgrade specbox-tms
codex plugin add specbox@specbox-tms
```

Плагин не задаёт имена YAML-файлов, структуру каталогов или тестовый раннер.

Формат SpecBoxTMS и команды CLI приведены в документации
[SpecBoxTMS.Sync](https://github.com/spec-box-tms/sync).
