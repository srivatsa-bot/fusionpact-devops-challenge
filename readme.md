# Fusionpact DevOps Challenge

A full-stack web application demonstrating modern DevOps practices with FastAPI backend, Nginx frontend, comprehensive monitoring, and automated CI/CD pipeline.

## 1) Cloud Deployment

### Prerequisites
- Docker and Docker Compose
- Git
- SSH access to target server

### Quick Start

#### Application Deployment
```bash
# Clone the repository
git clone https://github.com/srivatsa-bot/fusionpact-devops-challenge.git
cd fusionpact-devops-challenge

# Deploy the application stack
docker compose -f docker-compose-app.yml up --build -d
```

#### Monitoring Stack Deployment
```bash
# Deploy monitoring stack
docker compose -f docker-compose-monitoring.yml up -d
```

### Service Endpoints
- **Frontend**: http://localhost:80
- **Backend API**: http://localhost:80/api
- **Metrics**: http://localhost:80/metrics
- **Prometheus**: http://localhost:9090
- **Grafana**: http://localhost:3000
- **Node Exporter**: http://localhost:9100



## 2) Monitoring & Observability

### Monitoring Stack Components

#### Prometheus Configuration
- **Scrape Interval**: 15 seconds
- **Targets**:
  - Prometheus self-monitoring (port 9090)
  - FastAPI application metrics (port 8888)
  - Node Exporter system metrics (port 9100)

#### Node Exporter
- **System Metrics**: CPU, memory, disk, network
- **Host Mode**: Direct access to host system metrics
- **Port**: 9100

#### Grafana Dashboards
- **Default Port**: 3000
- **Data Source**: Prometheus
- **Visualization**: System metrics, application performance, custom dashboards


### Metrics Collection
- **Application Metrics**: Request rates, response times, error rates
- **System Metrics**: CPU usage, memory consumption, disk I/O


## 3) CI/CD Automation

### Jenkins Pipeline Overview

The Jenkins pipeline implements a complete CI/CD workflow with the following stages:

#### Pipeline Stages

1. **Checkout**
   - Clean workspace
   - Clone repository from GitHub

2. **Build**
   - Build Docker images
   - Start application stack
   - Wait for services to initialize

3. **Testing Frontend**
   - Verify frontend accessibility using curl

4. **Testing Backend**
   - API endpoint validation
   - User creation and retrieval tests
   - Metrics endpoint verification

5. **Deployment**
   - SSH into FastAPI server
   - Perform `docker compose down` to remove existing application stack
   - Execute `git pull origin main` to update the infrastructure code
   - Run `docker compose -f docker-compose-app.yml up --build -d` to deploy updated application


### Local Development
```bash
# Start application
docker compose -f docker-compose-app.yml up --build

# Start monitoring
docker compose -f docker-compose-monitoring.yml up -d

# View logs
docker compose logs -f
```

### Production Deployment
```bash
# SSH into server and deploy
ssh user@server 'cd /path/to/project && docker compose -f docker-compose-app.yml up --build -d'
```

### Monitoring Setup
1. Access Grafana at http://localhost:3000
2. Configure Prometheus as data source
3. Import monitoring dashboards
4. Set up alerting rules
