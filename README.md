# Fleet Monitoring Stack

A comprehensive monitoring solution for managing multiple server nodes using Prometheus, Grafana, Node Exporter, and Alertmanager. This stack provides real-time monitoring, visualization, and alerting capabilities for your server fleet.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 🚀 Features

- **Centralized Monitoring:** Monitor multiple servers from a single dashboard
- **Real-time Metrics:** Collect system-level metrics including CPU, memory, disk, and network
- **Beautiful Dashboards:** Pre-configured Grafana dashboards for instant visualization
- **Smart Alerting:** Configurable alerts via Telegram with different severity levels
- **High Availability:** Reliable monitoring with automatic recovery
- **Secure Access:** Basic authentication for Prometheus and Grafana interfaces

## 🏗️ Architecture

- **Node Exporter:** Collects system metrics from each server node
- **Prometheus:** Central metrics collection and storage
- **Grafana:** Data visualization and dashboarding
- **Alertmanager:** Alert handling and notifications

## 📋 Prerequisites

- Docker and Docker Compose
- Linux-based servers for monitoring
- Telegram Bot (for alerts)
- Sufficient disk space for metrics storage

## 🛠️ Installation

1. Clone the repository:

```bash
git clone https://github.com/masihjahangiri/fleet-monitoring-stack.git
cd fleet-monitoring-stack
```

2. Create environment variables file:
```bash
cp .env.example .env
```

3. Configure the environment variables:
```bash
# Edit .env file with your settings
PROM_PASSWORD=your_hashed_password
GF_SECURITY_ADMIN_PASSWORD=your_grafana_password
PROMETHEUS_PERSIST_PATH=/path/to/prometheus/data
ALERTMANAGER_PERSIST_PATH=/path/to/alertmanager/data
GRAFANA_PERSIST_PATH=/path/to/grafana/data
```

4. Configure your server nodes in `prometheus/prometheus.yml`

5. Start the monitoring stack:
```bash
docker-compose up -d
```

## 🔧 Configuration

### Prometheus
- Default port: 9090
- Configuration file: `prometheus/prometheus.yml`
- Alert rules: `prometheus/rules/node_rules.yml`

### Grafana
- Default port: 3000
- Default username: admin
- Password: Set via environment variable
- Datasources: Auto-configured for Prometheus
- Dashboards: Automatically provisioned

### Alertmanager
- Default port: 9093
- Configuration: `alertmanager/alertmanager.yml`
- Supports Telegram notifications
- Configurable alert routing and grouping

## 🚨 Alert Rules

Pre-configured alerts include:
- High CPU Usage (>80%)
- High Memory Usage (>85%)
- High Disk Usage (>85%)
- Instance Down
- High Network Traffic (>10MB/s)
- Network 95th Percentile (>50MB/s)

## 📊 Metrics Collection

Node Exporter collects various system metrics including:
- CPU utilization
- Memory usage
- Disk I/O
- Network traffic
- System load
- File system usage

## 🔐 Security

- Basic authentication enabled for Prometheus
- Grafana authentication required
- Internal Docker network for components
- Configurable access controls

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Support

For support, please open an issue in the GitHub repository.

## ⭐ Show Your Support

Give a ⭐️ if this project helped you!



