Install Loki with Docker or Docker Compose : 
You can install Loki and Promtail with Docker or Docker Compose if you are evaluating, testing, or developing Loki. For production, Grafana recommends installing with Helm or Tanka.
The configuration files associated with these installation instructions run Loki as a single binary.

 #################
Prerequisites
##################
Docker
Docker Compose (optional, only needed for the Docker Compose install method)


Install with Docker on Linux
Create a directory called loki. Make loki your current working directory:

mkdir loki
cd loki 

(Below cmd gives you the yaml file to setup loki and promtail)
wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
wget https://raw.githubusercontent.com/grafana/loki/v3.0.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

 docker run --name loki -d -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:3.2.1 -config.file=/mnt/config/loki-config.yaml
docker run --name promtail -d -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:3.2.1 -config.file=/mnt/config/promtail-config.yaml
