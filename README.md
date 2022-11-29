# docker
## docker - контенирезатор приложений
1. Разрешение зависимостей
2. Доставка "в коробке"
3. Изолированность от других программ

- доставка "в коробке" (разрешение зависимостей) / изолированность от других программ
- стандартизация
- воспроизводимость
- откат
- масштабируемость

<b>Платформа для удобной разработки, доставки, тестирования, запуска и эксплуатации приложений.</b>

Сущности:
 - Демон (docker daemon)
 - Образ (docker image)
 - Контейнер (docker container)
 - Репозиторий (docker registry) (репозиторий/сервер)

Docker host - Client - Daemon (Container/Image - instraction)

<b>Docker host (Хост)</b> - Компьютер, на котором установлен докер<br>
<b>Docker container (Контейнер)</b> - Изолированная среда запуска приложений<br>
<b>Docker image (Образ)</b> - Шаблон инструкций по созданию докер контейнера<br>
<b>Docker daemon (Демон)</b> - Фоновая программа, которая управляет объектами докера<br>
<b>Docker client (Клиент)</b> - Интерфейс взаимодействия с демоном<br>
<b>Docker registry (Репозиторий)</b> - Сервер, используемый для хранения образов

## Инструкция по установке докера на Linux
Ссылки:
* [Документация (установка докера)](https://docs.docker.com/engine/install/ubuntu/)
* [Документация (запуск докера не из-под суперпользователя)](https://docs.docker.com/engine/install/linux-postinstall/)
* [Статья с DO по установке докера на Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-ru)
* [Документация (установка docker-compose)](https://docs.docker.com/compose/install/)
* [Статья с DO по установке docker-compose на Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)

<b>Установка докера на дистрибутив линукса Ubuntu:</b>

<b>1. Добавляем репозиторий докера (чтобы получить последнюю его версию)</b>
```sh
sudo apt-get update
```
```sh
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y
```
```sh
sudo mkdir -p /etc/apt/keyrings
```
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```sh
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
<b>2. Устанавливаем docker</b>
```sh
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```
<b>3. Устанавливаем docker-compose</b>
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```sh
sudo chmod +x /usr/local/bin/docker-compose
```

<b>4. Проверяем, что всё установилось</b>
```sh
sudo docker -v
```
```sh
sudo docker ps
```
```sh
sudo docker images
```
```sh
docker-compose -v
```

<b>5. Запуск докера не из-под суперпользователя</b>
```sh
sudo groupadd docker
```
```sh
sudo usermod -aG docker $USER
```
Затем выходим из терминала и заходим обратно.
После этого нужно проверить, что всё сработало:
```sh
id -nG
```
```sh
docker ps
```
```sh
docker images
```
## Команды 
<b>Работа с образами</b><br>
[docker images](https://docs.docker.com/engine/reference/commandline/images/) или [docker image ls](https://docs.docker.com/engine/reference/commandline/image_ls/) — посмотреть список образов<br>

[docker rmi <образ> [образ...]](https://docs.docker.com/engine/reference/commandline/rmi/) или [docker image rm <образ> [образ...]](https://docs.docker.com/engine/reference/commandline/image_rm/) — удалить образ(ы)<br>

<b>Работа с контейнерами</b><br>
[docker run <образ>](https://docs.docker.com/engine/reference/commandline/run/) — поднять контейнер на основе образа
      [docker run --name <имя> <образ>](https://docs.docker.com/engine/reference/run/#name---name) — при поднятии присвоить имя контейнеру
      [docker run --rm <образ>](https://docs.docker.com/engine/reference/run/#clean-up---rm) — удалять контейнер после завершения его работы
      [docker run -it <образ>](https://docs.docker.com/engine/reference/commandline/run/#assign-name-and-allocate-pseudo-tty---name--it) — позволяет «войти» в контейнер во время его создания
      [docker run -d <образ>](https://docs.docker.com/engine/reference/run/#detached--d) — поднять контейнер в фоновом режиме
[docker ps](https://docs.docker.com/engine/reference/commandline/ps/#show-both-running-and-stopped-containers) — список активных (работающих) контейнеров
      docker ps -a — список всех контейнеров
[docker stop <контейнер> [контейнер...]](https://docs.docker.com/engine/reference/commandline/stop/) — остановить работающий(ие) контейнер(ы)
[docker start <контейнер> [контейнер...]](https://docs.docker.com/engine/reference/commandline/start/) — запустить остановленный(ые) контейнер(ы)
[docker rm <контейнер> [контейнер...]](https://docs.docker.com/engine/reference/commandline/rm/) — удалить контейнер(ы)
[docker exec <контейнер> команда](https://docs.docker.com/engine/reference/commandline/exec/) — запустить команду в работающем контейнер
      [docker exec -it <контейнер> bash](https://docs.docker.com/engine/reference/commandline/exec/#run-docker-exec-on-a-running-container) — запустить bash процесс и «войти» в контейнер
