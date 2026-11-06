# Open WebUI Deployment

Local deployment of [Open WebUI](https://github.com/open-webui/open-webui) connected to a self-hosted OpenAI-compatible LLM gateway with built-in voice / audio notes transcription (Faster-Whisper) and eLabFTW MCP integration.

---

## Architecture

- **UI & Gateway**: Open WebUI container (`ghcr.io/open-webui/open-webui:v0.12.4`) published on port `3000`.
- **Speech-to-Text (STT)**: Built-in local `faster-whisper` (`base` model, `int8` quantization) running on CPU inside the container for microphone dictation and audio file uploads (`.mp3`, `.wav`, `.m4a`, etc.).
- **Data Persistence**: Named volume `open-webui-data` mapped to `/app/backend/data` (stores users, chats, settings, model cache, and uploads).
- **MCP Integration**: Dual-mounted with `elabftw-mcp` so uploaded voice notes and documents can be processed and linked directly to eLabFTW experiments and projects.

---

## Quick Start

### 1. Prerequisites
- [Podman](https://podman.io/) (or Docker) with Compose support.

### 2. Configure Environment
Copy the example environment file and set your credentials:
```bash
cp .env.example .env
# Edit .env with your gateway URL, API keys, and admin password
```

### 3. Launch Services
```bash
podman compose up -d
```
Access the web interface at:
**http://localhost:3000**

---

## Management Commands

```bash
# View logs
podman logs -f iiia-qwen-open-webui

# Restart
podman restart iiia-qwen-open-webui

# Stop
podman compose down
```
