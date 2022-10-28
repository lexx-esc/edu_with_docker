## Окружение python

Здесь, **если планируете использовать jupyter lab**, нужно проделать дополнительные манипуляции после [основных действий](../README.md):
1. При создании контейнера нужно пробросить порт для jupyter 8888 на, например - 8080:
```
$ docker run -p 23:22 -p 8080:8888 -v /full/path/my/project:/app -d --name dotnet lexxesc/edu_python
```
2. Необходимо сделать первую загрузку и задать пароль jupyter:
```
(venv) app > cd ..

(venv) ~ > jupyter lab -allow-root

[I 2022-11-13 08:36:47.489 ServerApp] jupyterlab | extension was successfully linked.
[I 2022-11-13 08:36:47.505 ServerApp] nbclassic | extension was successfully linked.
[I 2022-11-13 08:36:47.767 ServerApp] notebook_shim | extension was successfully linked.
[W 2022-11-13 08:36:47.793 ServerApp] WARNING: The Jupyter server is listening on all IP addresses and not using encryption. This is not recommended.
[I 2022-11-13 08:36:47.796 ServerApp] notebook_shim | extension was successfully loaded.
[I 2022-11-13 08:36:47.798 LabApp] JupyterLab extension loaded from /root/venv/lib/python3.10/site-packages/jupyterlab
[I 2022-11-13 08:36:47.799 LabApp] JupyterLab application directory is /root/venv/share/jupyter/lab
[I 2022-11-13 08:36:47.805 ServerApp] jupyterlab | extension was successfully loaded.
[I 2022-11-13 08:36:47.813 ServerApp] nbclassic | extension was successfully loaded.
[I 2022-11-13 08:36:47.815 ServerApp] Serving notebooks from local directory: /root/app
[I 2022-11-13 08:36:47.816 ServerApp] Jupyter Server 1.23.1 is running at:
[I 2022-11-13 08:36:47.816 ServerApp] http://localhost:8888/lab?token=853fdcbcd100d46e045bda10b249ec71b8fc246d9ef5704f
[I 2022-11-13 08:36:47.816 ServerApp]  or http://127.0.0.1:8888/lab?token=853fdcbcd100d46e045bda10b249ec71b8fc246d9ef5704f
[I 2022-11-13 08:36:47.816 ServerApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[C 2022-11-13 08:36:47.824 ServerApp] 
    
    To access the server, open this file in a browser:
        file:///root/.local/share/jupyter/runtime/jpserver-662-open.html
    Or copy and paste one of these URLs:
        http://localhost:8888/lab?token=853fdcbcd100d46e045bda10b249ec71b8fc246d9ef5704f
     or http://127.0.0.1:8888/lab?token=853fdcbcd100d46e045bda10b249ec71b8fc246d9ef5704f

```
Находим в выводе токен (подписан в ссылках, как token) и копируем его. Дальше идем в браузер, вводим адрес:
```
localhost:8080
```
Смотрним вниз страницы, вставляем в нужное поле токен и вводим под ним пароль

Теперь, если нужен сервер ноутбуков - стартуем его в работающем контейнере:
```
$ docker exec -d 1b5d ../venv/bin/jupyter-lab --allow-root
```