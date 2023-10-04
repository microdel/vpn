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