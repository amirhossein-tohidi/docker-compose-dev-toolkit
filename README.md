# 🐳 Docker Compose Dev Toolkit

# Hi, I'm **Amirhossein Tohidi** 👋

> ⚠️ **Note**
>
> Built for **Docker Desktop** on a developer machine.
>
> I created this repository to make local development easier for my projects and for anyone who wants ready-to-run Docker services. Clone the repo, open the service folder you need, and run it with Docker Compose.
>
> If you need another service or have an idea to improve this collection, let me know and I can add it.

## ✨ What You Get

- ✅ Ready-to-use `docker-compose.yml` files
- ✅ Default `.env` files included, so fresh clones work immediately
- ✅ `.env.example` files for quick reference
- ✅ Stable Docker named volumes for persistent services
- ✅ No fixed `container_name`, so fewer conflicts with existing containers
- ✅ Service-specific `RUN_GUIDE.txt` files
- ✅ Local development credentials included in each service `.env`

## 🚀 Quick Start

1. Install and start **Docker Desktop**.
2. Clone this repository.
3. Open PowerShell or CMD in the repository root.
4. Enter the service folder you need.
5. Run Docker Compose.

Example:

```powershell
cd ".\Redis\Stable Redis"
docker compose up -d
docker compose ps
```

If your Docker installation uses the legacy Compose command, replace `docker compose` with `docker-compose`:

```powershell
docker-compose up -d
```

## 📦 Included Services

| Service | Image / Version | Folder | Default ports |
| --- | --- | --- | --- |
| 🟢 MongoDB | `mongo:7.0` | `Mongo/Stable MongoDB` | `27017` |
| 🔴 Redis | `redis:7.4-alpine` | `Redis/Stable Redis` | `6379` |
| 🟦 SQL Server | `mcr.microsoft.com/mssql/server:2022-latest` | `Sql/Stable SQL Server` | `1433` |
| 🟡 ClickHouse | `clickhouse/clickhouse-server:25.3` | `ClickHouse/Stable ClickHouse` | `8123`, `9000` |
| 🟣 Kafka Stack | `confluentinc/cp-kafka:7.6.1`, `confluentinc/cp-zookeeper:7.6.1`, `tchiotludo/akhq:0.24.0` | `Kafka/Stable Kafka Zookeeper AKHQ` | `9092`, `2181`, `8080` |
| 🔐 HashiCorp Vault | `hashicorp/vault:1.19` | `hashicorpVault/Local Vault` | `8200` |
| 📊 Elastic Observability | Elastic Stack `9.4.1` | `Monitoring/Elastic Observability` | `9200`, `5601`, `8201` |
| 📈 Prometheus | `quay.io/prometheus/prometheus:v3.11.3` | `Monitoring/Prometheus` | `9090` |
| 📉 Grafana | `grafana/grafana-enterprise:13.0.1-security-01` | `Monitoring/Grafana` | `3000` |

## 🗂️ Folder Contents

Each service folder contains:

- `docker-compose.yml`: the Compose file for running the service
- `.env`: ready-to-use default settings
- `.env.example`: sample settings for reference
- `RUN_GUIDE.txt`: step-by-step run guide for that service

## 🔗 Default URLs

| Service | URL / Address | Login |
| --- | --- | --- |
| MongoDB | `localhost:27017` | `admin` / `Abcd@1234` |
| Redis | `localhost:6379` | Password: `Abcd@1234` |
| SQL Server | `localhost,1433` | `sa` / `Abcd@1234` |
| ClickHouse HTTP | `http://localhost:8123` | `admin` / `Abcd@1234` |
| ClickHouse Play UI | `http://localhost:8123/play` | `admin` / `Abcd@1234` |
| ClickHouse Dashboard | `http://localhost:8123/dashboard` | `admin` / `Abcd@1234` |
| ClickHouse Health Check | `http://localhost:8123/ping` | Not required |
| ClickHouse Native TCP | `localhost:9000` | `admin` / `Abcd@1234` |
| AKHQ | `http://localhost:8080` | Not required |
| Vault | `http://localhost:8200` | Token: `local-root-token` |
| Elasticsearch | `http://localhost:9200` | Not required |
| Kibana | `http://localhost:5601` | Not required |
| Kibana Elasticsearch | `http://localhost:5601/app/elasticsearch/getting_started` | Not required |
| Kibana APM | `http://localhost:5601/app/apm` | Not required |
| APM Server | `http://localhost:8201` | Token not required |
| Prometheus | `http://localhost:9090` | Not required |
| Grafana | `http://localhost:3000` | `admin` / `Abcd@1234` |

## ⚙️ Configuration

Every service includes default values in `.env`, so a fresh clone works without creating extra files.

If a default port is already in use on your machine, edit the matching port value in that service's `.env` file and run Compose again.

For example, if Redis port `6379` is busy:

```env
REDIS_PORT=6380
```

Then run:

```powershell
docker compose up -d
```

## 🧾 Service Details

### 🟢 MongoDB

| Item | Value |
| --- | --- |
| Image | `mongo:7.0` |
| Host | `localhost` |
| Port | `27017` |
| Default database | `appdb` |
| Authentication database | `admin` |
| Username | `admin` |
| Password | `Abcd@1234` |
| Connection string | `mongodb://admin:Abcd%401234@localhost:27017/appdb?authSource=admin` |
| Volumes | `mongodb-data`, `mongodb-config` |

Good for local APIs, backend apps, and projects that need a ready MongoDB instance.

### 🔴 Redis

