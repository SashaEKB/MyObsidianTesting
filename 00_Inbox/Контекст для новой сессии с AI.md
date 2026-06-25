---
type: ai-context
created: 2026-06-17
last_updated: 2026-06-18
purpose: restore-context-for-new-session
---

# Контекст для новой сессии с AI

> [!summary] Как использовать
> Если новая сессия с AI не помнит прошлую работу, сначала попросить: "Прочитай файл `00_Inbox/Контекст для новой сессии с AI.md` в DevOps-Linux". После этого AI должен восстановить стиль работы, проекты и правила ведения заметок.

## Пользователь

- Пользователь Linux: `kraz`.
- ОС: Ubuntu/Linux.
- Основные цели: изучить Linux, DevOps, терминал, английский для IT и практическую работу с инструментами.
- Стиль обучения: пошагово, практично, коротко, с объяснением команд простым языком.
- Пользователь часто диктует голосом через Voicer, поэтому текст может быть разговорным и с ошибками распознавания.

## Как AI должен помогать

- Действовать как наставник и инженер-практик.
- Не просто отвечать, а помогать строить систему знаний.
- После практической работы фиксировать результат в Obsidian.
- Для каждой темы желательно записывать: цель, что сделали, команды, ошибки, решения, выводы, следующий шаг.
- Если задача требует действий в файловой системе, сначала проверить текущие файлы и не перетирать чужие изменения.

## Главный vault Linux/DevOps

```text
/home/kraz/Documents/DevOps-Linux
```

Главная страница:

```text
Home.md
```

Структура:

```text
00_Inbox/
01_Daily/
02_Linux/
03_Terminal/
04_DevOps/
05_Projects/
06_Errors/
07_Cheatsheets/
08_Templates/
09_Archive/
```

## Как вести DevOps-Linux

Новые занятия писать в:

```text
01_Daily/YYYY-MM-DD - Тема занятия.md
```

Проекты писать в:

```text
05_Projects/
```

Ошибки и решения писать в:

```text
06_Errors/
```

Команды и короткие шпаргалки писать в:

```text
07_Cheatsheets/
```

## Когда обновлять этот файл

AI должен сам предлагать обновить этот файл:

- после завершения крупной настройки;
- после появления нового постоянного проекта;
- после изменения структуры vault;
- после добавления нового workflow обучения;
- после важных решений, которые пригодятся в будущих сессиях;
- в конце длинной сессии, если было много изменений.

Практическое правило: если после сессии новый AI без контекста не сможет быстро продолжить работу, этот файл нужно обновить.

## Что уже настроено

### Ubuntu, GNOME, NVIDIA

- Проверен NVIDIA-драйвер через `nvidia-smi`.
- Выяснено, что GNOME на `Wayland` работает заметно плавнее, чем на `X11`.
- Причина лагов на X11: NVIDIA + GNOME + мониторы с разной частотой обновления.

### Voicer

Проект:

```text
/home/kraz/Desktop/Voicer
```

Что делает:

- удержание `F8` начинает запись;
- отпускание `F8` запускает распознавание;
- текст копируется и вставляется через `Ctrl+Shift+V`;
- используется `faster-whisper`;
- запуск на GPU: `cuda`, `float16`, модель `medium`;
- добавлен фильтр случайных вставок: `min_rms = 0.0015`.

Важные файлы:

```text
voicer.py
run-voicer.sh
run-voicer-background.sh
stop-voicer.sh
setup-uinput.sh
```

Важные темы из настройки Voicer:

- `venv`;
- `pip`;
- `chmod +x`;
- `.desktop` файлы;
- `groups`;
- `sudo usermod -aG input $USER`;
- `/dev/input`;
- `/dev/uinput`;
- `udev`;
- `LD_LIBRARY_PATH`;
- `nvidia-smi`.

### Claude Code и npm

- Пользователь хочет использовать Claude Code как Linux/DevOps-наставника в терминале.
- При установке `npm install -g @anthropic-ai/claude-code` возникла ошибка `EACCES` на `/usr/local/lib/node_modules`.
- Решение выбрано безопасное: не использовать `sudo npm install -g`, а настроить пользовательский npm-prefix.
- Рабочая схема:

```bash
mkdir -p ~/.npm-global
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
npm install -g @anthropic-ai/claude-code
```

- Если shell `zsh`, вместо `~/.bashrc` использовать `~/.zshrc`.
- Дневная заметка: `01_Daily/2026-06-18 - Claude Code и npm global install.md`.
- Ошибка: `06_Errors/npm EACCES permission denied usr local lib node_modules.md`.

## English vault

Отдельный vault для английского:

```text
/home/kraz/Documents/EnglishPractice
```

Цель:

- правила английского простыми словами;
- карточки слов и фраз;
- практика RU -> EN и EN -> RU;
- упражнения, которые AI создаёт под изученные правила;
- прогресс и баллы.

Главный плагин для карточек:

```text
Spaced Repetition
```

Формат карточек:

```text
Question::Answer
Question:::Answer
```

`::` - обычная карточка. `:::` - двусторонняя карточка.

Подготовленные deck-файлы:

```text
02_Cards/IT Starter Deck.md
02_Cards/Grammar Starter Deck.md
```

Важно: если пользователь говорит про "карты" или "карточки", вероятнее всего он имеет в виду именно интерактивные flashcards через `Spaced Repetition`, а не обычные таблицы Markdown.

Как работать:

1. Пользователь изучает правило.
2. Просит AI: "Сделай практические задания".
3. AI создаёт набор упражнений в `03_Practice/`.
4. Пользователь отвечает.
5. AI проверяет, объясняет ошибки и обновляет прогресс.

## Рекомендованные Obsidian плагины

Плагины уже установлены и базово настроены.

Dashboard:

```text
Dashboard.md
```

Plugin workflow note:

```text
00_Inbox/Plugin Workflow.md
```

Для EnglishPractice:

- `Spaced Repetition` - главный плагин карточек.
- `Dataview` - таблицы и прогресс.
- `Templater` - шаблоны практики.
- `QuickAdd` - позже, быстрые команды создания карточек/практики.

Для DevOps-Linux:

- `Dataview` - установлен, используется для Dashboard и автоматических таблиц; DataviewJS отключен для безопасности.
- `Tasks` - установлен, используется для задач обучения и запросов задач.
- `Templater` - установлен, папка шаблонов `08_Templates`.
- `QuickAdd` - установлен, но actions пока не настроены; использовать позже, когда появятся стабильные повторяющиеся сценарии.

## Следующие направления DevOps

В `04_DevOps/DevOps Roadmap.md` нужно постепенно развернуть отдельные гиды:

- Docker Guide;
- Git Guide;
- Networking Guide;
- Linux Services/systemd Guide;
- CI/CD Guide;
- Kubernetes Guide;
- Ansible Guide.

Каждый гид лучше вести короткими практическими блоками: понятие, команда, пример, ошибка, проверка.
