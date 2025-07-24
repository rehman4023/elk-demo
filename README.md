# 🧰 ELK Stack on Kubernetes (Helm-based)

This repository provides a simple, production-friendly setup to deploy the **ELK Stack** (Elasticsearch, Logstash, Kibana) along with **Filebeat** on Kubernetes using **Helm charts**.

> ✅ Centralized logging for container workloads\
> 🧑‍💻 Ideal for DevOps, SREs, and Platform Engineers\
> ⚙️ All resources are deployed in a dedicated `elk` namespace

---

## 📆 Stack Overview

| Component     | Description                                                            |
| ------------- | ---------------------------------------------------------------------- |
| Elasticsearch | Stores logs as structured documents and indexes them for fast querying |
| Logstash      | Parses and filters logs received from Filebeat                         |
| Kibana        | UI for searching, visualizing, and analyzing logs                      |
| Filebeat      | Collects container logs from all nodes and ships them to Logstash      |

---

## 🚀 Quickstart

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/rehman4023/elk-demo.git
cd elk-stack-on-k8s
```

### 2️⃣ Create the `elk` Namespace

```bash
kubectl create namespace elk
```

### 3️⃣ Add Elastic Helm Repo

```bash
helm repo add elastic https://helm.elastic.co
helm repo update
```

### 4️⃣ Install Components

```bash
helm install elasticsearch elastic/elasticsearch -n elk -f elasticsearch-values.yaml
helm install logstash elastic/logstash       -n elk -f logstash-values.yaml
helm install kibana    elastic/kibana        -n elk -f kibana-values.yaml
helm install filebeat  elastic/filebeat      -n elk -f filebeat-values.yaml
```

---

## 🔍 Access Kibana

```bash
kubectl port-forward service/kibana-kibana -n elk 8080:5601
```

Open [http://localhost:8080] in your browser.

Once Kibana is up:

1. Go to **Discover**
2. Create a data view with pattern `filebeat-*`
3. Start analyzing your logs!

---

## 📈 Customizations

- Enable persistence for Elasticsearch by editing `elasticsearch-values.yaml`
- Add Grok filters or pipeline configurations in `logstash-values.yaml`
- Include additional Filebeat modules (system, nginx, mysql, etc.) in `filebeat-values.yaml`
- Secure your cluster with TLS and basic auth

---

## 👋 Author

Created by [Rehman Syed ](https://www.linkedin.com/in/rehman-syed-88b068125/)

---

⭐ If this helped you, please give the repo a star! ⭐

