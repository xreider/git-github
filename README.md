# Привет, Мир!

## Стартовая настройка

**git config --global user.name xreider**

**git config --global user.email xreider@...**

можно ещё --local, --system

Сначала отправляем файл в staging area, а только потом в репозиторий

**git status**

**git init**

**git add index.html**

**git add .**

**git commit** - открывает файл COMMIT_EDITMSG где надо указать в начале название коммита. В первой строке идёт заголовок и не ставится точка. Ниже можно указывать дополнения

**git commit -m "Added welcome scripts"**

**git config user.name**

**git config user.email**

**git config --list**

**git config --list --global**

**git restore --staged < file >**

## Commit early. Commit often.

Делать коммиты по каждой микро-задаче

## Внесение отдельных строчек

**git add -p index.html**

## Добавляем общие файлы для .gitignore

**git config --global core.excludesfile ~/.gitignore**

### Устанавливаем на винду nano

PowerShell в режиме администратора

Set-ExecutionPolicy Bypass -Scope Process -Force; \[System.Net.ServicePointManager\]::SecurityProtocol = \[System.Net.ServicePointManager\]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

**choco install -y nano**

**nano ~/.gitconfig**

**nano ~/.gitignore**

### Удаление папки

**git rm fff** = rm fff + git add fff

### Переименование/перенос

**git mv index.html main.html**

**git mv index.html ./src/**

## 3\. Ветвление и версионирование в git

Веток может быть много. Потом мы вливаем, мёрджим ветки.

### Подходы (git-flow ):

- Тематические ветки - ветки по фичам
- Релизные ветки. Поддержка отдельных версий продукта, например, v1.0 отдельно от main. Команда cherry-pick позволяет влить ветку в main непосредственно в релизную ветку 1.0 и т.п.

## 3\. Ветвление и версионирование в git

### HEAD. Создание и переключение веток.

**git branch feature** - создание ветки

**git checkout feature** - переключение ветки

**git checkout** - переключение ветки на main

В скрытой директории .git в файле HEAD указана последняя ветка

В .git\\refs\\heads\\master указан код последнего коммита

**cat .git/HEAD** - вывести содержание файла

**cat .git/refs/heads/master** - вывести содержание файла в ветке master

**cat .git/refs/heads/feature** - вывести содержание файла в ветке feature

**cat .git/ORIG_HEAD - ORIG_HEAD** = HEAD@{1} is previous state of HEAD

**git branch** - показать все ветки и текущую

**git branch -v** - показать все ветки и текущую и последний коммит.

**git checkout --force master** - Переходит в ветку мастер и удаляет незакоммитченные изменения.

**git stash** - позволяет архивировать изменения, чтобы потом вернуть к ним

**git stash pop** - достать изменения из архива

**git diff** - смотреть изменения

**git checkout -f HEAD**, **git checkout -f** - возвращение в последний коммит

Если у разных веток один и тот же файл одинаково закоммитчен, то можно переходить между ветками при незакоммитченных элементах.

### 3\. 4. Восстановление предыдущей ветки.

Восстановим файл из ветки мастер

**git checkout master index.html** - вытягивает файл и добавляет в staged area (git add над ним)

**git restore --staged index.html** - убрать из staged area (из git add)

**git log** - показывает коммиты

**git log --oneline** - показывает коммиты без подробной информации

**q** выход из git log

**git log master**

**git log master --oneline**

**git show идентификатор_коммита**

**git show master** - показывания изменения в ветке master

**git show HEAD/ветка~** - (Указываем либо HEAD, либо название ветки). Тильда означает посмотреть что было 1 коммит назад. Можно указать несколько тильд, две тильды - 2 коммита назад. HEAD - это текущая ветка.

**git show HEAD/ветка~2** - 2 коммита назад

**git show @~** - Собачка используется вместо HEAD

**git show HEAD~:index.html** - Посмотреть весь файл 1 коммит назад в текущей ветке

**git show HEAD~10:index.html** - Посмотреть весь файл 10 коммитов назад в текущей ветке

### 3\. 6. Слияние веток перемоткой и удаление веток

#### Слияние веток методом Fast-Forward (перемотка вперёд).

1\. Переключаемся на ветку мастер

2\. **git merge feature** - ветка мастер вливается в ветку feature и подхватывает последние изменения

#### Удаление веток

**git branch -d feature** удаляется не ветка, а ссылка на эту ветку. Гит позже их подчистит, если они не используются.

function_name2();

### 3\. 7. Истинное слияние веток.

newFunc();

**git branch -f main ORIG_HEAD**

**git commit -am "Added func function_name2() to index.html"** - git add + git commit

**git merge feature2** - вызовет конфликт

Сначала объединяет base + ours changes + their changes -> merge

**git merge-base main feature2** - показывает идентификатор коммита при слиянии

**git show 23c9<\первые 4 цифра коммита можно указать>:src/script.js** ----- показывает файл на момент разделения веток

**git show main:src/script.js** --------- показывает файл в ветке мэйн

**git show feature2:src/script.js** --------- показывает файл в ветке feature2

Есть различие в ветке feature2, поэтому не будет конфликтов при слиянии веток, сделается всё автоматически

\-----------

"Веселее" будет дальше:

**git show 23c9<\первые 4 цифра коммита можно указать>:index.html**

**git show main:index.html**

**git show feature2:index.html**

Во всех трёх состояния различные данные

\-----------

**git checkout --ours index.html** -------- видим изменения из состояния ours

**git checkout --theirs index.html** -------- видим изменения из состояния theirs

**git checkout --merge index.html** -------- видим изменения из состояния до этого

**git reset --hard** -------- Все состояния возвращаются на последнее состояние ветки main

**git merge feature** -------- получаем конфликт

**git checkout --conflict=diff3 --merge index.html** -------- Гит показывает ещё какие изменения были на момент состояния base

**git config --global merge.conflictstyle diff3** -------- внести глобальный конфликт стиль слияния

**git add .**
**git merge --continue** --------- продолжаем вести слияние

### 3\. 8. Отмена изменений - reset --hard

**git reset --hard h56j**

**git reset --hard head~1**

- **\--soft** — обновление HEAD
- **\--mixed** — обновление индекса
- **\--hard** — обновление рабочей директории.

После отката назад мы можем вернуться назад и дальше вести разработку
Коммиты сохраняются 30 дней, к ним можно вернуться

**git reset --hard ORIG_HEAD** - возвращение на коммит, с которого мы ушли при вводе команды **reset**

**git show HEAD~** - откатиться до текущего коммита

**git reset --hard HEAD** - тоже самое

### 3\. 8. Отмена изменений - reset --soft

**git reset --soft HEAD~** - изменения которые были коммит назад сохраняются. Позволяет добавить изменения в наши предыдущий коммит. Сохраняет все изменения.

**git commit -C --help** - продолжается разработка с добавленными изменения и с предыдущим коммитом.

**-C <\commit>**
**--reuse-message=<\commit>**
Take an existing commit object, and reuse the log message and the authorship information (including the timestamp) when creating the commit.

**-c <\commit>**
**--reedit-message=<\commit>**
Like -C, but with -c the editor is invoked, so that the user can further edit the commit message.

#### Коммитим и добавляем маленькое изменение в предыдущий коммит

- Коммитим
- **git reset --soft HEAD~**
- Делаем изменения
- **git add .**
- **git commit -C ORIG_HEAD** - внозим изменения в предыдущий коммит. А если напишем **git commit -c ORIG_HEAD**, то откроется ещё и текстовый редактор

#### Вносим дополнительные изменения

- **git add index.html**
- **git commit --amend** - вносим правки в текущий коммит
