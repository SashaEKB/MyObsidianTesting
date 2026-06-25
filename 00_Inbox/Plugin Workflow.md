---
type: plugin-workflow
created: 2026-06-17
area: devops-linux
---

# Plugin Workflow

## Dataview

Автоматически собирает таблицы из заметок по `frontmatter`.

Где используется:

- [[Dashboard]]
- список занятий;
- список проектов;
- список ошибок;
- список шпаргалок.

DataviewJS отключен для безопасности. Обычный Dataview включен.

Пример:

```text
type: project
status: working
```

Потом Dataview может собрать все `type: project` в таблицу.

## Tasks

Плагин для задач внутри Markdown.

Пример задачи:

```text
- [ ] Повторить chmod #task
```

Пример задачи с датой:

```text
- [ ] Разобрать systemd #task 📅 2026-06-18
```

Команда:

```text
Ctrl+P -> Tasks: Create or edit task
```

Где использовать:

- в дневных занятиях;
- в проектных заметках;
- в Roadmap.

## Templater

Плагин для умных шаблонов.

Папка шаблонов:

```text
08_Templates
```

Команда:

```text
Ctrl+P -> Templater: Open Insert Template modal
```

Использовать для:

- Daily Lesson;
- Command Note;
- Error Note.

## QuickAdd

Плагин установлен на будущее.

Для чего пригодится:

- быстро создать заметку ошибки;
- быстро создать заметку команды;
- быстро создать дневное занятие.

Пока не настраиваем сложные actions вручную. Когда workflow стабилизируется, настроим QuickAdd под 2-3 конкретные команды.
