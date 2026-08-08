# Alvin Ardiansyah Maulana — Portfolio

**Software Engineer** — Performance Engineering · Clean Architecture · Platform Engineering · AI-assisted Development

Bandung, Indonesia · [LinkedIn](https://www.linkedin.com/in/alvin-ardiansyah-maulana-a579b0250/) · alvinardiansyahmaulana@gmail.com

---

I work on **ePuskesmas**, a **national-scale multi-tenant healthcare platform** (**7,000+ puskesmas** across Indonesia, integrated with national health systems BPJS / PCare / Satu Sehat). Because it's a closed production system rather than a single public product, my strongest evidence is **measurable performance impact** on real production workloads. This repo documents the work I'm most proud of, with the numbers to back it up.

---

## 🏆 Showcase 1 — Drug-Stock Export: 90% memory reduction

**Problem.** Exporting 60,000 drug-stock rows to Excel consumed **2 GB of memory** — a real OOM risk on production servers.

**Solution.** Replaced the in-memory spreadsheet builder with **OpenSpout streaming** + a PHP **generator** that yields rows one at a time, writing to disk instead of holding everything in RAM. Later extended to stream directly to **S3** and return a presigned URL, so large exports no longer block the web server.

**Result.**

| Metric | Before | After |
|---|---|---|
| Memory | 2,000 MB | **198 MB** (~90% less) |
| Output format | Excel | Excel (unchanged) |
| Server crash risk | High (OOM) | None |

**Stack:** PHP · Laravel · OpenSpout · S3 · StreamedResponse

---

## 🏆 Showcase 2 — BPJS Visit Synchronization: 95% faster, 100% reliable

**Problem.** Syncing 100 "Kunjungan Sehat" (wellness visit) records to the national BPJS system was slow, unreliable, and resource-hungry.

**Solution.** Request pooling, bulk/batch DB updates, moving query logic into repositories, and dependency inversion.

**Result** (benchmarked on a 2 vCPU / 8 GB server):

| Metric | Before | After |
|---|---|---|
| Process time | 292 s | **14 s** (~95% faster) |
| Success rate | 28% | **100%** |
| DB queries | 192 | **12** |
| CPU usage | 78% | **40%** |
| Memory | 2,800 MB | **70 MB** |

**Stack:** PHP · Laravel · BPJS/PCare API · Repository pattern · Request pooling

---

## 🏆 Showcase 3 — Architecture Standardization: Service-Repository + SOLID + Hexagonal

**Problem.** A legacy codebase with business logic crammed into controllers, no separation of concerns, and no testability.

**Solution.** I was the **first developer** to refactor the legacy system toward the **Service-Repository pattern, SOLID principles, and Hexagonal Architecture** — introducing contracts, repositories, dependency inversion, and unit tests.

**Impact.** The pattern became the **company-wide standard** now used across all new modules. It improved testability, reduced system errors, and made the codebase maintainable.

**Stack:** PHP · Laravel · Service-Repository pattern · SOLID · Hexagonal Architecture · PHPUnit · Codeception

---

## 🏆 Showcase 4 — Agentic AI Workflows for Engineering

**Problem.** Engineering delivery (code review, testing, MR management) was manual and slow.

**Solution.** I adopted and built **agentic AI workflows** (Hermes Agent) to automate code review, test generation, and delivery — refining and building the workflows to fit our team's process.

**Impact.** Accelerated engineering throughput across the team; automated repetitive review and testing work.

**Stack:** Hermes Agent · AI-assisted development · CI/CD

---

## 🏆 Showcase 5 — CoreHub: Feature Toggle & Release Management Platform

**Problem.** Rolling out features across 7,000+ tenant deployments was risky and slow — no way to ship code behind a flag, no centralized release control, and no safe path to continuous delivery.

**Solution.** I built **CoreHub** (Config Service / MKF), an internal **Feature Toggle & Release Management** platform — a full-stack app (Vue 3 + Pinia + PrimeVue frontend, ElysiaJS + Drizzle + PostgreSQL + Valkey backend) with RBAC, audit trails, and a tenant-aware toggle API. I also built the **PHP client library** (`feature-toggle-client`) that lets Laravel apps consume toggles with Redis caching.

**Impact.** CoreHub enabled the team to adopt **Trunk-Based Development** — features ship behind toggles and are released centrally, so delivery is faster and safer. (TBD adoption was team-wide; my contribution was the platform that made it possible.)

**Stack:** TypeScript · Vue 3 · ElysiaJS · Drizzle · PostgreSQL · Valkey · PHP (client library) · RBAC · Audit trail

---

## Other notable work

- **App-level data encryption** — base encryptor, toggle-gated, for sensitive credential fields.
- **CDN migration** — moved tenant-specific static assets to a CDN, reducing latency and origin load.
- **Tagged cache system** — Redis-backed with a NoOp fallback for non-Redis drivers.
- **Tenant isolation** — migrated from a single `APP_WILAYAH_ID` env var to a domain-based resolver.
- **CI/CD** — GitLab CI pipelines and Ansible-based deployment automation.
- **Query optimization** — slow-query fixes on high-traffic endpoints (dashboard, registration, medical records).
- **Deadlock fixes** — reduced DB transaction scope to eliminate deadlocks on high-concurrency operations.

---

## Tech stack

PHP (Laravel) · JavaScript/TypeScript (Vue) · Python · MySQL/MariaDB · Redis · Docker · Git · CI/CD · AWS S3 · REST APIs · Hermes Agent

---

*This portfolio is maintained as a living document. Metrics are from real production benchmarks.*
