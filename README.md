# 🛡️ Sentinel — AI-Driven SRE Context Engine

> A lightweight, context-aware diagnostic CLI and daemon designed to collect local server telemetry, inspect project workspaces, and deliver instant SRE root-cause analysis via LLMs.

![Go Version](https://img.shields.io/badge/go-1.22+-00ADD8?style=flat&logo=go)
![Docker](https://img.shields.io/badge/docker-hardened-2496ED?style=flat&logo=docker)
![Architecture](https://img.shields.io/badge/architecture-hybrid_CLI%2FDaemon-orange)
---

## 📸 Demo

![Sentinel CLI Demo](docs/assets/sentinel-demo.gif)

---

## 📌 Overview

**Sentinel** is an infrastructure **Context Engine** built in Go. Rather than acting as a generic AI chatbot, Sentinel inspects host telemetry, process logs, and workspace source files locally, assembling a structured context payload to deliver hyper-condensed, actionable diagnostic steps via the Gemini API.

---

## 🏗️ Architecture

Sentinel uses a **hybrid architecture**: a fast, zero-dependency native CLI that interacts with a containerized background Daemon over local UNIX domain sockets.

```mermaid
graph LR
    User[Terminal User] -->|sentinel explain| CLI[Native Go CLI]
    CLI -->|Scans Local Path| Files[Workspace Files / Scripts]
    CLI -->|IPC / UNIX Socket| Daemon[Sentinel Daemon Container]
    Daemon -->|Structured Context + Tool Calling| Gemini[Gemini API]
    Daemon -->|Exposes Health & Metrics| Prom[Prometheus / Grafana]