| Item | Value |
| --- | --- |
| Image | `redis:7.4-alpine` |
| Host | `localhost` |
| Port | `6379` |
| Persistence | AOF enabled with `--appendonly yes` |
| Password | `Abcd@1234` |
| Connection string | `redis://:Abcd%401234@localhost:6379/0` |
| Volume | `redis-data` |

Great for caching, queues, sessions, rate limiting, and lightweight local experiments.

### 🟦 SQL Server

| Item | Value |
| --- | --- |
| Image | `mcr.microsoft.com/mssql/server:2022-latest` |
| Server | `localhost,1433` |
| Edition | `Developer` |
| Trust server certificate | `True` |
| Username | `sa` |
| Password | `Abcd@1234` |
| Volume | `sqlserver-data` |

Useful for .NET projects, reporting tools, integration tests, and local database work.

### 🟡 ClickHouse

| Item | Value |
| --- | --- |
| Image | `clickhouse/clickhouse-server:25.3` |
| HTTP endpoint | `http://localhost:8123` |
| Play UI | `http://localhost:8123/play` |
| Dashboard | `http://localhost:8123/dashboard` |
| Health check | `http://localhost:8123/ping` |
| Native TCP endpoint | `localhost:9000` |
| Database | `default` |
| Username | `admin` |
| Password | `Abcd@1234` |
| Volumes | `clickhouse-data`, `clickhouse-logs` |

Helpful for analytics, event data, logs, dashboards, and high-speed local queries.

### 🟣 Kafka + ZooKeeper + AKHQ

| Item | Value |
| --- | --- |
| Kafka image | `confluentinc/cp-kafka:7.6.1` |
| ZooKeeper image | `confluentinc/cp-zookeeper:7.6.1` |
| AKHQ image | `tchiotludo/akhq:0.24.0` |
| Kafka bootstrap server | `localhost:9092` |
| ZooKeeper port | `2181` |
| AKHQ UI | `http://localhost:8080` |
| AKHQ login | Not required |
| Auto topic creation | Enabled |
| Default partitions | `3` |
| Log retention | `168` hours |
| Volumes | `kafka-data`, `zookeeper-data`, `zookeeper-log` |

Includes AKHQ so you can inspect topics, messages, consumers, and Kafka state from a browser.

### 🔐 HashiCorp Vault

| Item | Value |
| --- | --- |
| Image | `hashicorp/vault:1.19` |
| Mode | Dev mode |
| UI | `http://localhost:8200` |
| Login token | `local-root-token` |
| Purpose | Local development only |

> Vault dev mode is not a production setup. Data should not be treated as reliable after container deletion or recreation.

### 📊 Elasticsearch + Kibana + APM

| Item | Value |
| --- | --- |
| Elasticsearch image | `elasticsearch:9.4.1` |
| Kibana image | `kibana:9.4.1` |
| APM Server image | `elastic/apm-server:9.4.1` |
| Elasticsearch endpoint | `http://localhost:9200` |
| Kibana UI | `http://localhost:5601` |
| Kibana Elasticsearch page | `http://localhost:5601/app/elasticsearch/getting_started` |
| APM endpoint | `http://localhost:8201` |
| Kibana APM page | `http://localhost:5601/app/apm` |
| Kibana menu path | `Observability` -> `APM and User Experience` |
| Dashboard | Kibana |
| Login | Not required |
| APM secret token | Not required |
| Volumes | `elastic-observability-elasticsearch-data`, `elastic-observability-kibana-data` |

Good for logs/search experiments and application performance monitoring. Kibana is the dashboard for this stack.

> Elasticsearch security is disabled in this local stack to keep setup simple. Do not use this configuration for production.

### 📈 Prometheus

| Item | Value |
| --- | --- |
| Image | `quay.io/prometheus/prometheus:v3.11.3` |
| UI | `http://localhost:9090` |
| Dashboard | Built-in Prometheus UI for queries, targets, alerts, and simple graphs |
| Login | Not required |
| Volume | `prometheus-data` |

Prometheus collects and stores metrics. Its built-in UI is useful for PromQL and checks, but Grafana is better for polished dashboards.

### 📉 Grafana

| Item | Value |
| --- | --- |
| Image | `grafana/grafana-enterprise:13.0.1-security-01` |
| UI | `http://localhost:3000` |
| Dashboard | Grafana |
| Default datasource | Prometheus at `http://host.docker.internal:9090` |
| Username | `admin` |
| Password | `Abcd@1234` |
| Volume | `grafana-data` |

Grafana is a separate dashboard tool. It can visualize Prometheus metrics, Elasticsearch data, and many other datasources.

## 💾 Data Persistence

Services that need persistent data use Docker named volumes. You do not need to create local data folders manually.

This command stops a service without deleting its data:

```powershell
docker compose down
```

This command deletes the service data volumes:

```powershell
docker compose down -v --remove-orphans
```

Use the reset command only when you intentionally want to delete the data.

## 🧹 Useful Commands

Show running containers for the selected service:

```powershell
docker compose ps
```

View logs:

```powershell
docker compose logs -f
```

Restart a service:

```powershell
docker compose restart
```

Stop a service:

```powershell
docker compose down
```

## ⚠️ Notes

- Run commands from inside the selected service folder unless its `RUN_GUIDE.txt` says otherwise.
- These Compose files are intended for local development, not production.
- Local credentials are intentionally included in service `.env` files because this repository is designed for easy local setup.
- If a port is already in use, edit the related value in that service's `.env` file.
- Docker Desktop factory reset, `docker compose down -v`, or `docker volume prune` can delete Docker volumes.
