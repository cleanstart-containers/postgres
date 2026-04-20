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


## Documentation Resources
Essential links and resources for further information
 
**CleanStart Images**: https://images.cleanstart.com/
 
**Community Images**:<br>
**Docker Hub**: https://hub.docker.com/u/cleanstart<br>
**GitHub**: https://github.com/cleanstart-containers<br>
**AWS ECR Public Gallery**: https://gallery.ecr.aws/cleanstart/
 
**Presence on Social Media**:<br>
**Community**: https://www.linkedin.com/groups/18324021/<br>
**YouTube**: https://www.youtube.com/@CleanStartOfficial<br>
 
**Contribute to Container Use Cases**: https://github.com/cleanstart-dev/cleanstart-use-cases/
