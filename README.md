# MiniStack + StackPort Docker Lab

A Docker Compose lab for running MiniStack (local AWS emulator) and StackPort (web UI) together.

## Setup

```bash
git clone <repository-url>
cd aws-lab
docker compose up -d
```

Open StackPort at http://localhost:8080

Stop everything:

```bash
docker compose down
```

## Architecture

```
Browser -> StackPort :8080 -> MiniStack :4566 (emulated AWS services)
```

- **StackPort** is the web UI, exposed on port `8080`.
- **MiniStack** emulates AWS services, exposed on port `4566`.

Compose puts both containers on a default network, so StackPort reaches MiniStack at `http://ministack:4566`. `ministack` is the service name, which Docker resolves through its internal DNS.

## Configuration

StackPort is pointed at MiniStack through environment variables in `compose.yaml`:

| Variable | Value | Purpose |
|---|---|---|
| `AWS_ENDPOINT_URL` | `http://ministack:4566` | Sends AWS API calls to MiniStack instead of real AWS |
| `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY` | `test` | Dummy credentials (MiniStack doesn't validate them) |
| `AWS_REGION` | `ap-south-1` | Region used for API calls |

## What this teaches

- Docker containers and images
- Docker Compose
- Container networking and service-name DNS
- Port mapping
- Environment variables
- Local AWS emulation
