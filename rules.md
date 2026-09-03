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
  * `evolution-api` (`evoapicloud/evolution-api:v2.2.3`): WhatsApp engine on port `8080` (internal)
  * `evolution-postgres` (`postgres:15-alpine`): Persistent PostgreSQL database
  * `redis` (`redis:6379/4`): High-speed session & event caching
* **Web UI (Evolution Manager)**: `https://support.cloudcrafts.net/manager`
* **API URL**: `https://support.cloudcrafts.net`
* **API Key Header**: `apikey: EvoCloudCrafts_9876543210!`
* **Nginx Configuration**: `/srv/docker/nginx/conf.d/support.cloudcrafts.net.conf` (reverse proxying to `http://evolution-api:8080`)
* **SSL Certificate**: Let's Encrypt SSL at `/etc/letsencrypt/live/support.cloudcrafts.net/`
* **Legacy CRM**: PM2 process `support-cloudcrafts` removed; code archived at `/srv/apps/support.cloudcrafts.net.bak`.

---

## 🔄 Mandatory Access & Git Pull Directive
* **Automatic Git Pull On Access**: Whenever this project workspace directory is accessed by an AI assistant CLI or model, `git pull` MUST be executed immediately to fetch and integrate the latest remote changes from GitHub before performing any reads, edits, or builds.

---

## 🎨 Quality & Testing Rules
* Always run `npm run typecheck` or `npm run build` locally before pushing changes to ensure zero compilation or type errors.
* Maintain mobile-first responsiveness across all inbox, pipeline, and automation views.
