---
type: project
status: working
topics:
  - python
  - linux
  - cuda
  - speech-to-text
---

# Voicer на Ubuntu

## Что это

Локальная голосовая диктовка на Ubuntu: удерживаешь `F8`, говоришь, отпускаешь, текст распознается и вставляется в активное окно.

## Где лежит проект

```text
/home/kraz/Desktop/Voicer
```

## Как запустить с терминалом

```bash
/home/kraz/Desktop/Voicer/run-voicer.sh
```

## Как запустить без терминала

```bash
/home/kraz/Desktop/Voicer/run-voicer-background.sh
```

## Как остановить

```bash
/home/kraz/Desktop/Voicer/stop-voicer.sh
```

## Текущий режим

```text
model: medium
device: cuda
compute_type: float16
hotkey: F8
paste: Ctrl+Shift+V
min_rms: 0.0015
```

## Как проверить GPU

```bash
nvidia-smi
```

Если Voicer работает на GPU, в списке процессов должен быть Python с типом `C` и использованием VRAM.
