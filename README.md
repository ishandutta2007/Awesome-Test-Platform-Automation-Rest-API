# Awesome-Test-Platform-Automation-Rest-API

# Awesome Test Platform Automation REST API

> A curated list of top Test Platform Automation REST API platforms — both SaaS/Hosted commercial test infrastructure APIs and open-source alternatives for programmatic control of test execution, session management, and CI/CD integration.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [BrowserStack Platform API](#browserstack-platform-api)
  - [Sauce Labs REST API](#sauce-labs-rest-api)
  - [LambdaTest Automation API](#lambdatest-automation-api)
  - [Cypress Cloud API](#cypress-cloud-api)
  - [CircleCI API](#circleci-api)
- [Open-Source Software](#-open-source-software)
  - [TestHub](#testhub)
  - [Karate](#karate)
  - [TestRail API Wrapper](#testrail-api-wrapper)
  - [Apache Guacamole (API)](#apache-guacamole-api)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Test Platform Automation REST APIs. These are not open-source but are included as reference points for feature comparison.

### BrowserStack Platform API
**Type:** Programmatic control of browser workers and test sessions
The BrowserStack Automate API provides REST endpoints for creating and managing browser workers (sessions), retrieving available browsers/devices, and querying session status. Authentication uses HTTP Basic Auth with username and access key. Key endpoints include `GET /browsers` for listing supported browsers and `POST /worker` for spawning a new browser instance with parameters like OS, browser version, URL, and timeout [citation:1]. The API returns a worker ID that can be used for further session control. There is also a .NET client library (`MartinCostello.BrowserStack.Automate`) that wraps the REST API with features including querying plan status, listing/deleting builds and sessions, and regenerating access keys .
**Best for:** Teams wanting programmatic control over BrowserStack test sessions for custom CI/CD orchestration or building internal tooling around their cloud testing infrastructure.

### Sauce Labs REST API
**Type:** Full lifecycle management for test jobs, builds, and devices
Sauce Labs provides a comprehensive REST API covering jobs, builds, devices, tunnels (Sauce Connect), and account information. Available operations include `list_jobs`, `get_job`, `update_job`, `stop_job`, and `delete_job`, with visibility and custom metadata updates for VDC jobs [citation:2]. The API also exposes device catalog management, tunnel inspection, and user concurrency queries. Authentication is HTTP Basic Auth with regional data center selection (US West, US East, Europe, Asia South). Python and other client libraries exist for programmatic access [citation:15].
**Best for:** Teams needing deep programmatic control over Sauce Labs test infrastructure, particularly for custom dashboards, automated cleanup, or integration with internal test management systems.

### LambdaTest Automation API
**Type:** Build and session management for cloud test execution
LambdaTest (now TestMu AI) provides a Node.js REST client (`@lambdatest/node-rest-client`) for interacting with its Automation API. The client supports fetching builds, managing sessions, and handling tunnels for local testing [citation:3]. Authentication uses username and access key set as environment variables. The API is part of LambdaTest's broader platform supporting Selenium, Appium, Playwright, and other frameworks.
**Best for:** Node.js teams wanting a lightweight client library for programmatic LambdaTest build and session management.

### Cypress Cloud API
**Type:** Test analytics and reporting data extraction
Cypress Cloud provides a Data Extract API for retrieving test analytics data including project lists, spec counts, run durations, and flaky test details. The API supports reports like `project-list`, `average-passing-build-duration`, `flake-per-project-over-time`, and `top-flaky-per-project` [citation:4]. Data is available near real-time (30 minutes after run completion), with a maximum of 500,000 records per request. Authentication uses a token parameter. This is an analytics extraction API rather than a test execution control API.
**Best for:** Teams wanting to export Cypress Cloud test analytics into external dashboards or data warehouses for trend analysis and flaky test tracking.

### CircleCI API
**Type:** CI/CD pipeline and workflow automation
CircleCI's API v3 provides REST endpoints for managing workflows, pipelines, and jobs. List operations require scope filters like `filter[org_id]` or `filter[project_id]` and return 400 without them [citation:9]. The API follows REST conventions with GET, POST, PUT, and DELETE methods (no PATCH). Error responses include a single `error` object with type, title, and detail fields. Rate limiting returns 429 with `Retry-After` and `RateLimit-Policy` headers. This is CI/CD orchestration rather than test-specific session management.
**Best for:** Teams wanting programmatic control over CircleCI pipelines that run their test suites, including triggering builds and retrieving workflow status.

---

## 🟩 Open-Source Software

Self-hosted, community-driven tools that provide REST APIs for test management, automation, or remote session control.

### TestHub
**Stack:** Node.js / SQLite | **License:** Open Source (per npm)
TestHub is a local-first test management tool with a full REST API for programmatic control of projects, test cases, plans, and executions. It runs with zero configuration via `npx testhub-app` and stores data locally in SQLite [citation:11]. The API supports CRUD operations for projects, libraries, directories, cases, tags, and plans. Authentication uses an `x-testhub-token` header auto-generated on startup. It includes a built-in `/skill.md` guide and OpenAPI spec for AI agent integration, making it accessible to automation tools and LLM agents. Swagger UI is available at `/api/docs`.
**Best for:** Small teams wanting a lightweight, self-hosted test management API for AI agent integration or custom tooling, without cloud dependencies or complex setup.

### Karate
**Stack:** Java | **License:** Open Source (Apache 2.0)
Karate is an open-source framework that combines API testing, mocks, performance testing, and UI automation in a single tool. While primarily a testing framework rather than a REST API platform, Karate tests are written in a domain-specific language and can be run programmatically via Java or Maven/Gradle, with results accessible for CI integration [citation:12]. It supports contract testing and can serve as a mock server for API dependencies.
**Best for:** Teams wanting an open-source, code-centric API testing framework that can be integrated into automated pipelines, rather than a management API.

### TestRail API Wrapper
**Stack:** Python | **License:** Open Source (per PyPI)
The `testrail-api` Python package provides a programmatic wrapper around TestRail's official REST API. It supports milestones, runs, results, attachments, and other TestRail objects [citation:5]. Example usage includes adding milestones, creating test runs, adding results for cases, and attaching screenshots. Authentication uses URL, email, and password (or environment variables). This is a client library for a commercial platform, not an open-source test platform itself.
**Best for:** Python teams wanting a clean, typed wrapper for the TestRail API to automate test management workflows.

### Apache Guacamole (API)
**Stack:** Java / JavaScript | **License:** Apache 2.0
Apache Guacamole is a clientless remote desktop gateway that includes a documented REST API and JavaScript API for integration into other applications. It supports VNC, RDP, and SSH sessions through a browser, with session recording capabilities [from previous context]. While not a test platform API, it provides programmatic control over remote sessions that could be used for test infrastructure access.
**Best for:** Teams needing an open-source API for controlling remote desktop sessions in test environments, particularly for manual testing or debugging on remote machines.

---

## 📊 Comparison at a Glance

| Software | License | Type | Primary Use | Self-Hosted | Best For |
|----------|---------|------|-------------|-------------|----------|
| **BrowserStack API** | Proprietary | Session control | Worker creation, browser listing | ❌ | Custom test orchestration |
| **Sauce Labs API** | Proprietary | Full lifecycle | Jobs, builds, devices, tunnels | ❌ | Deep infrastructure control |
| **LambdaTest API** | Proprietary | Build management | Builds, sessions, tunnels | ❌ | Node.js client integration |
| **Cypress Cloud API** | Proprietary | Analytics extraction | Flaky tests, durations, reports | ❌ | Data warehouse export |
| **CircleCI API** | Proprietary | CI/CD orchestration | Workflows, pipelines | ❌ | Pipeline automation |
| **TestHub** | Open Source | Test management | Projects, cases, plans | ✅ (local) | Lightweight local API |
| **Karate** | Apache 2.0 | Test framework | API/UI/performance testing | ✅ (code) | Code-centric API testing |
| **TestRail Wrapper** | Open Source | API client | TestRail automation | ❌ (client) | Python TestRail automation |
| **Guacamole** | Apache 2.0 | Remote sessions | VNC/RDP/SSH access | ✅ | Remote test access API |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Test Platform Automation REST API tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem for **test platform automation APIs** is limited compared to commercial offerings. Most open-source projects in this space are either test management tools with APIs (TestHub), testing frameworks (Karate), or client libraries for commercial platforms (TestRail Wrapper). BrowserStack, Sauce Labs, and LambdaTest remain the most comprehensive APIs for programmatic test session control, but they are proprietary SaaS platforms.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
