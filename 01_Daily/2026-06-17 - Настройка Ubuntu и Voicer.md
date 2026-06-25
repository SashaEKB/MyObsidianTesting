---
type: daily
date: 2026-06-17
topics:
  - linux
  - nvidia
  - wayland
  - python
  - voicer
  - obsidian
---

# 2026-06-17 - Настройка Ubuntu и Voicer

> [!summary] Итог дня
> Настроили Ubuntu под комфортную работу, разобрались с NVIDIA/Wayland, сделали голосовую диктовку Voicer по клавише `F8`, включили GPU CUDA и начали базу знаний в Obsidian.

## Цель

- Проверить, нормально ли работает NVIDIA-драйвер.
- Разобраться, почему GNOME тормозил на X11.
- Настроить голосовую диктовку на Linux.
- Сделать запуск Voicer удобным, без ручной активации `.venv`.
- Начать вести конспекты Linux/DevOps в Obsidian.

## Что сделали

- Проверили NVIDIA через `nvidia-smi`.
- Перешли с `X11` на `Wayland`, и GNOME стал работать плавнее.
- Создали проект `Voicer` на рабочем столе.
- Настроили Python `.venv`.
- Установили `faster-whisper`, `sounddevice`, `evdev`.
- Сделали диктовку: удерживаешь `F8`, говоришь, отпускаешь, текст распознается.
- Настроили вставку в терминал через `Ctrl+Shift+V`.
- Добавили запуск через `.desktop` ярлыки.
- Включили CUDA/GPU для модели `medium`.
- Добавили фильтр случайных вставок по длительности и громкости `RMS`.

## Важные команды

```bash
nvidia-smi
```

Показывает состояние NVIDIA-драйвера, видеокарту, процессы на GPU и использование VRAM.

```bash
echo $XDG_SESSION_TYPE
```

Показывает тип графической сессии: `x11` или `wayland`.

```bash
python3 -m venv .venv
```

Создает виртуальное окружение Python в папке проекта.

```bash
source .venv/bin/activate
```

Активирует виртуальное окружение в текущем терминале.

```bash
python -m pip install -r requirements.txt
```

Ставит Python-зависимости из файла `requirements.txt`.

```bash
chmod +x run-voicer.sh
```

Дает файлу право на запуск как программе.

```bash
sudo usermod -aG input $USER
```

Добавляет пользователя в группу `input`, чтобы программа могла читать клавиатуру через `/dev/input`.

```bash
sudo /home/kraz/Desktop/Voicer/setup-uinput.sh
```

Настраивает доступ к `/dev/uinput`, чтобы `ydotool` мог отправлять нажатия клавиш.

## Ошибки и решения

### GNOME тормозил на X11

Причина: связка `NVIDIA + GNOME + X11 + мониторы с разной частотой` может давать неровную плавность.

Решение: перейти на `Ubuntu on Wayland` на экране входа.

### `evdev` не установлен

Ошибка:

```text
Не установлен пакет evdev
```

Решение:

```bash
python -m pip install -r requirements.txt
```

### Нет доступа к клавиатуре

Причина: Linux защищает устройства ввода в `/dev/input`.

Решение:

```bash
sudo usermod -aG input $USER
```

После этого нужен полный `Log Out` и вход обратно.

### `ydotool` не мог открыть `/dev/uinput`

Ошибка:

```text
failed to open uinput device
```

Решение: создали `setup-uinput.sh`, который добавляет udev-правило для группы `input`.

### CUDA не находила `libcublas.so.12`

Ошибка:

```text
Library libcublas.so.12 is not found or cannot be loaded
```

Решение: поставили CUDA runtime библиотеки в `.venv`:

```bash
python -m pip install nvidia-cublas-cu12 nvidia-cudnn-cu12
```

И добавили их пути в `LD_LIBRARY_PATH` внутри `run-voicer.sh`.

## Что понял

- Wayland на современной NVIDIA может работать лучше X11 для GNOME.
- `.venv` нужен, чтобы зависимости проекта не смешивались с системой.
- В Linux доступ к клавиатуре, микрофону и виртуальному вводу контролируется правами.
- `nvidia-smi` помогает понять, реально ли процесс работает на GPU.
- Obsidian хранит заметки как обычные `.md` файлы.

## Что повторить

- Что такое `venv`.
- Что такое `PATH` и `LD_LIBRARY_PATH`.
- Чем отличаются `Wayland` и `X11`.
- Что такое группы пользователей в Linux.
- Что такое `/dev/input`, `/dev/uinput`, `udev`.

## Следующий шаг

- Привести Obsidian к удобному виду.
- Начать вести ежедневные учебные заметки.
- Постепенно разбирать Linux-команды, которые уже использовались.
