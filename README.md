# 🚀 AWS Observability Stack

## 🧱 Tech Stack

- AWS EC2 (Ubuntu)
- Node.js / Backend Framework
- PostgreSQL
- Prometheus (Metrics collection)
- Node Exporter (System metrics)
- Grafana (Visualization)
- Alertmanager (Email alerts via SMTP)

---

## ⚙️ Setup Instructions

### 1️⃣ Launch EC2 Instance
- Ubuntu 22.04 recommended
- Open ports:
  - 22 (SSH)
  - 3000 (Backend)
  - 3001 (Grafana)
  - 9090 (Prometheus)
  - 9093 (Alertmanager)

---
## 📧 SMTP Email Alert Configuration

Alertmanager is configured with SMTP for sending system alerts.

 sudo tee /etc/alertmanager/alertmanager.yml > /dev/null <<'EOF'
global:
  resolve_timeout: 5m
  smtp_smarthost: 'smtp.gmail.com:587'     # Replace with your SMTP server & port
  smtp_from: 'tariqulislamtazim99@gmail.com'   # The sender email address
  smtp_auth_username: 'tariqulislamtazim99@gmail.com'
  smtp_auth_password: 'twft zynr atyk csmp' # Your email SMTP app password
  smtp_require_tls: true

route:
  group_by: ['alertname', 'server']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 3h
  receiver: 'email-receiver'

receivers:
  - name: 'email-receiver'
    email_configs:
      - to: 'tariqulislamtazim99@gmail.com' # Where alerts will be sent
        send_resolved: true                   # Sends a follow-up email when fixed
        headers:
          subject: '[Alert] {{ .Status | toUpper }} - {{ .GroupLabels.alertname }}'
        html: |
          <h3>Alert: {{ .GroupLabels.alertname }}</h3>
          <p><strong>Status:</strong> {{ .Status }}</p>
          <p><strong>Severity:</strong> {{ .CommonLabels.severity }}</p>
          <hr/>
          <h4>Details:</h4>
          <ul>
            {{ range .Alerts }}
              <li>
                <strong>Description:</strong> {{ .Annotations.description }}<br/>
                <strong>Instance:</strong> {{ .Labels.instance }}<br/>
                <strong>Started at:</strong> {{ .StartsAt }}
              </li>
            {{ end }}
          </ul>
EOF

## 📊 Screenshots

<img src="assets\ApplicationRunning.png" alt="Prometheus Dashboard" width="800"/>
<img src="assets\GrafanaDashboard.png" alt="Prometheus Dashboard" width="800"/>
<img src="assets\GrafanaRunning.png" alt="Prometheus Dashboard" width="800"/>
<img src="assets\PromethusAndPromtailInstalled.png" alt="Prometheus Dashboard" width="800"/>
<img src="assets\PromethusRunning.png" alt="Prometheus Dashboard" width="800"/>

---
