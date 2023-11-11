# Шпаргалка по Git

---

## Введение

Git(*Global Information Tracker*) - система контроля версий, т.е. программа позволяющая контролировать изменения в проекте.

### Основные функции системы контроля версий

- хранит историю изменений в виде отдельных ревизий;
- позволяет манипулировать историей, например: менять порядок ревизий, полностью удалять версии, возвращаться назад в истории;
- позволяет анализировать изменения, например: кто и когда вносил изменения, кто чаще всего вносил изменения в определённый файл и так далее.

---

## Базовые команды в консоли

### Навигация

- показать текущую папку
```
pwd
```
- показать содержимое текущей паки
```
ls
```

- перейти в папку *project*
```
cd ~/project
```

- перейти на уровень выше, в родительскую папку
```
cd ..
```

- перейти в домашнюю директорию
```
cd ~
```

- перейти в корневую директорию
```
cd /
``` 

### Работа с файлами и папками 

- создать файл *text.txt* в текущей папке
```
touch text.txt
```

- создать папку *folder* в текущей папке
```
mkdir folder
```

- копирование файлов в другое место
```
cp text.txt ~/folder
```

- перемещение файлов в другое место
```
mv text.txt ~/folder
```

- показать содержимое файла
```
cat text.txt
```

- удаление файла *text.txt*
```
rm text.txt
```

- удаление папки *folder*
```
rmdir folder
```

- удаление папки *folder* и всего что в ней находится
```
rm -r folder
```

---

## Настройка Git

Для того чтобы при работе в команде пользователи понимали кто именно сделал коммит, вам нужно настроить свой Git - указать своё имя и почту. Сделать это можно следующим образом:

```
gii config --global user.name "Ivan Ivanov"

git config --global user.mail ivanov@gmail.com
```

Не важно в какой папке вы находитесь, потому что вы используете ключ *-global*.

После выполнения этих команд в файл *.gitconfig*, который находится в домашней директории, запишется ваша информация. Вы можете это проверить с помощью следующих команд:

- прочитать этот файл

```
cat ~/.gitconfig
```

- вывести содержимое файла конфигурации с той же командой *git config*, с флагом *-list*

```
git config --list
```

---

## Инициализация репозитория

### Сделать папку репозиторием

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать **Git репозиторием**. Для этого нужно преместиться в нужную папку и ввести команду

```
git init
```

### "Разгитить" папку, если что-то пошло не так

Если вдруг вы случайно инициализировали репозиторй не в той папке, её можно "разгитить". Для этого нужно удалить скрытую папку *.git*. Сделать это можжно так:
```
cd <папка с репозиторием>

rm -rf .git
```

#### Подробнее, что такое *-rf*

- ключ *-r* позволяет удалять папки вместе с их содержимым

- ключ *-f* избавит вас от вопросов вроде «Вы точно хотите удалить этот файл? А этот? И этот тоже?»

*Будьте осторожны: в подпапке .git хранится история изменений. Если удалить .git, то вся история проекта будет стёрта без возможности восстановления — останется только последняя версия файлов.*

### Проверить состояние репозитория

При инициализации можно проверить состояния репозитория, запустив команду:

```
git status
```

Данная команла выведет:

-  название текущей ветки *On branch master* илии *On branch main*

- сообщение о коммитах в репозитории

- сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать»

---

## Первый коммит

Для того, чтобы сделать коммит, для начала необходимо подготовить файл к сохранению, а затем сделать коммит.

### Подготовить файлы к сохранению

Для подготовки файлов к сохранению используется команда
```
git add <имя файла>
```

Если вы хотите подготовить все файлы, можете воспользоваться командой:

```
git add --all
```

### Выполнить коммит

Для того, чтобы сделать коммит, можно воспользоаваться командой

```
git commit -m "Название коммита"
```

Ключ *-m* присваивает коммиту сообщение.

### Просмотр истории коммитов

Также есть возможность просмотра истории коммитов, при помощи функции

```
git log
```

---

## SSH-ключ

### Немного теории

Компьютеры при обмене данными в сети следуют сетевым протоколам - правила обмена данными между компьютерами.

