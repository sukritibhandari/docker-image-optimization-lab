# Docker Image Optimization Lab

A hands-on comparison of Docker build strategies across **Node.js**, **Python**, and **Java Spring Boot**, focused on understanding **real-world tradeoffs** in image size, security, build behavior, and runtime operability.

---

## TL;DR

This repository starts with intentionally **naive Dockerfiles** and incrementally evolves them into **production-grade container images** using dependency caching, multi-stage builds, runtime base comparisons (glibc vs Alpine), and security hardening.

Every variant is built and measured in CI to keep conclusions grounded in data.

**Key takeaway:** container optimization is about understanding layering, build systems, and runtime behavior — not just chasing smaller images.

---

## Why this project exists

In many production systems, container images:
- silently grow beyond **500MB–1GB**
- ship build tools into runtime images
- rely on “best practices” without understanding tradeoffs
- introduce avoidable security and operability risks

This lab explores **why those issues happen** and how to fix them systematically.

---

## Technology stacks covered

- **Node.js**
- **Python (FastAPI)**
- **Java Spring Boot (Maven → JRE)**

Each stack follows the same progression:
1. Naive baseline  
2. Dependency caching  
3. Multi-stage builds  
4. Runtime base comparison  
5. Secure, production-ready image  

---

## Image comparison results

### Node.js
| Variant | Size (MB) |
|---|---:|
| node-naive | ~1038 |
| node-slim-cache | ~183 |
| node-alpine-cache | ~121 |
| node-secure | ~183 |

---

### Python (FastAPI)
| Variant | Size (MB) |
|---|---:|
| python-naive | ~1106 |
| python-slim-cache | ~163 |
| python-alpine-singlerun | ~93 |
| python-wheels-multistage | ~171 |
| python-secure | ~172 |

---

### Java (Spring Boot)
| Variant | Size (MB) |
|---|---:|
| java-naive | 523.51 |
| java-multistage-jre17 | 271.89 |
| java-multistage-jre17-alpine | 194.09 |
| java-secure | 293.16 |

---

## Security hardening approach

Secure variants introduce:
- Non-root users with fixed UIDs
- Minimal runtime artifacts (only application binaries)
- Health checks without adding curl or OS tools
- Clear separation of build-time and runtime dependencies

---

## CI-driven validation

All images are:
- Built in CI
- Measured consistently
- Compared across variants

---

## Key takeaways

- Container optimization is a **systems problem**, not a Dockerfile trick.
- Layer immutability explains many image-size surprises.
- Multi-stage builds improve clarity, security, and maintainability.
- Alpine images are powerful when used deliberately.
- Secure defaults can be introduced with minimal overhead.

---

## Repository structure

```
apps/
dockerfiles/
.github/workflows/
```

---

## Possible extensions

- CI guardrails for image size regression
- JVM container-aware memory tuning
- Kubernetes readiness/liveness probes
- Distroless Java runtime comparison