# Шпаргалка по Git

 ---

 **Сделать папку репозиторием — `git init`**

 Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать Git-репозиторием (от англ. repository — «хранилище»). Для этого следует переместиться в неё и ввести команду git init (от англ. initialize — «инициализировать»).

**«Разгитить» папку, если что-то пошло не так, — `rm -rf .git`**

**Проверить состояние репозитория — `git status`**

**Подготовить файлы к сохранению — `git add`**

- Команда git add --all подготовит к сохранению сразу все файлы.
- С помощью git add . можно добавить в репозиторий текущую папку со всеми файлами.

**Выполнить коммит — `git commit -m "Описание коммита"`**

**Просмотреть историю коммитов — git log**

**Привязать удалённый репозиторий к локальному — git remote add**

Перейдите на страницу удалённого репозитория, выберите тип SSH и скопируйте URL. Кнопка справа позволит сделать это мгновенно.Откройте консоль, перейдите в каталог локального репозитория и введите команду git remote add (от англ. remote — «удалённый» и add — «добавить»).Команде необходимо передать два параметра: имя удалённого репозитория и его URL. В качестве имени используйте слово origin. А URL вы скопировали со страницы удалённого репозитория.

`$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git `

origin (англ. «источник») — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

**Убедиться, что репозитории связаны, — git remote -v**

```
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```

**Отправить изменения на удалённый репозиторий — git push**

```
$ git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master. 
```

В первый раз эту команду нужно вызвать с флагом -u и параметрами origin (имя удалённого репозитория) и main или master (название текущей ветки). Флаг -u свяжет локальную ветку с одноимённой удалённой.

## Зачем нужен README.md

- Название проекта и его краткое описание: кем создан, для чего, какие решает задачи и какие закрывает проблемы.
- Технологии, которые применяются в проекте. В чём его отличие от аналогичных.
- Документация проекта — подробная инструкция о том, что представляет собой проект.
- Планы проекта, если они есть.

---

## Log

**Получить сокращённый лог — `git log --oneline`**

**Файл HEAD**

Файл HEAD (англ. «голова», «головной») — один из служебных файлов папки .git. Он указывает на коммит, который сделан последним (то есть на самый новый).

Вместо хеша последнего коммита можно написать слово HEAD — Git вас поймёт.

## Статусы файлов в Git

**Статусы untracked/tracked, staged и modified**

Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.

* `untracked` (англ. «неотслеживаемый») 
 Мы говорили, что новые файлы в Git-репозитории помечаются как untracked, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У untracked-файла нет предыдущих версий, зафиксированных в коммитах или через команду git add.
