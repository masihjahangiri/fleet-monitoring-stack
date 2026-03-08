# Fleet Monitoring Stack

Production-ready monitoring solution for managing multiple server nodes. Collects system metrics via Node Exporter, stores and queries with Prometheus, visualizes in Grafana, and alerts through Alertmanager with Telegram integration.

Built for self-managed infrastructure where you need full observability without relying on managed cloud monitoring services.

## Architecture

```
Server Nodes (Node Exporter :9100)
        |
        v
  Prometheus (:9090)  -->  Alertmanager (:9093)  -->  Telegram
        |
        v
   Grafana (:3000)
```

## What's Included

- **Prometheus** -- Metric collection with dynamic target configuration via environment variables. Basic auth enabled. Custom build with gomplate templating for target injection.
- **Grafana** -- Pre-configured Node Exporter dashboard. Prometheus datasource auto-provisioned.
- **Alertmanager** -- Telegram notifications for critical alerts. Basic auth enabled.
- **Node Exporter installer** -- One-liner script to deploy Node Exporter on target servers as a systemd service.

## Pre-configured Alerts

| Alert | Condition | Severity |
|---|---|---|
| Instance Down | Target unreachable for 1m | Critical |
| High CPU | >80% for 2m | Warning |
| High Memory | >85% for 2m | Warning |
| High Disk Usage | >85% | Warning |
| High Network Traffic | >10MB/s for 5m | Warning |

## Quick Start

1. Clone the repo and copy the environment file:

```bash
git clone https://github.com/masihjahangiri/fleet-monitoring-stack.git
cd fleet-monitoring-stack
cp example.env .env
```

2. Configure `.env` with your targets and credentials:

```bash
NODE_EXPORTER_TARGETS_JSON='[{"host":"server1:9100","label":"web-01"},{"host":"server2:9100","label":"db-01"}]'
PROM_PASSWORD=your-prometheus-password
GF_SECURITY_ADMIN_PASSWORD=your-grafana-password
```

3. Install Node Exporter on each target server:

```bash
curl -fsSL https://raw.githubusercontent.com/masihjahangiri/node-exporter-installer/main/install.sh | sudo bash
```

4. Start the stack:

```bash
docker compose up -d
```

5. Access Grafana at `http://your-server:3000`.

## Configuration

All configuration is via environment variables in `.env`. See `example.env` for the full list.

| Variable | Description |
|---|---|
| `NODE_EXPORTER_TARGETS_JSON` | JSON array of `{host, label}` objects for Prometheus targets |
| `PROM_PASSWORD` / `PROM_HASHED_PASSWORD` | Prometheus basic auth credentials |
| `GF_SECURITY_ADMIN_PASSWORD` | Grafana admin password |
| `PROMETHEUS_PERSIST_PATH` | Host path for Prometheus data persistence |
| `GRAFANA_PERSIST_PATH` | Host path for Grafana data persistence |
| `ALERTMANAGER_PERSIST_PATH` | Host path for Alertmanager data persistence |
| `NETWORK_NAME` | Docker network name |

## Requirements

- Docker and Docker Compose
- Ubuntu 20.04+ on target servers (for Node Exporter installer)

## License

MIT
