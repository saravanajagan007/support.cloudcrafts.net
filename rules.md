# support.cloudcrafts.net Workspace Rules & Guidelines

> [!IMPORTANT]
> **Mandatory Rule Compliance Directives**:
> 1. **Project Rules**: This `rules.md` file is located inside this project root (`/Users/saravanajagan/Projects/support.cloudcrafts.net/rules.md`) and **MUST BE FOLLOWED AT ALL COSTS** by all AI assistants and developers during every session.
> 2. **Global Rules**: The master global rules file is located on pCloud Drive at `/Users/saravanajagan/global-rules.md`. Those global rules **MUST BE FOLLOWED TOO AT ALL COSTS** for UI design standards, quality assurance, security, rate limiting, remote server/database credentials, and Git sync workflows.

---

## 🚀 Project Overview & Architecture
* **Project Name**: `support.cloudcrafts.net` (WhatsApp CRM & Support Platform)
* **Domain / Subdomain**: `support.cloudcrafts.net`
* **Repository**: [`https://github.com/saravanajagan007/support.cloudcrafts.net`](https://github.com/saravanajagan007/support.cloudcrafts.net)
* **Tech Stack**:
  * **Framework**: Next.js 16 (App Router) + React 19 + TypeScript
  * **Styling**: Tailwind CSS v4 + Lucide Icons + Shadcn UI
  * **Database & Auth**: Supabase (Postgres + Auth + Storage)
  * **Integrations**: Meta WhatsApp Business Cloud API, OpenAI / Anthropic AI reply assistant

---

## 🖥️ Server & Deployment Configuration
* **VPS Host**: `172.93.49.117`
* **SSH User**: `root`
* **Deployment Path**: `/srv/apps/evolution-api` (Docker Compose)
* **Services**:
  * `evolution-api` (`evoapicloud/evolution-api:v2.2.3`): WhatsApp engine on port `8080` (internal, `CONFIG_SESSION_PHONE_VERSION=2.3000.1043857760`)
  * `evolution-postgres` (`postgres:15-alpine`): Persistent PostgreSQL database
  * `redis` (`redis:6379/4`): High-speed session & event caching
* **Nginx Configuration**: `/srv/docker/nginx/conf.d/support.cloudcrafts.net.conf` (reverse proxying to `http://evolution-api:8080`)
* **SSL Certificate**: Let's Encrypt SSL at `/etc/letsencrypt/live/support.cloudcrafts.net/`
* **Legacy CRM**: PM2 process `support-cloudcrafts` removed; code archived at `/srv/apps/support.cloudcrafts.net.bak`.

---

## 🔑 Evolution API Credentials & Access Details

### 1. Web Manager UI & API Gateway:
* **Evolution Manager (Web UI)**: [`https://support.cloudcrafts.net/manager`](https://support.cloudcrafts.net/manager)
* **API Base URL**: `https://support.cloudcrafts.net`
* **Global API Key**: `EvoCloudCrafts_9876543210!`
* **Auth Header**: `apikey: EvoCloudCrafts_9876543210!`

### 2. Internal Database & Cache Credentials:
* **PostgreSQL Service**: `evolution-postgres:5432` (internal Docker network `srv_default`)
  * **Database Name**: `evolution`
  * **Database User**: `evolution`
  * **Database Password**: `EvoPostgres_9876543210!`
  * **Connection URI**: `postgresql://evolution:EvoPostgres_9876543210!@evolution-postgres:5432/evolution`
* **Redis Cache**:
  * **URI**: `redis://redis:6379/4` (Database index 4 on existing Redis container)
  * **Prefix Key**: `evolution`

### 3. Persistent Data Volumes (on VPS):
* `/srv/apps/evolution-api/data/postgres`: PostgreSQL database files
* `/srv/apps/evolution-api/data/instances`: Baileys session data, encryption keys & tokens
* `/srv/apps/evolution-api/data/store`: WhatsApp chats, messages, and contact store

### 4. Basic API Usage Quick Reference:
* **Fetch All Instances**:
  ```bash
  curl -X GET "https://support.cloudcrafts.net/instance/fetchInstances" \
    -H "apikey: EvoCloudCrafts_9876543210!"
  ```
* **Send Text Message (No 24h Window / No Template Needed)**:
  ```bash
  curl -X POST "https://support.cloudcrafts.net/message/sendText/<instance-name>" \
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