* `staged` (англ. «подготовленный»)
  После выполнения команды git add файл попадает в staging area (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии staged.
* `tracked` (англ. «отслеживаемый») 
 Состояние tracked — это противоположность untracked. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью git commit, а также файлы, которые были добавлены в staging area командой git add. То есть все файлы, в которых Git так или иначе отслеживает изменения. 
* `modified` (англ. «изменённый») 
 Состояние modified означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

---

## Как исправить коммит 

Иногда в только что выполненном коммите нужно что-то поменять: например, добавить ещё пару файлов или заменить сообщение на более информативное.

В таком случае можно внести правки в уже сделанный коммит с помощью опции `--amend` (от англ. amend — «исправить», «дополнить») у команды `commit`: `git commit --amend`. Разберём, как она работает.

>  Важно: опция `--amend` работает только с последним коммитом (HEAD). Для исправления более ранних коммитов есть другие команды. 

**Дополнить коммит новыми файлами — `git commit --amend --no-edit`**

Обратите внимание на опцию `--no-edit`. Она сообщает команде `commit`, что сообщение коммита нужно оставить как было.

**Изменить сообщение коммита — `git commit --amend -m "Новое сообщение"`**

## Как откатить все назад

**Выполнить unstage изменений — `git restore --staged <file>`**

Допустим, вы создали или изменили какой-то файл и добавили его в список «на коммит» (staging area) с помощью git add, но потом передумали включать его туда. Убрать файл из staging поможет команда `git restore --staged <file>` (от англ. restore — «восстановить»).

Чтобы «сбросить» все файлы из staged обратно в `untracked/modified`, можно воспользоваться командой `git restore --staged .`: она сбросит всю текущую папку (.).

**«Откатить» коммит — `git reset --hard <commit hash>`**

Иногда нужно «откатить» то, что уже было закоммичено, то есть вернуть состояние репозитория к более раннему. Для этого используют команду `git reset --hard <commit hash>` (от англ. reset  — «сброс», «обнуление» и hard — «суровый»).

```
$ git log --oneline # хеш можно найти в истории
7b972f5 (HEAD -> master) style: добавить комментарии, расставить отступы
b576d89 feat: добавить массив Expenses и цикл для добавления трат # вот сюда и вернёмся
4b58962 refactor: разделить analyzeExpenses() на countSum() и saveExpenses()

$ git reset --hard b576d89
# теперь мы на этом коммите
HEAD is now at b576d89 feat: добавить массив Expenses и цикл для добавления трат
```

Теперь коммит b576d89 стал последним: вся дальнейшая разработка будет вестись от него. Файл также вернулся к тому состоянию, в котором был в момент этого коммита. А коммит 7b972f5 Git просто удалил.

**«Откатить» изменения, которые не попали ни в staging, ни в коммит, — `git restore <file>`**

Может быть так, что вы случайно изменили файл, который не планировали. Теперь он отображается в `Changes not staged for commit (modified)`. Чтобы вернуть всё «как было», можно выполнить команду `git restore <file>`.

```
# случайно изменили файл example.txt
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
          modified:   example.txt

$ git restore example.txt
$ git status
On branch main
nothing to commit, working tree clean
```

Изменения в файле «откатятся» до последней версии, которая была сохранена через `git commit` или `git add`.

* Команда git restore --staged <file> переведёт файл из staged обратно в modified или untracked.
* Команда git reset --hard <commit hash> «откатит» историю до коммита с хешем <hash>. Более поздние коммиты потеряются!
* Команда git restore <file> «откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии.

---

## Просматриваем изменения в файлах

**Просмотр изменения в файлах -- `git diff`**

* Команда git diff сравнит последнюю закоммиченную версию файла с той, что находится в состоянии modified.
* Команда git diff --staged покажет изменения в staged-файлах относительно последних закоммиченных версий.

---

## Игнорирование файлов в Git

Чтобы Git игнорировал ненужные файлы и не пытался добавить их в репозиторий, нужно создать файл .gitignore (от англ. ignore — «игнорировать») и записать в него названия игнорируемых файлов. 

**Как заполнить .gitignore**

С точки зрения Git `.gitignore` — это обычный текстовый файл. Его добавляют в корень репозитория и тоже коммитят.
В простейшем случае в `.gitignore` указывают все файлы, которые нужно игнорировать (по одному имени на строку). Но часто удобнее использовать шаблоны. Шаблон, или правило, — это способ указать сразу на несколько файлов с однотипными названиями.

> Правила из .gitignore применяются только к новым (untracked) файлам. Если файл уже попал в staging area или в коммит, то правила на него не распространяются.

**Комментарий**

Если строка начинается с `#`, то это комментарий, и .gitignore не будет его учитывать.

**Просто название файла

Допустим, нужно, чтобы Git игнорировал все файлы `.DS_Store`. Для этого достаточно добавить в .gitignore строку с названием файла.

```
# для macOS
.DS_Store
```

В таком случае Git будет игнорировать файлы с именем .DS_Store, причём не только в корне репозитория, но и во всех вложенных папках.

**Звёздочка `(*)`**

Символ звёздочки (*) соответствует любой строке, включая пустую. Если такой символ используется в шаблоне в .gitignore, значит, файл будет проигнорирован вне зависимости от того, что будет на месте звёздочки.

```
# игнорировать все файлы, которые заканчиваются на .jpeg
*.jpeg

# игнорировать все файлы "tmp" во всех подпапках папки docs
docs/*/tmp 
```

Теперь Git будет игнорировать все файлы, которые заканчиваются на `.jpeg` — пригодится тем, кто не любит картинки. А также все временные файлы `tmp` (от англ. temporary — «временный») в подпапках папки docs. Например, Git проигнорирует файл `docs/current/tmp`.

**Вопросительный знак (?)**

Вопросительный знак `?` соответствует одному любому символу.

`file?.txt`

**Квадратные скобки ([…])**

Квадратные скобки, как и вопросительный знак, соответствуют одному символу. При этом символ не любой, а только из списка, который указан в скобках.
```
# игнорировать файлы file0.txt, file1.txt и file2.txt
# при этом не игнорировать file3.txt, file4.txt, ...
file[0-2].txt 
```
В скобках можно либо перечислить символы ([abc]), либо задать диапазон ([a-z]).

**Слеш (/)**

Косая черта, или слеш (/), указывает на каталоги. Если шаблон в .gitignore начинается со слеша, то Git проигнорирует файлы или каталоги только в корневой директории.
```
# игнорировать todo.txt в корне репозитория
/todo.txt

# для сравнения: spam.txt будет игнорироваться во всех папках
spam.txt 
```

Теперь файл todo.txt в корневом каталоге будет проигнорирован. При этом, например, файл subdir/todo.txt по-прежнему отслеживается.
Если шаблон заканчивается слешем, то правило применится только к папке.
```
# игнорировать папку build
build/ 
```

Обратите внимание: если build — это папка, то она будет проигнорирована. Если build — обычный файл, то он не подпадёт под правило и не будет игнорироваться.

**Парные звёздочки (`**`)**

Функция парных звёздочек (`**`) похожа на функцию одинарной (`*`). Отличие в том, как они работают с вложенными папками. Двойная звёздочка может соответствовать любому количеству таких папок (в том числе нулю). Одинарная может соответствовать только одной.

```
# игнорировать файлы "docs/current/tmp", "docs/old/tmp",
# а также "docs/old/saved/a/b/c/d/tmp"
# и даже "docs/tmp", потому что ноль вложенных папок тоже подходит
docs/**/tmp

# игнорировать только "docs/current/tmp" и "docs/old/tmp"
# файл "docs/old/saved/a/b/c/d/tmp" не попадает в правило
docs/*/tmp
```

**Восклицательный знак (!)**

Любое правило в файле .gitignore можно инвертировать с помощью восклицательного знака (!).
```
# игнорировать все JPEG-файлы
*.jpeg

# но только не мем с Doge
!doge.jpeg 
```
Теперь файл doge.jpeg будет отслеживаться, хотя остальные jpeg-файлы будут проигнорированы. Такие правила удобны для добавления исключений из других правил .gitignore.

Вот что важно помнить:
* Если нужно, чтобы Git игнорировал какие-то файлы, стоит составить файл .gitignore.
* Посмотреть, что игнорируется, можно с помощью команды git status --ignored.
* Сам файл .gitignore — это обычный файл в репозитории. Его тоже стоит закоммитить.
* Шаблонов много, но их легко найти в интернете вместе с примерами использования.

---

