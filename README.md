#Создание репозитория на GitHub
		
## 1. Создание нужной папки
$ pwd 
~/dev # текущая папка
$ mkdir info-project # создали нужную папку
$ cd ~/dev/info-project # перешли в нужную папку
$ git init # создали репозиторий 
Initialized empty Git repository in C:/Users/Eugene/dev/info-project/.git/

## 2. Создание файла
### 2.1 Проверить состояние репозитория:
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

### 2.2 Создание файла и его редактирование
$ touch README.md  # как вариант:    > README.md
$ nano README.md    # отредактировать - например вставить подготовленный текст   затем ctrl-O  ctrl-x
$ git add README.md
$ git commit -m "add file README.md"
[master (root-commit) e731895] add file README.md
 1 file changed, 22 insertions(+)
 create mode 100644 README.md
 
## 3. Регистрация на GitHub  
на https://github.com  через почту  стандартно 
используя имя Eugene-Mineev

## 4. Создание репозитория на GitHub
Зайти в свой профиль  https://github.com/Eugene-Mineev
В главном меню выбрать пункт "Repositories" и на вкладке кликнуть "New"
ввести имя репозитория "info-project" и сохранить

## 5. Генерируем SSH-ключ
$ cd ~ # перешли в домашнюю директорию 
$ ls -la .ssh/ # вывели список созданных ключей   не должно быть *.pub
$ ssh-keygen -t ed25519 -C "eugene.mineev@gmail.com"
### 5.1 После выполнения команды ssh-keygen в директории ~/.ssh будет создано два файла — id_ed25519 и id_ed25519.pub 
(или id_rsa и id_rsa.pub — в зависимости от того, какой алгоритм вы использовали):
    id_ed25519/id_rsa — приватный ключ (файл без .pub в конце). Ни в коем случае не копируйте его и не делитесь им.
    id_ed25519.pub/id_rsa.pub — публичный ключ (на это указывает расширение .pub).
$ clip < ~/.ssh/id_ed25519.pub  # скопировать содержимое ключа в буфер обмена	
#### Пункт Settings (англ. «настройки») в меню аккаунта.
#### В меню слева нажмите на пункт SSH and GPG keys.
#### В открывшейся вкладке выберите New SSH key 
#### Правильность ключа с помощью следующей команды. $ ssh -T git@github.com 
The authenticity of host 'github.com (140.82.121.4)' can't be established. ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU. 
This key is not known by any other names. Are you sure you want to continue connecting (yes/no/[fingerprint])?
yes
Hi Eugene-Mineev! You've successfully authenticated, but GitHub does not provide shell access. 

### 5.2 Привязать удалённый репозиторий к локальному — git remote add
$ git remote add origin https://github.com/Eugene-Mineev/info-project.git
### 5.3 Проверка
$ git remote -v
origin  https://github.com/Eugene-Mineev/info-project.git (fetch)
origin  https://github.com/Eugene-Mineev/info-project.git (push)

### 5.4 Перенести изменения в GitHub
$  git push --set-upstream origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 635 bytes | 635.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Eugene-Mineev/info-project.git
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'.

## 6. Оформление сообщений к коммитам
В выводе команды git log --oneline умещается максимум 7272 первых символа сообщения.
Сообщение коммита должно помочь определить, что внутри.
Корпоративный стиль: $ git commit -m "LGS-239: Дополнить список пасхалок новыми числами".
Conventional Commits предлагает такой формат коммита: <type>: <сообщение>. Первая часть type — это тип изменений. Таких типов достаточно много. Вот два примера:
    feat (сокращение от англ. feature) — для новой функциональности;
    fix (от англ. «исправить», «устранить») — для исправленных ошибок.
GitHub-стиль: $ git commit -m "Исправить #334, добавить график температуры" 	
