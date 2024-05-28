# Monitoring

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project is a monitoring tool using Node Exporter, Alert Manager, Prometheus and Grafana in a docker-compose environment.

## Installation

1. Clone the repository
```bash
git clone https://github.com/PierreDubosq/Monitoring.git
```

2. Go to the project directory
```bash
cd Monitoring
```

3. Update the `alertmanager/alertmanager.yml` file with your email address
```yaml
route:
  receiver: "Mail Alert"
  group_by: [alertname]
  repeat_interval: 30s
  group_wait: 15s
  group_interval: 15s

receivers:
  - name: "Mail Alert"
    email_configs:
      - smarthost: "..." # SMTP server. Ex: smtp.gmail.com:587
        auth_username: "..." # SMTP username
        auth_password: "..." # SMTP password
        from: "prometheus@alertmanager.com"
        to: "..." # Email address to send alerts to
        headers:
          subject: "Prometheus Mail Alerts"
```

4. Add the `GRAFANA_USERNAME`, `GRAFANA_PASSWORD` and `GRAPHANA_PORT` environment variables to the environment
```bash
export GRAFANA_USERNAME=admin
export GRAFANA_PASSWORD=admin
export GRAFANA_PORT=3000
```

5. Start the monitoring stack
```bash
docker-compose up -d
```

## Usage

1. Access Grafana at `http://localhost:${GRAFANA_PORT}` and login with the credentials you set in the environment variables

2. Go to `Dashboards` and load the Node Exporter Full dashboard

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.