# Caddy Observability with Prometheus

This repository contains a Docker Compose setup for monitoring a Caddy web server using Loki, Grafana, Prometheus.

### Architecture Overview

| Service        | Role                        | Data Source                         | Exposed Port                   |
| :------------- | :-------------------------- | :---------------------------------- | :----------------------------- |
| **Caddy**      | Web Server, Metrics Emitter | Requests made by users              | 80, 443, 2019, 81              |
| **Prometheus** | Metrics Collector           | Scrapes Caddy's Admin API (2019)    | 9090                           |
| **Loki**       | Aggregates logs             | Receives logs from Promtail         | 3100, 4317 (gRPC), 4318 (HTTP) |
| **Promtail**   | Watches logs and ships them | Reads Caddy logs from shared volume | N/A                            |
| **Grafana**    | Visualization & Dashboard   | Queries Prometheus & Loki           | 81                             |

### Quick Start

1.  **Deploy the stack:**
    ```bash
    docker compose up -d
    ```
2.  **Access Grafana:** Open your browser to `http://localhost:81`.
    - **User/Password:** `admin`/`admin`
3.  **Access Caddy:** Open your browser to `http://localhost:80`.

### Persistent Data

All persistent data (metrics, logs, and state) is stored in the local `./volumes` directory.
