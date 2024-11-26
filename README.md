
# Лабораторная работа 4.

Создаю docker image (образ). Для этого пишу Dockerfile. Создаю пустой текстовый документ, где в первую очередь указываю, что мой образ будет работать на основе Ubuntu последней достпной версии (latest).  
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
[image!](result.png)

И уже напрямую в терминале контейнера запустить команду
```
/usr/games/cowsay "Moo"
```
Проверим запущенные контейнеры у вас на машине командой
```
docker ps
```
Особенность контейнеризации заключается в том, что рекомендуется под один сервис запускать один контейнер. Также, когда сервис отработал, контейнер автоматически заканчивает свою работу. Поскольку своё предназначение данный контейнер выполнил - вы не увидите его в выводе команды.  
Но в случае, если контейнер был запущен с флагом -it – он ожидает ручных команд и не будет отключаться самостоятельно.  

## Задание:  
Запустить в контейнере приложение “aafire”. Обратите внимание, что оно бесконечное и контейнер не будет автоматически отключаться.  
Приложить скриншот в процессе работы контейнера.  

Далее в рамках лабораторной работы необходимо самостоятельно настроить сеть между двумя контейнерами, также как в предыдущей работе вы настраивали связь между двумя виртуальными машинами.  

Для проверки сети между контейнерами вам потребуется утилита ping. Поскольку контейнеры очень маленькие и в них нет ничего лишнего (по сравнению с виртуальными машинами) - ping там не установлен. В вашем образе нужно будет установить пакет с этой утилитой, помимо aafire.  

Далее запустите два контейнера с aafire и оставьте их в работающем состоянии.  
Откройте ещё одно окно терминала и создайте сеть при помощи команды 
```
docker network create myNetwork
```
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
