## Учебная платформа. Зачем?

Когда я пошел на курсы, мне стало нужно писать по чуть-чуть на разных языках программирования. И каждый из них тащил свои зависимости, которыми не хотелось засорять компьютер. Тогда и возникла идея воспользоваться docker (а заодно - и познакомится с ним).

Не хотелось сильно мудрить, поэтому решил, что будет единая база, а на нее будут достраиваться образы необходимых библиотек и инструментов.

Ознакомится с содержимым можно тут:
- [База](edu_platform/)
- [dotnet](edu_dotnet)

По мере добавления языков, будут добавляться и потомки

## Как использовать?

Конечно, цель - автоматизировать все. Но, пока, многое приходится настраивать руками.

1. Скачиваем образ (или создаем сами на основании вложенного Dockerfile)

```
$ docker pull lexxesc/edu_platform
$ docker pull lexxesc/edu_dotnet

или

$ docker build -t lexxesc/edu_dotnet
```

А потом запускаем сборку контейнера
```
S docker run -p 23:22 -v /full/path/my/project:/app -d lexxesc/edu_dotnet
```

Если хотите все оставить внутри приложения, ключ -v и его параметры можно не прописывать

2. Проверяем что контейнер работает
```
$ docker ps
CONTAINER ID   IMAGE                COMMAND               CREATED          STATUS          PORTS                NAMES
1b5d5af97650   lexxesc/dotnet_edu   "/usr/sbin/sshd -D"   1 minute ago   Up 1 minute   0.0.0.0:23->22/tcp   pensive_euclid
```

3. Заходим внутрь контейнера для настройки
```
$ docker exec -it 1b5d zsh
```
4. Настраиваем пароль root (да - работать будем от него, и да - приветствие изменено)
```
app > passwd
Новый пароль: 
Повторите ввод нового пароля:
passwd: пароль успешно обновлён
app >
```
5. Настраиваем git
```
app > git config --global user.name John Doe
app > git config --global user.email doe.john@yahoo.com
app > git config --global init.defaultbranch main
app > git config --global core.quotepath false
app > cd && mkdir .ssh && cd .ssh && ssh-keygen -t ed25519 -C "doe.john@yahoo.com" -f "DoeJohn"
.ssh > echo 'Host github.com\n    HostName github.com\n    User git\n    IdentityFile ~/.ssh/DoeJohn' >> config
```
Публичный ключ нужно прописать в репозиторий (на github есть подробная инструкция)

6. Устанавливаем в VSCode расширение от Microsoft [remote-ssh](https://github.com/Microsoft/vscode-remote-release)

![gif](https://microsoft.github.io/vscode-remote-release/images/ssh-readme.gif)

Подключаемся к хосту открываем папку */app* и терминал к ней
```
$ ssh root@ip_host -p 23
```

7. Внимание!!! Русского языка в терминале VSCode по умолчанию - нет. Нужно чуть подстроить локаль, чтобы она нормально подхватывалась.

```
app > locale-gen ru_RU.UTF-8 && dpkg-reconfigure locales

и следуем инструкциям.
``` 

После **перезагрузки контейнра** русский язык появится.

8. Создаем или клонируем репозиторий и наслаждаемся чистотой в системе =)
