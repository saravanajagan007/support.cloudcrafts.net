# support.cloudcrafts.net Workspace Rules & Guidelines

> [!IMPORTANT]
> **Mandatory Rule Compliance Directives**:
> 1. **Project Rules**: This `rules.md` file is located inside this project root (`/Users/saravanajagan/Projects/support.cloudcrafts.net/rules.md`) and **MUST BE FOLLOWED AT ALL COSTS** by all AI assistants and developers during every session.
> 2. **Global Rules**: The master global rules file is located on pCloud Drive at `/Users/saravanajagan/global-rules.md`. Those global rules **MUST BE FOLLOWED TOO AT ALL COSTS** for UI design standards, quality assurance, security, rate limiting, remote server/database credentials, and Git sync workflows.

---

## 🚀 Project Overview & Architecture
* **Customer Support CRM**: `https://support.cloudcrafts.net` (Chatwoot v3 / Rails 7 + Vue + Sidekiq)
* **WhatsApp Gateway API**: `https://wa.cloudcrafts.net` (Evolution API v2.2.3 / Baileys)
* **Repository**: [`https://github.com/saravanajagan007/support.cloudcrafts.net`](https://github.com/saravanajagan007/support.cloudcrafts.net)

---

## 🖥️ Server & Deployment Configuration
* **VPS Host**: `172.93.49.117`
* **SSH User**: `root`

### 1. Chatwoot Support CRM (`support.cloudcrafts.net`):
* **Path**: `/srv/apps/chatwoot` (Docker Compose)
* **Services**:
  * `chatwoot-web` (`chatwoot/chatwoot:latest`): Rails web server listening on port `3000` (internal)
  * `chatwoot-worker` (`chatwoot/chatwoot:latest`): Sidekiq background task processor
  * `chatwoot-postgres` (`pgvector/pgvector:pg15`): PostgreSQL 15 database with pgvector
* **Redis**: `redis://redis:6379/5`
* **Nginx Configuration**: `/srv/docker/nginx/conf.d/support.cloudcrafts.net.conf` (proxies to `http://chatwoot-web:3000` with `underscores_in_headers on;`)
* **SSL Certificate**: `/etc/letsencrypt/live/support.cloudcrafts.net/`

### 2. Evolution API Gateway (`wa.cloudcrafts.net`):
* **Path**: `/srv/apps/evolution-api` (Docker Compose)
* **Services**:
  * `evolution-api` (`evoapicloud/evolution-api:v2.2.3`): WhatsApp engine on port `8080` (internal, `CONFIG_SESSION_PHONE_VERSION=2.3000.1043857760`)
  * `evolution-postgres` (`postgres:15-alpine`): Dedicated PostgreSQL database
  * `redis` (`redis:6379/4`): High-speed session & event caching
* **Nginx Configuration**: `/srv/docker/nginx/conf.d/wa.cloudcrafts.net.conf` (proxies to `http://evolution-api:8080`)
* **SSL Certificate**: `/etc/letsencrypt/live/wa.cloudcrafts.net/`

---

## 🔑 Credentials & Access Details

### 1. Chatwoot CRM Access:
* **Web Login URL**: [`https://support.cloudcrafts.net/app/login`](https://support.cloudcrafts.net/app/login)
* **SuperAdmin URL**: [`https://support.cloudcrafts.net/super_admin/sign_in`](https://support.cloudcrafts.net/super_admin/sign_in)
* **Admin Email**: `saravanajagan@gmail.com`
* **Admin Password**: `Goldwinner007#`
* **Account**: `CloudCrafts` (ID: `1`)
* **API Access Token**: `LFqENNfz6J4C526Qm4WB6Uom`
* **Connected Inboxes**:
  * `personel`: Linked to WhatsApp number `+91 91765 89951` via Evolution API (Webhook: `https://wa.cloudcrafts.net/chatwoot/webhook/personel`)

### 2. Evolution API Access:
* **Manager UI**: [`https://wa.cloudcrafts.net/manager`](https://wa.cloudcrafts.net/manager)
* **API Base URL**: `https://wa.cloudcrafts.net`
* **Global API Key**: `EvoCloudCrafts_9876543210!`
* **Auth Header**: `apikey: EvoCloudCrafts_9876543210!`
* **Active WhatsApp Instance**: `personel` (Owner: `+91 91765 89951`, Status: `open`)

### 3. API Usage Quick Reference:
* **Send Outbound WhatsApp Message via Evolution API**:
  ```bash
  curl -X POST "https://wa.cloudcrafts.net/message/sendText/personel" \
    -H "apikey: EvoCloudCrafts_9876543210!" \
    -H "Content-Type: application/json" \
    -d '{
      "number": "919876543210",
      "text": "Hello! Reaching out from CloudCrafts."
    }'
  ```

---

## 🔄 Mandatory Access & Git Pull Directive
* **Automatic Git Pull On Access**: Whenever this project workspace directory is accessed by an AI assistant CLI or model, `git pull` MUST be executed immediately to fetch and integrate the latest remote changes from GitHub before performing any reads, edits, or builds.

---

## 🎨 Quality & Testing Rules
* Always run `npm run typecheck` or `npm run build` locally before pushing changes to ensure zero compilation or type errors.
* Maintain mobile-first responsiveness across all inbox, pipeline, and automation views.
