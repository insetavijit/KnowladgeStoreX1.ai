# Docker & Containerization

**Core definition:** Packaging your LangGraph agent into a **Container** (standard unit of software) so it runs exactly the same on your laptop as it does in the cloud.

**Position in ecosystem:**
The standard way to deploy agents.

**Key idea:**
- **Dockerfile:** The recipe for building the image.
- **Base Image:** Use `python:3.11-slim` for smaller size.
- **Dependencies:** Copy `requirements.txt` / `pyproject.toml` and install.

## Sample Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "main.py"]
```

## Quick Summaries

**30-second version:** Docker is a shipping container. It doesn't matter if you put the container on a truck, a ship, or a train; the contents (your code) remain arranged exactly the same way inside.

**One-line recall:**
**Docker guarantees your graph works in production exactly as it did in dev.**

---

## Linked Concepts
- [[Environment-Specific Configuration]]
- [[Installing LangGraph]]
- [[Role in Agent Stack]] <!-- From 1.1.1.1 -->

---
**Last updated:** December 2025
