Grafana + Prometheus + Node Exporter Monitoring Lab (RHEL 10)
Project Overview
This project demonstrates a complete monitoring solution deployed on a RHEL 10 Virtual Machine using:

Grafana
Prometheus
Node Exporter
The solution provides:

CPU Monitoring
Memory Monitoring
Disk Utilization Monitoring
Server Health Monitoring
Network Monitoring
Alerting Foundation for Backup Infrastructure
This lab can be extended to monitor:

Veeam Backup & Replication
Commvault
Backup Repositories
Storage Utilization
Backup Success/Failure Status
Architecture
Node Exporter (9100)
        |
        v
Prometheus (9091)
        |
        v
Grafana (3000)
        |
        v
Email / Dashboard Alerts
Environment
Component	Version
RHEL	10
Grafana	Latest
Prometheus	3.16.0
Node Exporter	1.12.1
Hypervisor	VirtualBox
Monitoring Server	RHEL VM
Installation Steps
Install Grafana
sudo dnf install grafana -y
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
Install Prometheus
./prometheus --config.file=prometheus.yml --web.listen-address=:9091
Install Node Exporter
./node_exporter
Prometheus Configuration
prometheus.yml

global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9091"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["localhost:9100"]
Monitoring Dashboard
Grafana Dashboard
Grafana Dashboard

Features:

CPU Usage
Memory Usage
Filesystem Utilization
Network Monitoring
Server Health
Prometheus Targets
Prometheus Targets

Healthy Targets:

Prometheus
Node Exporter
Alerting
Example Alert Rules:

CPU Usage
100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
Threshold:

Above 85%
Memory Usage
(1-(node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes))*100
Threshold:

Above**0%
*--

Disk Utilization
100 - (
node_files*stem_avail_bytes{mountpoint*"/"}
/
node_filesystem_size_bytes{*ount*oint="/"}
*100
)
Threshold*

Above 80%
*--

Future Enhancements
Vee*m Backup Monitoring
Commvault Mo*itoring
Backup Failure Alerts
*epository Capacity Monitoring
Email Notifications
Microsoft*Teams Notifications
SLA*Dashboard
Capacity Forecast*ng
Author
Vipin Tanwar* Backup Engineer - L2

Techn*logies:

V*eam Backup & Replication
Commv*ult
Grafana
Prometheus
Linux Administration
InfrastrucureMonitoring
