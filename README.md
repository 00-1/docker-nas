# docker-nas-arm

NAS server on arm in docker containers

## hardware

[odroid hc1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080)

## containers

### portainer

https://portainer.readthedocs.io/en/latest/deployment.html

use tag `linux-arm`

### watchtower

https://hub.docker.com/r/v2tec/watchtower/

use tag `armhf-latest`

### home assistant

https://hub.docker.com/r/homeassistant/home-assistant/

need to build for arm

### minio

https://hub.docker.com/r/minio/minio/

may need to build for arm