Одним из наиболее распространённых протоколов является SSH (Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. 
С помощью этого протокола можно получать данных с удалённого компьютера или отправлять их на него.

SSH использует пару ключей для обеспечения безопансости - публичный и приватный:

- приватный - хранится на вашем компьютере и не должен передавться кому-либо ещё. Используется дл расшифровки данных.

- публичный -  доступен всем и используется для шифрования данных.

### Проверка наличия SSH-ключа

Прежде чем генерировать SSH-ключ, нужно убедиться, что у вас их ещё нет. Обычно они находятся в папке *.ssh* в домашней директории. 
Сделать это можно с помощью следующих команд:

```
cd ~

ls -la .ssh/
```

Если папка пуста, то всё впорядке. Если же есть файлы с похожими названиями, то SSH-ключи уже создавались:

- *id_dsa.pub*

- *id_ecdsa.pub*

- *id_ec25519.pub*

Если вы не создавали эти файлы, то удалите их всех.

### Генерация SSH-ключа

Сгенерировать ключ можно при помощи следующих команд:

```
ssh-keygen -t ed25519 -C "ivanov@gmail.com"
```

Используйте электронную почту которая привязана к вашему GitHub аккаунту.

Если у вас возникла ошибка, то скорее всего ваша система не поддерживает алгоритм шифрования *ed25519*. Ничего страшного, воспользуйтесь следующей командой:

```
ssh-keygen -t rsa -b 4096 -C "ivanov@gmail.com"
```

Далее у вас потребуют указать место хранения ключей. Самый простой способ - сделать домашний католог пользователя по умолчанию. Для этого нажмите *Enter*.

Затем у вас попросят задать кодовое слово - это так сказать пароль от SSH-ключа, как бы странно это не звучало. Вы можеете оставитьб его пустым, для этого два раза нжмите *Enter*.

Теперь проверим, сгенерировались ли ключи, для этого вызовите команду:

```
ls -a ~/.ssh
```

На экране должны появится два файла, один с расширением *.pub* - публичный ключ, а другой без - приватный ключ.

---

## Привязка SSH-ключа к GitHub

Для начала скопируем ключ, это можно сделать при помощи команды:

```
clip <~/.ssh/id_ed25519.pub

# или

clip <~/.ssh/id_rsa.pub
```

Выбираете в зависимости от того с помощью какой команды генерировали SSH-ключ.

Если *clip* не работает, вы можеет вывести информацию с помощью *cat* и скопировать ключ в буфер:

```
cat ~/.ssh/id_ed25519.pub

# или

cat ~/.ssh/id_rsa.pub
```

Далее следуйте инструкции:

- перейдите на GitHub и выберите пункт **Settings** в меню аккаунта

- в меню слева нажмите **SSH and GPG keys**

- в открывшейся вкладке выберите **New SSH key**

- в поле **Title** введите название ключа, например **Personal Key**

- в поле **Key type** должно быть **Authentication Key**

- в поле **Key** вставьте ваш ключ, котрый вы скопировали ранее

- нажмите кнопку **Add SSH key**

Далее не плохо было бы проверить правильность ключа с помощью следующей команды:

```
ssh -T git@github.com
```

Если вы первый раз используете Git, чтобы поделиться проектом на GitHub, у вас появиться предупреждение.

Это предупреждение сообщает, что вы ни когда не соединялись с сервером GitHub. Поэтому Git не может гарантировать, что этот сервер является тем, за кого себя выдаёт.

Для подтверждения подлинности сервер генерирует и публикует ключи SHA256. Вы можете проверить ключи [здесь](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints). Если ключ совпадает с тем, что на сайте, значит сервер верный. Введите *yes*, чтобы продолжить.

---

## Связывание локального и удалённого репозитория

Для начала создайте локальный репозиторий (см. Инициализация репозитория), затем создайте удалённый репозиторий на GitHub.

Затем перейдите на страницу удалённого репозитория, выберите тип **SSH** и скопируйте *URL*. 

Откройте консоль, перейдите в каталог локального репозитория и введите следующую команду:

```
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```

Команде необходимо передать 2 параметра: имя удалённого репозитория и его *URL*. В качестве имени можете использовать слово *origin*. А *URL* вы скопировали со страницы удалённого репозитория.

> *origin* - стандартный псевдоним, с помощью которго можно обращаться к удалённому репозиторию.

Затем нужно убедиться, что связывание прошло успешно, сделать это можно при помощи следующей команды:

```
git remote -v
```

В выводе вы должны увидеть две строчки подобные на эти:

```
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push) 
```

---

## Коммит на удалённый репозиторий

Для начала сделайте коммит на локальный репозиторий, после чего можно загрузить содержимое локального репозитория на GitHub. 

Это можно сделать при помощи следующей команды:

```
git push -u origin main
```

Команда *git push* указывается с параметрами *-u* - который свяжет локлаьную ветку с удалённой, *origin* - имя удалённого репозитория и *main* - название текущей ветки. В последующих коммитах можно не указывать параметр *-u*.

---

## Хеш

**Хеширование** - способ преобразования данных и получение их *отпечктка*. 

Каждый коммит состоит из набора информации: автор, дата, описание, содержимое репозитория на момент коммита и ссылка на прошлое состояние.
Git хеширует эту информацию с помощью алгоритма SHA-1 и получает для каждого комита уникальный хеш, с помощью которого можно обращаться к коммиту.

Хеш обладает следующими свойствами:

- если получить хеш дважды для одного и того же набора входных данных, то результат будет полностью одинаковым

- если хоть что-то в исходных данных поменятся, то поменятся и хеш.