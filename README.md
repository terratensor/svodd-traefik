# svodd-traefik

### Конфигурация сервиса traefik для кластера svodd

Основная киллер-фича Traefik в том, что он автоматически подхватывает настройки из всех сервисов.

В кластер с одним общим Traefik можно задеплоить сколько угодно проектов на любых доменах или поддоменах, и они автоматически получат Let's Encrypt сертификаты и заработают.

А при использовании Nginx+Certbot нужно все конфигурации и домены для каждого сайта прописывать в них вручную.

```
HOST={server_ip_addres} PORT=22 IMAGE_TAG=master-1 BUILD_NUMBER=1 make deploy
```

`--providers.docker.exposedByDefault=false`

Это значит, что по умолчанию traefik будет подхватывать не все наши сервисы в сети, а только те у которых установлена метка - traefik.enable=true

`- traefik.docker.network=traefik-public`
объявляет с какой сетью работает traefik

name указывает, что докеру не надо добавлять префиксы по названию проекта к названию сети traefik-public 
```
networks:
    traefik-public:
        name: traefik-public
```
