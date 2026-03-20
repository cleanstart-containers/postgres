# 🐘 CleanStart PostgreSQL Container

Official PostgreSQL database container image optimized for enterprise environments with CleanStart security standards.

## 🚀 Quick Start

### Pull Images
```bash
docker pull ghcr.io/cleanstart-containers/postgres:latest
docker pull ghcr.io/cleanstart-containers/postgres:latest-dev
```

### Run Container
```bash
docker run --rm -it --name postgres-db -e POSTGRES_PASSWORD=secure_password ghcr.io/cleanstart-containers/postgres:latest
```

### Production Deployment
```bash
docker run -d --name postgres-prod \
  -p 5432:5432 \
  -e POSTGRES_PASSWORD=secure_password \
  -v postgres_data:/var/lib/postgresql/data \
  --security-opt=no-new-privileges \
  cleanstart/postgres:latest
```

### Docker Compose Setup Complete database service configuration
```bash
version: '3.8'
services:
  postgres:
    image: cleanstart/postgres:latest
    container_name: postgres
    restart: unless-stopped
    ports:
      - "5432:5432"
    environment:
      POSTGRES_PASSWORD: secure_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    security_opt:
      - no-new-privileges:true
volumes:
  postgres_data:
```

### Connect to Database Access database shell for administration
```bash
docker exec -it postgres-prod psql -U postgres
```

### Security & Best Practices
#### Recommended Security Context
```bash
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  runAsGroup: 1000
  readOnlyRootFilesystem: true
  allowPrivilegeEscalation: false
  capabilities:
    drop: ['ALL']
```

## 🌟 Features

- **Complete PostgreSQL Environment**: Server, client tools, and utilities
- **Security Hardened**: Minimal attack surface with FIPS-compliant crypto
- **Cloud Native**: Optimized for microservices and container orchestration
- **Multi-Platform**: Supports linux/amd64 and linux/arm64

## 🏗️ Architecture Support

```bash

# AMD64

docker pull --platform linux/amd64 ghcr.io/cleanstart-containers/postgres:latest

# ARM64

docker pull --platform linux/arm64 ghcr.io/cleanstart-containers/postgres:latest
```

## 🔒 Best Practices

- Use specific image tags for production (avoid `latest`)
- Configure resource limits: memory and CPU constraints
- Enable read-only root filesystem when possible
- Use environment variables for database configuration


## Resources

- **Official Documentation:** https://www.postgresql.org/docs/
- **Provenance / SBOM / Signature:** https://images.cleanstart.com/images/postgres
- **Docker Hub:** https://hub.docker.com/r/cleanstart/postgres
- **CleanStart All Images:** https://images.cleanstart.com
- **CleanStart Community Images:** https://hub.docker.com/u/cleanstart

### Vulnerability Disclaimer

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

Security remains a shared responsibility: CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
