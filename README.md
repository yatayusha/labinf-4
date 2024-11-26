
# Лабораторная работа 4.

Создаю docker image (образ). Для этого пишу Dockerfile. Создаю пустой файл, где в первую очередь указываю, что мой образ будет работать на основе Ubuntu последней достпной версии (latest).  
```
FROM ubuntu:latest
```
Далее указываю, что мы обновляем пакетный менеджер и устанавливаем библиотеку `libaa-bin` в которой содержится `aafire`. 
```
RUN apt-get update && apt-get install -y libaa-bin
```
На этом Dockerfile готов, закрываю и сохраняю его под этим названием. В терминале в папке с этим файлом запускаю команду сборки образа с тегом “aafire”.
```
docker build -t aafire .
```
Далее запускаю контейнер на основе созданного образа и подключаюсь к нему напрямую. При создании контейнера передаю ему запуск приложения “aafire”, которое находится в папке /usr/bin/aafire

`-it` флажок, который обозначает, что приложение будет работать бесконечно

```
docker run -it aafire /usr/bin/aafire
```

Результат работы программы:

![image!](result.png)

Далее настраиваю сеть между двумя контейнерами: для этого в соседней директории создаю ещё один Dockerfile и проделывваю те же действия, что и в первом (запускаю контейнер и подключаюсь к нему). Для каждого контейнера своё окно терминала.

Затем создаю новый образ `aafire-ping`
```
sudo docker build -t aafire-ping

В образе помимо aafire устанавливаю пакет с утилитой `ping`:

```
RUN apt update && apt install -y libaa-bin iputils-ping
```

Далее запускаю контейнер на основе нового созданного образа. При создании контенера передаю ему запуск приложения `aafire`:
```
sudo docker run -it --name image_1 aafire-ping /usr/bin/aafire
```
```
sudo docker run -it --name image_2 aafire-ping /usr/bin/aafire
```
Далее убеждаюсь в том, что оба контейнера запущены с помощью команды
```
sudo docker ps
```
![image!](dockerps.png)

Далее запускаю два контейнера с aafire и оставляю их в работающем состоянии.  
С помощью команды `docker network create myNetwork` создаю сеть:

![image!](createnetwork.png)


После этого нужно будет подключить контейнеры к вашей сети. Названия контейнеров можно увидеть при выводе списка действующих контейнеров у вас на машине.
```
docker network connect myNetwork mycontainer1
docker network connect myNetwork mycontainer2
```
Теперь при помощи следующей команды вы можете увидеть настройки созданной вами сети.
```
docker network inspect myNetwork
```
Далее вам нужно самостоятельно протестировать соединение между контейнерами утилитой ping и приложить скриншот.

### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы.

Что вам нужно знать, чтобы успешно защитить работу:

Как создавать и управлять - докерфайлом (команды, оптимизация), образами (создание, запуск, принцип работы), контейнерами (запуск, отслеживание, объединение); виртуализация и контейнеризация. 

## Источники

[Источник где можно найти все](https://google.com)
