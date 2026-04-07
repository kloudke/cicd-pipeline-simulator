# CI/CD Pipeline Simulator

A system that allows users to define, execute, and monitor CI/CD pipelines, similar to Jenkins or GitHub Actions.

---

## Architecture Diagram

```
                    +----------------------+
                    |     Frontend UI      |
                    | (Pipeline Dashboard) |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |      Backend API     |
                    |  (Pipeline Manager)  |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |     Job Queue        |
                    |   (Redis / RabbitMQ) |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |     Worker Engine    |
                    |  (Executes Jobs)     |
                    +----------+-----------+
                               |
         +---------------------+----------------------+
         |                                            |
         v                                            v
+----------------------+                +---------------------------+
|   Docker Runtime     |                |   Kubernetes Jobs         |
| (container execution)|                | (scalable execution)      |
+----------------------+                +---------------------------+

                               |
                               v
                    +----------------------+
                    |     PostgreSQL      |
                    | (pipelines, logs)   |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |   Log Streaming      |
                    |   (WebSockets)       |
                    +----------------------+
```

---

## Pipeline Flow

1. User defines pipeline in YAML
2. Backend parses and stores pipeline
3. Job is sent to queue
4. Worker executes pipeline steps
5. Logs are streamed back in real time
6. Status is updated in database

---

## Repository Structure

```
cicd-pipeline-simulator/
│
├── frontend/
│   ├── src/
│   ├── components/
│   │   ├── PipelineEditor/
│   │   ├── JobLogs/
│   │   └── Dashboard/
│   └── Dockerfile
│
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── pipeline-parser/
│   │   ├── queue/
│   │   └── models/
│   └── Dockerfile
│
├── worker/
│   ├── src/
│   │   ├── executors/
│   │   │   ├── docker/
│   │   │   └── kubernetes/
│   │   ├── runner/
│   │   └── logger/
│   └── Dockerfile
│
├── infra/
│   ├── vpc/
│   ├── eks/
│   ├── s3/
│   └── rds/
│
├── k8s/
│   ├── backend/
│   ├── frontend/
│   ├── worker/
│   ├── redis/
│   └── ingress/
│
├── helm/
├── .github/workflows/
└── README.md
```

---

## Key Features

* YAML-based pipeline definitions
* Job queue system
* Containerized execution
* Real-time logs
* Pipeline history tracking

---

## Future Enhancements

* Parallel job execution
* Pipeline caching
* Secrets management
* Artifact storage
* Multi-branch pipelines

---

## Development Order

1. Build CI/CD Pipeline Simulator (MVP first)
2. Add Docker-based execution
3. Introduce Kubernetes jobs
4. Build Metrics Dashboard
5. Integrate both systems

---

## Notes

* Start simple (MVP)
* Focus on functionality before optimization
* Gradually introduce advanced DevOps features
