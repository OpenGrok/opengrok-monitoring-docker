# OpenGrok Docker instance with monitoring

Inspired by https://github.com/vegasbrianc/prometheus

Place the data to index under the `./opengrok/src` directory and run the
`docker-compose`:

```
ADMIN_USER=root ADMIN_PASSWORD=root docker-compose up
```

## OpenGrok

The web application is running on http://localhost:7777

## Grafana

The Grafana is available on http://localhost:3333
