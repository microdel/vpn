# OpenVPN

Настройка сервера

```
docker-compose run --rm openvpn ovpn_genconfig -u udp://{vpn_server_address}
docker-compose run --rm openvpn ovpn_initpki
```

Создание клиентского сертификата:

`docker-compose run --rm openvpn easyrsa build-client-full {client_name} nopass`

Экспорт клиентской конфигурации:

`docker-compose run --rm openvpn ovpn_getclient {client_name} > certificate.ovpn`

# Wireguard

Чтобы вывести на экран qr код добавления туннеля, на сервере исполняем команду:

`docker exec -it wireguard /app/show-peer 1`

## Конфиги подключения
Настройка клиента на любой платформе по сути сводится к тому, чтобы импортировать на клиент уже готовый файл конфигурации с сервера.

На сервере выведем содержимое монтируемой внутрь docker контейнера директории `~/wireguard/config`

В этой директории наблюдаем файлы и директории жизнедеятельности контейнера. Нас интересуют директории peer1, peer2, peerN, где N - номер пира, как вы уже поняли.

Внутри каждой директории под каждого пира лежат заранее сгенерированные при старте контейнера файлы, а именно:

```
privatekey-peer1, publickey-peer1 - приватный и публичный ключ
peer1.png - изображение с qr кодом подключения
peer1.conf - целевой конфигурационный файл, который требуется на клиенте
```