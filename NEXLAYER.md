# Nexlayer — social-analyzer

<!-- nexlayer:meta version=1 analyzed=2026-06-05T19:10:36Z repo=https://github.com/KatieHarris2397/social-analyzer branch=main -->

## Project Summary
<!-- nexlayer:section agent-managed=project_summary -->
Social Analyzer is an OSINT tool used to find and analyze social media profiles across 1000+ websites using string analysis, OCR, and web automation. It provides a Web UI, API, and CLI for investigative profile discovery.
<!-- nexlayer:end -->

## Technology Stack
<!-- nexlayer:section agent-managed=tech_stack -->
| Name | Kind | Version | Detected From |
|------|------|---------|---------------|
| Node.js | language | >=20.18.1 | package.json |
| Express | framework | ^4.18.1 | package.json |
| Selenium | tool | 4.3.0 | package.json |
| Python | language | not specified | requirements.txt |
<!-- nexlayer:end -->

## Repository Structure
<!-- nexlayer:section agent-managed=structure_map -->
- app.js — Main Express application entry point
- modules/ — Analysis and detection logic modules
- public/ — Static assets for the Web GUI
- app.py — Python-based analysis components
- test/ — Test suite
<!-- nexlayer:end -->

## External Services Required
<!-- nexlayer:section agent-managed=external_deps -->
Services that must be configured separately (not deployed by Nexlayer):

- Selenium Grid (Hub and Nodes)
<!-- nexlayer:end -->

## Local Development Setup
<!-- nexlayer:section user-editable=local_setup -->
### Prerequisites

- Node.js >= 20.18.1
- npm
- Python 3.x

### Environment variables

Copy `.env.example` to `.env.local` and fill in:

```
CPU_CORES=2
```

### Steps

1. `npm install` — Install Node.js dependencies
2. `pip install -r requirements.txt` — Install Python helper dependencies
3. `npm start -- --gui` — Launch the application on http://localhost:9005

<!-- nexlayer:end -->

## Nexlayer Deployment Plan
<!-- nexlayer:section user-editable=deployment_plan -->
### Pod Topology

| Pod | Image | Port | Role |
|-----|-------|------|------|
| social-analyzer | mirror.gcr.io/library/node:18-alpine | 9005 | web |
| selenium-hub | mirror.gcr.io/library/selenium/hub:latest | 4444 | master |
| selenium-firefox | mirror.gcr.io/library/selenium/node-firefox:latest | 5900 | worker |

### Inter-pod environment variables

- `selenium-firefox` pod: `SE_EVENT_BUS_HOST=${selenium-hub:4442}`

### Deployment notes

- Application refers to the Selenium Grid via ${selenium-hub:4444}
- Firefox node connects to the hub using ${selenium-hub:4442} for event bus communication
- Standard official mirrors are used to avoid Docker Hub namespaced image failures

<!-- nexlayer:end -->

## Build Notes
<!-- nexlayer:section user-editable=build_notes -->
<!-- Add notes for future builds here — preserved across re-analysis -->
<!-- nexlayer:end -->

## Nexlayer Configuration
<!-- nexlayer:section agent-managed=nexlayer_config -->
**Last deployed:** 2026-06-05T19:15:56Z  
**Live URL:** https://kitbear-studio-slim-reef-social-analyzer.cloud.nexlayer.ai  
**Runtime:** node · **Port:** 3000  
**Deploy branch:** main  

```yaml
application:
  name: slim-reef-social-analyzer
  pods:
    - name: app
      image: "# filled by pipeline"
      path: /
      servicePorts:
        - 9005
      vars:
        - key: NODE_ENV
          value: production
        - key: PORT
          value: "9005"
        - key: HOSTNAME
          value: "0.0.0.0"
```
<!-- nexlayer:end -->

## Build History
<!-- nexlayer:section agent-managed=build_history -->
| Date | Status | Notes |
|------|--------|-------|
| 2026-06-05T19:10:36Z | analyzed | initial repo analysis |
| 2026-06-05T19:15:56Z | success | deployed https://kitbear-studio-slim-reef-social-analyzer.cloud.nexlayer.ai |
<!-- nexlayer:end -->
