# grafana-docker

This repository contain all files required to build a "shadow Grafana" for [openITCOCKPIT](https://github.com/it-novum/openITCOCKPIT) as Docker container. 🐳

## Local usage
````
git clone https://github.com/it-novum/grafana-docker.git
cd grafana-docker

docker run -t -i --rm \
  -p 127.0.0.1:3033:3033 \
  --name=shadow_grafana \
  -e "GF_SECURITY_ADMIN_PASSWORD=admin" \
  -e "GF_PATHS_CONFIG=/etc/openitcockpit/grafana/grafana.ini" \
  -e "GF_PATHS_DATA=/var/lib/grafana" \
  -e "GF_PATHS_HOME=/usr/share/grafana" \
  -e "GF_PATHS_LOGS=/var/log/grafana" \
  -e "GF_PATHS_PLUGINS=/var/lib/grafana/plugins" \
  -e "GF_PATHS_PROVISIONING=/etc/grafana/provisioning" \
  -v grafana-data:/var/lib/grafana \
  -v /etc/openitcockpit/grafana:/etc/openitcockpit/grafana \
  grafana/grafana
````

## Builds
The content of this repository is available as debian package (deb) `openitcockpit-grafana` at
https://packages.openitcockpit.com/

The debian package also contains a `grafana.tar.bz2` file, which is the Docker image of the container.

Export Docker image to file:
````
docker save grafana/grafana > grafana.tar
bzip2 grafana.tar
````

Import a Docker image from tar
````
docker load < grafana.tar.bz2
````

# License
[MIT License](https://github.com/it-novum/grafana-docker/blob/master/LICENSE)
