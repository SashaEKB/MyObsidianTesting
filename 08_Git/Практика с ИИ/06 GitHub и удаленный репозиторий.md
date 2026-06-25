# GitHub и удаленный репозиторий

Git — программа для контроля версий.

GitHub — сайт, где можно хранить Git-репозитории онлайн.

## Git и GitHub — не одно и то же

Git работает на твоем компьютере.

GitHub хранит копию репозитория в интернете.

Связь между ними называется `remote`, то есть удаленный репозиторий.

## Скопировать чужой репозиторий

```bash
git clone <url>
```

`git clone` скачивает репозиторий на компьютер.

`<url>` — ссылка на репозиторий.

## Посмотреть удаленные репозитории

```bash
git remote -v
```

Показывает, куда Git будет отправлять или откуда получать изменения.

Пример HTTPS-ссылки:

```text
https://github.com/SashaEKB/testing-GIT.git
```

Пример SSH-ссылки:

```text
git@github.com:SashaEKB/testing-GIT.git
```

Если ссылка начинается с `https://`, GitHub попросит логин и токен.

Если ссылка начинается с `git@github.com:`, GitHub будет использовать SSH-ключ.

## Добавить удаленный репозиторий

```bash
git remote add origin <url>
```

`origin` — стандартное имя основного удаленного репозитория.

Важно: `origin` — это не сам GitHub и не глобальное имя на весь компьютер.

`origin` — короткий ярлык для URL внутри конкретного Git-проекта.

Например, вместо длинной ссылки:

```text
https://github.com/SashaEKB/Git-TESTING.git
```

Git позволяет писать коротко:

```text
origin
```

Команда читается так:

```bash
git remote add origin https://github.com/SashaEKB/Git-TESTING.git
```

Смысл:

```text
Добавь удаленный репозиторий и назови его origin.
```

## Если репозиториев много

У каждого локального Git-проекта свой `origin`.

Пример:

```text
~/Desktop/Git        origin -> Git-TESTING
~/Desktop/MySite     origin -> MySite
~/Documents/App      origin -> App
```

Они не конфликтуют, потому что каждый `origin` хранится внутри своей папки `.git`.

Проверить, куда ведет `origin` в текущем проекте:

```bash
git remote -v
```

Главное правило: сначала зайди в нужную папку проекта, потом проверяй `git remote -v`.

## Зачем нужен upstream

`remote` отвечает на вопрос: куда отправлять изменения.

`upstream` отвечает на вопрос: с какой веткой на GitHub связана моя текущая локальная ветка.

Когда ты меняешь GitHub repository или первый раз отправляешь новую ветку, Git может написать:

```text
fatal: The current branch main has no upstream branch.
```

Это значит: локальная ветка `main` пока не связана с веткой `main` на GitHub.

Решение:

```bash
git push -u origin main
```

`-u` означает `--set-upstream`.

Эта команда делает две вещи:

1. Отправляет локальную ветку `main` в `origin`.
2. Запоминает связь `main` -> `origin/main`.

После этого можно писать короче:

```bash
git push
```

Проверить связь ветки:

```bash
git branch -vv
```

Если видишь `main [origin/main]`, значит связь есть.

## Изменить ссылку remote на SSH

```bash
git remote set-url origin git@github.com:SashaEKB/testing-GIT.git
```

`set-url` меняет адрес удаленного репозитория.

Это нужно, если репозиторий был подключен через HTTPS, а ты хочешь использовать SSH.

## Отправить коммиты на GitHub

```bash
git push -u origin main
```

`git push` отправляет локальные коммиты в удаленный репозиторий.

`-u` запоминает связь между твоей веткой `main` и веткой `main` на GitHub.

После этого обычно можно писать короче:

```bash
git push
```

## HTTPS и токен

GitHub больше не принимает обычный пароль от аккаунта для `git push`.

Если используешь HTTPS, вместо пароля нужен Personal Access Token.

Ошибка выглядит так:

```text
Password authentication is not supported for Git operations.
```

Смысл ошибки: пароль от GitHub вводить нельзя, нужен токен.

## SSH-ключи

SSH-ключ — это способ доказать GitHub, что это твой компьютер.

Есть два файла:

```text
id_ed25519      приватный ключ, никому не показывать
id_ed25519.pub  публичный ключ, добавить в GitHub
```

Создать ключ:

```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

`ssh-keygen` создает SSH-ключ.

`-t ed25519` выбирает современный тип ключа.

`-C` добавляет комментарий, обычно email.

Публичный ключ нужно добавить в GitHub:

```text
GitHub -> Settings -> SSH and GPG keys -> New SSH key
```

## Проверить SSH-доступ к GitHub

```bash
ssh -T git@github.com
```

Успешный ответ выглядит так:

```text
Hi SashaEKB! You've successfully authenticated, but GitHub does not provide shell access.
```

Это не ошибка.

Смысл: GitHub узнал твой ключ, но обычную консоль через SSH не дает. Для Git этого достаточно.

## Что у нас не работало

SSH зависал на подключении:

```text
Connecting to github.com ... port 22
```

Причина: порт `22` мог быть заблокирован сетью или провайдером.

Решение: подключить GitHub SSH через порт `443`.

Файл настройки:

```text
~/.ssh/config
```

Содержимое:

```sshconfig
Host github.com
  HostName ssh.github.com
  User git
  Port 443
  IdentityFile ~/.ssh/id_ed25519
```

После этого команда `git push` продолжает выглядеть обычно, но внутри SSH идет через порт `443`.

## Что получилось

После добавления ключа в GitHub и настройки порта `443` проверка прошла успешно:

```text
Hi SashaEKB! You've successfully authenticated, but GitHub does not provide shell access.
```

А `git push` ответил:

```text
Everything up-to-date
```

Смысл: подключение работает, а новых коммитов для отправки пока нет.

## Получить изменения

```bash
git pull
```

`git pull` скачивает изменения из удаленного репозитория и применяет их к текущей ветке.
