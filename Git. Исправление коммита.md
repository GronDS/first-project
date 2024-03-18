
###  **`git commit --amend`** - внести правки в с последний сделанный коммит (`HEAD`)

#### Пример

Создаем тренировочный репозиторий для отработки команды и добавляем несколько файлов.


```BASH
$ mkdir ~/dev/commit-amend-fun
$ cd ~/dev/commit-amend-fun
$ git init
# вывод git init 
$ touch main.html
$ touch common.css
# дальше отредактировали оба файла 
```
##### `git commit --amend --no-edit` — дополнить коммит новыми файлами

В какой-то момент мы забыли о файле `common.css` и добавили в коммит только `main.html`.

```BASH
$ git add main.html
$ git commit -m "Добавить главную страницу"
$ git log --oneline
777fec3 Добавить главную страницу 
```

Файл `common.css` так и остался «висеть» в `untracked`. В этом легко убедиться, если вызвать `git status`.

```BASH
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
          common.css

nothing added to commit but untracked files present (use "git add" to track) 
```

Дополним последний коммит забытым файлом `common.css` с помощью опции `--amend`.

```BASH
$ git add common.css
# добавили файл common.css в список на коммит как обычно

# но вместо команды commit -m '...'
# будет:
$ git commit --amend --no-edit

$ git log --oneline
8340eb2 Добавить главную страницу
# коммит в истории всё ещё один (но у него новый хеш) 
```

С опцией `--amend` команда `commit` не создаст новый коммит, а дополнит последний, просто добавив в него файл `common.css`. При этом хеш последнего коммита изменится, потому что изменился список файлов в коммите.

Опция `--no-edit` сообщает команде `commit`, что сообщение коммита нужно оставить как было.

Точно так же можно добавить не новый файл, а дополнительные изменения в уже добавленном в коммит файле.

```BASH
# ещё раз отредактировали main.html

$ git add main.html # добавили в список на коммит
$ git commit --amend --no-edit 
```


##### `git commit --amend -m "Новое сообщение"` —  изменить сообщение коммита 


```BASH
$ git commit --amend -m "Добавить главную страницу и стили"
$ git log --oneline
a31fa24 Добавить главную страницу и стили 
```

Хеш коммита снова поменялся, потому что изменились сообщение и время коммита. При этом файлы в коммите остались те же: `main.html` и `common.css`.