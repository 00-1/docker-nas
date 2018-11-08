# docker-nas-arm

NAS server on arm in docker containers

## hardware

[odroid hc1](https://www.hardkernel.com/main/products/prdt_info.php?g_code=G150229074080)

## containers

### portainer

https://portainer.readthedocs.io/en/latest/deployment.html

use tag `linux-arm`

```yaml
  portainer:
    image: portainer/portainer
    container_name: portainer
    restart: always
    command: -H unix:///var/run/docker.sock
    ports:
      - "XXXX:9000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ${USERDIR}/docker/portainer/data:/data
      - ${USERDIR}/docker/shared:/shared
    environment:
      - TZ=${TZ}
```

### watchtower

https://hub.docker.com/r/v2tec/watchtower/

use tag `armhf-latest`

```yaml
  watchtower:
    container_name: watchtower
    restart: always
    image: v2tec/watchtower
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: --schedule "0 0 4 * * *" --cleanup
```    

### home assistant

https://hub.docker.com/r/homeassistant/armhf-homeassistant/

```yaml
 homeassistant:
    container_name: homeassistant
    restart: always
    image: homeassistant/home-assistant
    devices:
      - /dev/ttyUSB0:/dev/ttyUSB0
      - /dev/ttyUSB1:/dev/ttyUSB1
      - /dev/ttyACM0:/dev/ttyACM0
    volumes:
      - ${USERDIR}/docker/homeassistant:/config
      - /etc/localtime:/etc/localtime:ro
      - ${USERDIR}/docker/shared:/shared
    ports:
      - "XXXX:8123"
    privileged: true
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
```      

### minio

https://hub.docker.com/r/minio/minio/

need to build for arm: https://github.com/alexellis/docker-arm/tree/master/images/armhf/minio
