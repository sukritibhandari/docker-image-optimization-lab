# Docker Image Optimization Lab (Node + Python + Java)
This repo is a hands-on lab to practice Dockerfile optimization across:
- **Node.js** (plain HTTP API)
- **Python** (FastAPI)
- **Java** (Spring Boot)

You’ll compare:
- `slim` vs `alpine` (where feasible)
- caching patterns
- multi-stage builds (esp. Java + Python wheels)
- security hardening (non-root)
- `.dockerignore`, HEALTHCHECK
- optional distroless 

## Quick start (local)
### Build everything
```bash
bash scripts/build_all.sh
