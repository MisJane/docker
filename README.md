# docker
docker course
Docker.tmp
docker - контенирезатор приложений
1. Разрешение зависимостей
2. Доставка "в коробке"
3. Изолированность от других программ

- доставка "в коробке" (разрешение зависимостей) / изолированность от других программ
- стандартизация
- воспроизводимость
- откат
- масштабируемость

Платформа для удобной разработки, доставки, тестирования, запуска и эксплуатации приложений.

Сущности:
 - Демон (docker daemon)
 - Образ (docker image)
 - Контейнер (docker container)
 - Репозиторий (docker registry) (репозиторий/сервер)

Docker host - Client - Daemon (Container/Image - i  nstraction)
ХОСТ
- процесс
  |
  |
  l___процесс в контейнере
      |
	  l____процесс в контейнере
	  
	  КОНТЕЙНЕР
  - процесс
  - процесс
  - процесс

> Инструкция по установке докера на Linux
Ссылки:
* [Документация (установка докера)]	(https://docs.docker.com/engine/install/ubuntu/)
* Документация (запуск докера не из-под суперпользователя)	https://docs.docker.com/engine/install/linux-postinstall/
* Статья с DO по установке докера на Ubuntu 20.04	https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-ru
* Документация (установка docker-compose)	https://docs.docker.com/compose/install/
* Статья с DO по установке docker-compose на Ubuntu 20.04	https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04

Установка докера на дистрибутив линукса Ubuntu:
1. Добавляем репозиторий докера (чтобы получить последнюю его версию)

	  sudo apt-get update

	  sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release -y

	  sudo mkdir -p /etc/apt/keyrings

	  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

	  echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
2. Устанавливаем docker
	  sudo apt-get update
	  sudo apt-get install docker-ce docker-ce-cli containerd.io -y
3. Устанавливаем docker-compose
	  sudo curl -L "https://github.com/docker/compose/releases/download/v2.6.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

	  sudo chmod +x /usr/local/bin/docker-compose

4. Проверяем, что всё установилось
	  sudo docker -v
	  sudo docker ps
	  sudo docker images
	  docker-compose -v

5. Запуск докера не из-под суперпользователя
	  sudo groupadd docker
	  sudo usermod -aG docker $USER
Затем выходим из терминала и заходим обратно.
После этого нужно проверить, что всё сработало:
	  id -nG
	  docker ps
	  docker images
