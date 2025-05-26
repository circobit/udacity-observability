# 📊 AWS Observability Stack: EC2 and EKS Monitoring with Prometheus & Grafana

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-%23E6522C.svg?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-%23F46800.svg?style=for-the-badge&logo=grafana&logoColor=white)
![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)

## 📖 Overview

This project sets up a complete observability stack using **Terraform**, **Prometheus**, and **Grafana** to monitor both EC2 and EKS resources. It includes alerting rules for key metrics like CPU, memory, network usage, and application availability. Additional tools like **Blackbox Exporter** and **Postman collections** are included for active endpoint testing and validation.

> ⚠️ **Disclaimer:**  
> This project is intended as a demonstration of observability concepts and SRE practices.  
> It is not hardened for production use and intentionally omits concerns such as authentication, encryption, network security, and cost optimization to focus on the core monitoring stack and alerting pipeline.

---

## 🗂️ Project Structure

```
.
├── document/
│   └── SRE Project Template – Observing Cloud Resources.pdf
├── screenshots/
│   └── *.png (dashboard + alerts)
├── starter/
│   ├── terraform/             # Infra code (modularized)
│   │   ├── main.tf
│   │   └── modules/{vpc,ec2,eks}
│   ├── prometheus-additional.yaml
│   ├── blackbox-values.yaml
│   ├── debug-pod.yaml
│   ├── values.yaml            # Helm override values
│   ├── SRE-Project.postman_environment.json
│   └── SRE-Project-postman-collection.json
└── README.md
```

---

## 🚀 How to Use

### 🔧 Terraform Setup

1. **Initialize Terraform:**
   ```bash
   cd starter/terraform
   terraform init
   ```

2. **Deploy the infrastructure:**
   ```bash
   terraform apply
   ```

> This will create VPC, EC2 instances, and an EKS cluster with IAM and networking preconfigured.

---

### 📈 Deploy Monitoring Stack

1. **Configure Prometheus**
   - Edit `prometheus-additional.yaml` to define scrape targets and alert rules.

2. **Install using Helm:**
   ```bash
   helm upgrade --install prometheus prometheus-community/prometheus \
     -f starter/values.yaml
   ```

3. **Add Blackbox Exporter (for HTTP endpoint checks):**
   ```bash
   helm upgrade --install blackbox-exporter prometheus-community/prometheus-blackbox-exporter \
     -f starter/blackbox-values.yaml
   ```

---

### 📬 Alerts & Dashboards

- Alerts are defined in `prometheus-additional.yaml`
- Dashboards are accessed via:
  - **Grafana on EC2**: `http://<ec2-ip>:3000`
  - **Grafana on EKS**: use LoadBalancer IP from `kubectl get svc`

---

### 🧪 Postman Tests

Run included Postman collections to simulate endpoint monitoring and observe alerts.

- Open `starter/SRE-Project-postman-collection.json` in Postman
- Use `starter/SRE-Project.postman_environment.json` for test environment setup

---

## 🧰 Tools & Technologies

- **AWS EC2, EKS**
- **Terraform** – Infrastructure provisioning
- **Prometheus & Alertmanager** – Metrics + alerting
- **Grafana** – Dashboards
- **Blackbox Exporter** – Endpoint probes
- **Postman** – Manual test collections

---

## 📸 Screenshots

Visuals include:
- Node Exporter setup
- Prometheus and Grafana dashboards
- Memory, CPU, and network alerts
- Blackbox probe results

(See `/screenshots` folder)

---

## 🙌 Author

Made with ❤️ and 🧉 by [Cristian Cevasco](https://github.com/circobit)
