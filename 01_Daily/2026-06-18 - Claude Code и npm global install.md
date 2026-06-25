---
type: daily
date: 2026-06-18
topics:
  - linux
  - npm
  - claude-code
  - path
  - permissions
---

# 2026-06-18 - Claude Code и npm global install

> [!summary] Итог
> Разобрали, как установить Claude Code в Linux, почему `npm install -g` уперся в права доступа, и как безопасно перенести глобальные npm-пакеты в домашнюю директорию пользователя.

## Цель

- Понять, как поставить `Claude Code` на Linux.
- Разобрать ошибку `EACCES` при глобальной установке через `npm`.
- Настроить установку глобальных npm-пакетов без `sudo`.
- Понять роль переменной `PATH`.

## Что сделали

- Обсудили разницу между `Claude Code` отдельно и `OpenCode + Anthropic API`.
- Выбрали простой старт: использовать официальный `Claude Code` как CLI-инструмент.
- При установке через `npm install -g @anthropic-ai/claude-code` появилась ошибка прав.
- Разобрали, что `npm` пытался писать в системную папку `/usr/local/lib/node_modules`.
- Решили не использовать `sudo npm install -g`, а настроить пользовательский npm-prefix.
- Подготовили команды для установки глобальных npm-пакетов в `~/.npm-global`.

## Команды

Проверить shell:

```bash
echo $SHELL
```

Создать пользовательскую папку для глобальных npm-пакетов:

```bash
mkdir -p ~/.npm-global
```

Сказать `npm`, что глобальные пакеты нужно ставить туда:

```bash
npm config set prefix ~/.npm-global
```

Проверить текущий prefix:

```bash
npm config get prefix
```

Добавить папку с пользовательскими командами в `PATH` для `bash`:

```bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Если используется `zsh`, добавить в `~/.zshrc`:

```bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Установить Claude Code:

```bash
npm install -g @anthropic-ai/claude-code
```

Проверить установку:

```bash
claude --version
```

Запустить Claude Code:

```bash
claude
```

## Ошибки и решения

### `EACCES: permission denied, mkdir '/usr/local/lib/node_modules'`

Где встретилась:

```bash
npm install -g @anthropic-ai/claude-code
```

Текст ошибки:

```text
npm ERR! code EACCES
npm ERR! syscall mkdir
npm ERR! path /usr/local/lib/node_modules
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied, mkdir '/usr/local/lib/node_modules'
```

Причина:

- Флаг `-g` означает глобальную установку.
- По умолчанию `npm` пытался ставить пакет в системную директорию `/usr/local/lib/node_modules`.
- Обычный пользователь `kraz` не имеет права писать в эту директорию.

Решение:

```bash
mkdir -p ~/.npm-global
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
npm install -g @anthropic-ai/claude-code
```

Важно: `sudo npm install -g` лучше не использовать без необходимости, потому что npm-пакет будет выполняться с root-правами во время установки.

Отдельная заметка: [[06_Errors/npm EACCES permission denied usr local lib node_modules]]

## Что понял

- `npm install -g` ставит пакет так, чтобы команда была доступна из любого места.
- Системные директории вроде `/usr/local/lib/node_modules` защищены правами Linux.
- Для dev-инструментов безопаснее использовать пользовательскую директорию в `$HOME`.
- `PATH` определяет, где shell ищет команды.
- Если `claude` лежит в `~/.npm-global/bin`, эту папку нужно добавить в `PATH`.

## Что повторить

- Что такое права доступа в Linux.
- Что такое `$HOME`.
- Что такое `PATH`.
- Разницу между системной и пользовательской установкой программ.
- Почему `sudo` не нужно использовать автоматически.

## Следующий шаг

- Завершить установку `Claude Code`.
- Создать учебную папку `~/devops-learning`.
- Добавить `CLAUDE.md` с ролью Linux/DevOps-наставника.
- Запустить `claude` из учебной папки и начать первое практическое занятие.
