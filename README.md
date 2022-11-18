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

## Инструкция по установке докера на Linux
Ссылки:
* [Документация (установка докера)](https://docs.docker.com/engine/install/ubuntu/)
* [Документация (запуск докера не из-под суперпользователя)](https://docs.docker.com/engine/install/linux-postinstall/)
* [Статья с DO по установке докера на Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-ru)
* [Документация (установка docker-compose)](https://docs.docker.com/compose/install/)
* [Статья с DO по установке docker-compose на Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04)

Установка докера на дистрибутив линукса Ubuntu:
1. Добавляем репозиторий докера (чтобы получить последнюю его версию)
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
2. Устанавливаем docker
```sh
sudo apt-get update
```
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io -y
```
3. Устанавливаем docker-compose
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```sh
sudo chmod +x /usr/local/bin/docker-compose
```

4. Проверяем, что всё установилось
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

5. Запуск докера не из-под суперпользователя
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
