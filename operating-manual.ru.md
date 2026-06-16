# Использование системы

## Назначение

Система предназначена для ведения квалификационных репозиториев по отдельным техническим направлениям.

Каждый репозиторий содержит:

- roadmap изучаемой области;
- единый реестр задач;
- реализации задач;
- исследования и заметки по задачам.

Система обеспечивает:

- централизованное управление задачами;
- автоматическую генерацию структуры задач;
- единый способ запуска реализаций;
- синхронизацию файловой структуры с реестром задач.

---

# Структура репозитория

```txt
.
├── README.md
├── ROADMAP.md
├── TRACKER.md
├── task-list.require.json
├── package.json
├── tsconfig.base.json
├── scripts
│   ├── sync-tasks.mjs
│   └── execute-task.mjs
├── implements
│   └── ...
└── research
    ├── index.md
    └── ...
```

---

# Назначение файлов

## README.md

Описание репозитория.

Содержит:

- цель репозитория;
- область квалификации;
- используемые технологии;
- правила работы.

---

## ROADMAP.md

Содержит перечень тем и направлений развития внутри репозитория.

Пример:

```md
# Roadmap

## Runtime

- Event Loop
- Microtasks
- Worker Threads
- Streams

## Memory

- Heap
- Garbage Collector
- Memory Leaks
```

Roadmap отражает направление развития, но не является списком задач.

---

## TRACKER.md

Единый реестр задач.

Пример:

```md
# Tracker

| ID  | Status | Task              | Implementation                     | Research                         |
| --- | ------ | ----------------- | ---------------------------------- | -------------------------------- |
| 001 | [x]    | Event Loop Phases | ./implements/001_event_loop_phases | ./research/001_event_loop_phases |
| 002 | [ ]    | Worker Threads    | —                                  | —                                |
```

Правила:

- `[ ]` — задача не выполнена;
- `[x]` — задача выполнена;
- после завершения задачи должны быть указаны ссылки на реализацию и исследование.

TRACKER является единственным источником информации о состоянии задач.

---

## task-list.require.json

Содержит список обязательных задач.

Пример:

```json
["001_event_loop_phases", "002_worker_threads", "003_memory_profiling"]
```

Правила:

- идентификатор задачи должен быть уникальным;
- идентификатор начинается с трехзначного номера;
- номер является постоянным и не изменяется.

---

# Синхронизация задач

После изменения файла:

```txt
task-list.require.json
```

необходимо выполнить:

```bash
npm run tasks:sync
```

---

## Создание новой задачи

Пример:

```json
["001_event_loop_phases", "002_worker_threads"]
```

Добавляется новая запись:

```json
["001_event_loop_phases", "002_worker_threads", "003_memory_profiling"]
```

После запуска:

```bash
npm run tasks:sync
```

будут автоматически созданы:

```txt
implements/
└── 003_memory_profiling
    ├── README.md
    ├── execute.sh
    ├── tsconfig.json
    └── src
        └── index.ts

research/
└── 003_memory_profiling
    └── index.md
```

---

## Переименование задачи

Если название задачи изменяется:

Было:

```json
["003_memory_profiling"]
```

Стало:

```json
["003_nodejs_memory_profiling"]
```

После выполнения:

```bash
npm run tasks:sync
```

директории будут автоматически переименованы:

```txt
implements/
└── 003_nodejs_memory_profiling

research/
└── 003_nodejs_memory_profiling
```

---

## Удаление задачи

Если задача удаляется из:

```txt
task-list.require.json
```

то после запуска:

```bash
npm run tasks:sync
```

соответствующие директории будут удалены:

```txt
implements/<task>
research/<task>
```

---

# Выполнение исследования

Исследование оформляется в:

```txt
research/<task>/index.md
```

Пример:

```md
# Event Loop Phases

## Sources

- Node.js Docs
- libuv Docs

## Notes

Описание механизма работы фаз Event Loop.
```

Исследование выполняется до или во время реализации задачи.

---

# Выполнение реализации

Код задачи размещается в:

```txt
implements/<task>/src
```

Основная точка входа:

```txt
src/index.ts
```

Допускается создание дополнительной структуры:

```txt
src/
├── index.ts
├── benchmark.ts
├── examples
└── helpers
```

---

# Настройка запуска задачи

Каждая задача содержит собственный скрипт:

```txt
execute.sh
```

Пример:

```bash
#!/usr/bin/env bash

set -e

npx --no-install tsx src/index.ts
```

Допускается любая реализация запуска.

Например:

```bash
npm run dev
```

или

```bash
node dist/index.js
```

Главное требование:

```txt
execute.sh является единственной точкой запуска задачи.
```

---

# Запуск задачи

Для запуска используется общий интерфейс.

Формат:

```bash
npm run execute -- <ID>
```

Пример:

```bash
npm run execute -- 001
```

Алгоритм:

1. Выполняется поиск директории в `implements`.
2. Выполняется поиск директории, начинающейся с указанного номера.
3. Выполняется запуск файла `execute.sh`.
4. Вывод задачи отображается в терминале.

---

# Завершение задачи

После выполнения необходимо:

1. Заполнить исследование.

```txt
research/<task>/index.md
```

2. Завершить реализацию.

```txt
implements/<task>
```

3. Обновить запись в TRACKER.

Было:

```md
| 001 | [ ] | Event Loop Phases | — | — |
```

Стало:

```md
| 001 | [x] | Event Loop Phases | ./implements/001_event_loop_phases | ./research/001_event_loop_phases |
```

На этом жизненный цикл задачи считается завершенным.
