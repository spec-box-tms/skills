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
| `specbox:review` | Проверить качество требований по Карлу Вигерсу |
| `specbox:propose` | Описать планируемое поведение как `propose` |
| `specbox:apply` | Реализовать `propose` и преобразовать его в `assert` |

`assert` означает реализованное поведение приложения. `propose` имеет ту же
структуру, но описывает ещё не реализованное поведение. Наличие автотеста —
отдельная характеристика и не определяет тип записи.

Архитектурные решения и контракты skills описаны в
[docs/design.md](docs/design.md).

## Установка

Нужен Codex CLI. Плагин устанавливается из personal marketplace.

1. Поместите этот каталог в `~/plugins/specbox`:

   ```sh
   mkdir -p ~/plugins
   cp -R /path/to/spec-box-tms/skill ~/plugins/specbox
   ```

2. Если файла `~/.agents/plugins/marketplace.json` ещё нет, создайте его:

   ```json
   {
     "name": "personal",
     "interface": { "displayName": "Personal" },
     "plugins": [
       {
         "name": "specbox",
         "source": { "source": "local", "path": "./plugins/specbox" },
         "policy": { "installation": "AVAILABLE", "authentication": "ON_INSTALL" },
         "category": "Productivity"
       }
     ]
   }
   ```

   Если файл уже есть, сохраните его содержимое и добавьте в массив `plugins`
   только объект `specbox` из примера. Запомните значение поля `name`.

3. Установите плагин и откройте новый task:

   ```sh
   codex plugin add specbox@personal
   codex plugin list
   ```

   Если marketplace называется не `personal`, подставьте его значение вместо
   `personal`. В новом task будут доступны `specbox:create`,
   `specbox:extract` и остальные skills.

Плагин не задаёт имена YAML-файлов, структуру каталогов или тестовый раннер.

Формат SpecBoxTMS и команды CLI приведены в документации
[SpecBoxTMS.Sync](https://github.com/spec-box-tms/sync).
