# OpenGrok Docker instance with monitoring

Inspired by https://github.com/vegasbrianc/prometheus and
https://github.com/Einsteinish/Docker-Compose-Prometheus-and-Grafana

# How to run

Place the data to index under the `./opengrok/src` directory and run the
`docker-compose`:

```
ADMIN_USER=root ADMIN_PASSWORD=root docker-compose up
```

## Service

To run the `docker-compose` as a service in Ubuntu, assuming this was checked out to `/home/ubuntu/monitoring`,
place the following to `/etc/systemd/system/docker-monitoring.service`.

```
[Unit]
Description=Docker Compose for monitoring
Requires=docker.service
After=docker.service

[Service]
User=ubuntu
Group=ubuntu
WorkingDirectory=/home/ubuntu/monitoring
ExecStart=/usr/bin/docker-compose up -d
ExecStop=/usr/bin/docker-compose down
TimeoutStartSec=0
Restart=on-failure
StartLimitBurst=3
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

and run

```
sudo chown root /etc/systemd/system/docker-monitoring.service
sudo systemctl daemon-reload
sudo systemctl enable docker-monitoring.service
sudo systemctl start docker-monitoring.service
```

# Properties

## OpenGrok

The web application is running on http://localhost:7777

## Grafana

The Grafana is available on http://localhost:3333 and it has 3 preconfigured
dashboards:
  - web app latencies
  - web app JVM statistics
    - the JVM memory panel has preconfigured alert for 1 GiB overall memory
  - indexer metrics
