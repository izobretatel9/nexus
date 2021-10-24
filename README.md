# Хранилище артефактов NEXUS

В этом репозитории находятся файлы:
1. `docker-compose.yml`\
   конфигурация сервисов
1. `nginx.conf`\
   конифгурация nginx
1. `ssl.crt`\
  бандл сертификатов для ssl в nginx
1. `ssl.key`\
   ключ от сертификатов

## nginx.conf
Конфигурация прокси представляет собой интерес, так как реализует следующие сценарии работы Nexus*:

### Проксирование и кэширование пакетов Alpine

Использование репозитория.

- Поменять конфиг менеджера пакетов apk
  
  ```bash
  sed -i -- 's/dl-cdn.alpinelinux.org/nexus.xxx.ru/g' /etc/apk/repositories
  ```

- Добаить в hosts

  ```ini
  <nexus IP>    dl-cdn.alpinelinux.org
  ```

- В запуск команд Docker CLI

  ```bash
  docker [run|build] --add-host dl-cdn.alpinelinux.org:<nexus IP> ...
  ```

### Проксирование группы nuget репозиториев

http://nuget.xxx.ru/nuget

### Проксирование группы Docker репозиториев

Командой `docker pull nexus.xxx.ru/<name>` можно получить любой образ из Docker Hub, Microsoft Container Registry и нашего приватного хранилища

Притом, команда `docker push nexus.xxx.ru/<name>` запостит образ в наше приватное хранилище.

**Сами конфигурации репозиториев хранатся в nexus*
