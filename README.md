# monitoring_Prometheus

```
mkdir monitoring && cd monitoring
```

### Создаем docker-compose.yml
```
nano docker-compose.yml
```
### Содержимое docker-compose.yml
```
version: '3.7'

services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"
```

### Создаем prometheus.yml
```
nano prometheus.yml
```

### Содержимое docker-compose.yml

```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'esp8266'
    metrics_path: '/metrics'
    static_configs:
      - targets: ['192.168.253.142:80']
```
### Запускаем docker-compose

```
docker compose up -d
```



