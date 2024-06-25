# Prometheus-Loki-Grafana-NodeExport on Docker

Run the latest version of the Grafana-Loki-Prometheus with Docker and Docker Compose. You can monitoring and logging your system and containers.

 <img src="loki.webp" alt="loki" width="400" height="400"/> 

we need to use a plugin to collect promtaile container log. we will install a driver and get permission for loki.

```
 docker plugin install grafana/loki-docker-driver:latest --alias loki --grant-all-permissions
```

then we will change the default settings of where docker will dump the logs to loki. we will do this by entering a few extra lines in the /etc/docker/daemon.json file. the config we will enter is below and then we will restart docker. 
```
{
    "log-driver": "loki",
    "log-opts": {
        "loki-url": "http://localhost:3100/loki/api/v1/push",
        "loki-batch-size": "400"
    }
}
```
then run this command.
```
systemctl restart docker
```

finally you can run this command
```
docker compose up -d 
```
