# Open Agentic Protocol (OAP)
**A Universal Standard for Portable, Interoperable AI Agents**

*White Paper – Draft v0.1*

[![Status: Draft](https://img.shields.io/badge/Status-Draft_v0.1-orange.svg)]()
[![Contributions: Welcome](https://img.shields.io/badge/Contributions-Welcome_RFCs-brightgreen.svg)]()

---

## Abstract

The rapid evolution of AI agents has created a fragmented ecosystem. Today, agents are platform-bound, non-portable, inconsistently versioned, and lack standardized security models. Each vendor and framework defines its own format, runtime assumptions, and execution model.

The **Open Agentic Protocol (OAP)** proposes a universal, open, model-agnostic standard for defining, packaging, distributing, and executing AI agents across platforms.

OAP introduces:
- A standardized agent manifest
- A runtime interoperability contract
- A permission-based security model
- Multi-agent communication standards
- Portable user context profiles ("Persona Agents")
- A community-driven registry called **OAPverse**

OAP aims to become for AI agents what OpenAPI became for APIs and Docker for containers: a neutral, open infrastructure layer for the next generation of intelligent systems.

---

## Table of Contents

1. [The Problem](#1-the-problem)
2. [Vision](#2-vision)
3. [Core Architecture](#3-core-architecture)
4. [OAP Core Specification](#4-oap-core-specification)
5. [OAP Runtime Interface](#5-oap-runtime-interface)
6. [OAP Messaging Layer](#6-oap-messaging-layer)
7. [OAPverse](#7-oapverse)
8. [Persona Agents](#8-persona-agents-portable-user-context)
9. [Security Model](#9-security-model)
10. [Governance](#10-governance)
11. [Design Principles](#11-design-principles)
12. [Non-Goals](#12-non-goals)
13. [Long-Term Impact](#13-long-term-impact)
14. [Open Challenges (v0.1)](#14-open-challenges-and-unresolved-core-areas-v01)
15. [Roadmap](#15-roadmap-proposed)
16. [Get Involved](#-get-involved-request-for-comments)

---

## 1. The Problem

### 1.1 Fragmentation

Today, AI agents are:
- Locked into specific platforms (ChatGPT GPTs, Claude Projects, Copilot Agents)
- Tied to proprietary execution environments
- Incompatible across LLM providers
- Not easily versioned or shared
- Difficult to compose or merge
- Lacking standardized security models

An agent created in one ecosystem cannot easily be executed in another. There is no portable, open standard for agents.

### 1.2 No Universal Contract

There is currently no:
- Standard manifest format
- Standard permission declaration model
- Standard runtime interface
- Standard packaging system
- Standard multi-agent messaging format
- Standard identity and user-context portability model

As a result, the ecosystem remains siloed and non-interoperable.

---

## 2. Vision

OAP envisions a world where:
- Agents are **portable**
- Agents are **versioned** with semantic versioning
- Agents are **interoperable** across runtimes
- Agents **declare permissions** explicitly
- Agents can **communicate** with each other
- Users **own** their contextual identity layer
- The ecosystem is **open**, not vendor-controlled

> **OAP is not a platform. It is a standard.**

---

## 3. Core Architecture

OAP consists of four foundational layers:

| Layer | Description |
|-------|-------------|
| **OAP Core Specification** | Standardized agent manifest format |
| **OAP Runtime Interface** | Interoperability contract for runtimes |
| **OAP Messaging Layer** | Multi-agent communication standard |
| **OAPverse** | Community registry layer |

---

## 4. OAP Core Specification

OAP defines a standardized agent manifest. An OAP agent is described declaratively.

*Example conceptual manifest (`oap.yaml`):*

```yaml
name: research-analyst
version: 1.2.0
description: Multi-source research agent

instructions: |
  You are a structured research analyst.

capabilities:
  - reasoning
  - web-search
  - summarization

tools:
  - type: mcp
    name: brave-search
  - type: openapi
    spec: ./jira-api.yaml

permissions:
  network: true
  filesystem: false
  persona:
    - profile.basic
    - profile.work.projects

compatibility:
  runtimes:
    - openai
    - anthropic
    - local-ollama
```

OAP does **not** define:
- A specific LLM
- A specific orchestration method
- A specific execution engine

It defines only the **contract** between an agent and a runtime.

---

## 5. OAP Runtime Interface

Any platform may implement an **OAP Adapter**. Examples include ChatGPT, Claude, Windsurf, Ollama, LangGraph, and custom servers.

An OAP-compatible runtime must:
- Load and validate OAP manifests
- Enforce declared permissions
- Execute tool calls
- Handle agent messaging
- Inject persona context safely
- Return structured outputs

> OAP does not replace runtimes. It standardizes their entry point.

---

## 6. OAP Messaging Layer

To enable multi-agent collaboration, OAP defines a standard communication format: **OAP-MSG**.

It defines:
- Agent identity
- Message type
- Scope
- Context boundaries
- Authorization constraints
- Structured payload format

This allows:
- Agent A to call Agent B
- Debate-style collaboration
- Agent merging
- Controlled context propagation
- Runtime-agnostic orchestration

---

## 7. OAPverse

**OAPverse** is the open community registry for OAP agents. It functions similarly to Docker Hub, GitHub, or the npm registry.

OAPverse enables:
- Publishing public or private agents
- Versioning via semver
- Forking, pull requests, code reviews
- Issues and discussions
- Stars and reputation
- Agent merge tooling
- Cryptographic signatures & Trust badges
- Mirrors for decentralization

> Note: OAPverse is not mandatory for OAP. It is the primary community distribution layer.

---

## 8. Persona Agents (Portable User Context)

### 8.1 The Problem It Solves

Today, every AI platform starts from scratch. You explain to ChatGPT that you are a backend developer, that you work in TypeScript, that you prefer concise answers. Then you do the same with Claude. Then with Copilot. Then with the next tool that ships six months from now.

This is not just UX friction. It is a fundamental asymmetry: platforms accumulate knowledge about you, but you own nothing. You are a tenant of your own context.

The Persona Agent reverses that dynamic.

### 8.2 Definition

A Persona Agent is a standard OAP agent whose *subject* is the user themselves. It is a portable, encrypted, user-controlled file that encapsulates:

- **Professional identity** (role, tech stack, domain, active projects)
- **Communication preferences** (level of detail, language, expected tone)
- **Organizational context** (team, tools in use, constraints)
- **Accumulated memory** (past decisions, learned preferences, long-term context)
- **Multiple personas** (Work, Personal, Research, Creative...)

Structurally, a Persona Agent looks like this:

```yaml
persona:
  id: user-uuid-xxxx
  version: 1.0.4
  created: 2024-01-15
  last_updated: 2025-06-10

  scopes:
    profile.basic:
      name: "Alice"
      language: "en"
      communication_style: "concise, direct, technical"

    profile.work:
      role: "Lead Backend Engineer"
      stack: ["TypeScript", "Go", "PostgreSQL", "Kubernetes"]
      team: "Platform Team"
      current_projects:
        - name: "API Gateway v2"
          status: "in_progress"
          context: "Migration from monolith, deadline Q3"

    profile.work.preferences:
      code_style: "functional over OOP when possible"
      review_tone: "direct, no sugarcoating"
      doc_format: "ADR-style for architectural decisions"

    profile.personal:
      # Encrypted separately, inaccessible to the work scope
      ...

  memory:
    decisions:
      - date: 2025-03-10
        context: "API Gateway"
        decision: "Chose tRPC over REST for internal services"
        rationale: "Type safety end-to-end, team already on TypeScript"
    learned_preferences:
      - "Prefers code examples before theoretical explanations"
      - "Dislikes responses that start by restating the question"
```

### 8.3 The Scope-Based Permission Model

An agent that wants to access the Persona must explicitly declare the scopes it requires:

```yaml
permissions:
  persona:
    - profile.basic
    - profile.work.projects
```

It cannot access `profile.personal`, `profile.work.stack`, or accumulated memory without explicitly requesting them. The user sees exactly what is being requested before granting access — just like a mobile app permission prompt.

This model enables fine-grained control:

| Scope | Contents | Typical Use Case |
|-------|----------|-----------------|
| `profile.basic` | Name, language, tone | Almost all agents |
| `profile.work` | Role, team, tools | Professional agents |
| `profile.work.projects` | Active projects and context | Productivity agents |
| `profile.work.preferences` | Code style, review preferences | Development agents |
| `profile.personal` | Personal context | Lifestyle / wellness agents |
| `memory.decisions` | Historical decision log | Long-term advisory agents |
| `memory.learned` | Learned preferences | Conversational agents |

### 8.4 Portability and Storage

The Persona Agent is **local-first** by design. It lives on the user's device, not on a third-party server. Supported storage options:

- **Encrypted local file** (`.oap/persona.enc`) — desktop / CLI use case
- **End-to-end encrypted sync** via a user-chosen service (iCloud, personal S3, Nextcloud...)
- **Manual export/import** for device migration

What OAP does **not** do: host Persona Agents. It defines the format. Storage remains under the user's control.

### 8.5 A Persona That Evolves Over Time

One underexplored aspect of v0.1 is the Persona's capacity to **learn and evolve**. After each session, an OAP-compatible runtime may propose updates to the Persona:

```
Session complete. The agent learned the following:
  → You prefer responses with fewer than 5 bullet points
  → You now use Bun instead of Node for new projects

Would you like to update your Persona? [Accept all] [Choose] [Ignore]
```

The user remains in full control of what enters their Persona. There is no silent learning.

### 8.6 Multiple Personas and Isolation

A user can maintain multiple, cryptographically isolated Persona Agents:

```
~/.oap/personas/
  work.persona.enc        ← Tech stack, projects, team
  personal.persona.enc    ← Lifestyle preferences, personal projects
  research.persona.enc    ← Areas of study, active bibliography
  creative.persona.enc    ← Writing style, creative projects
```

These personas are **cryptographically isolated**. An agent loading `work.persona` cannot infer the contents of `personal.persona`. Isolation is guaranteed at the format level, not merely by convention.

### 8.7 The Persona as an AI Identity Layer

In the longer term, the Persona Agent becomes something more fundamental: **the user's identity layer within the AI ecosystem**. Not a profile stored at a vendor. Not an account on a platform. A file you own, carry with you, and selectively reveal depending on context — exactly as you naturally adapt what you share depending on whether you are speaking with a colleague, a doctor, or a friend.

This is likely OAP's most original contribution relative to everything that exists today.

### 8.8 Open Questions for RFCs

Several questions remain open for community discussion:

- How should merge conflicts be handled when a Persona is updated from two devices simultaneously?
- Should a cryptographic signature format be defined to certify that a Persona has not been tampered with?
- How should a "stale" Persona (containing outdated information) signal its freshness level to consuming agents?

---

## 9. Security Model

OAP is **security-first**. Agents must declare:
- Network access
- Filesystem access
- API access
- Required secrets
- Persona scopes

The runtime enforces permissions. Agents cannot silently escalate privileges. This model resembles OAuth scopes, mobile app permissions, and container isolation.

---

## 10. Governance

OAP is:
- Open source
- RFC-driven
- Vendor-neutral
- Community governed

The goal is not to build a SaaS platform. The goal is to establish an **infrastructure standard**.

---

## 11. Design Principles

| Principle | Description |
|-----------|-------------|
| Security by default | Permissions must be explicitly declared |
| Declarative over imperative | Manifests define intent, not execution |
| Model-agnostic | Works with any LLM |
| Runtime-agnostic | Works with any execution environment |
| Minimal core, extensible layers | Small, focused spec with optional extensions |
| Open governance | Community-driven, vendor-neutral |
| Portability-first | Agents belong to users, not platforms |

---

## 12. Non-Goals

OAP does **not** aim to:
- Replace LLM providers
- Replace agent frameworks
- Enforce a specific orchestration architecture
- Become a proprietary ecosystem
- Compete with vendors

> OAP standardizes the **interface layer**.

---

## 13. Long-Term Impact

If adopted, OAP enables:
- True agent portability
- Cross-platform agent ecosystems
- Secure multi-agent collaboration
- User-owned AI identity layers
- Marketplace-neutral distribution
- A composable agent internet

OAP could become:
- **The OpenAPI** of AI agents
- **The Docker** of cognitive systems
- **The npm** of intelligent modules

---

## 14. Open Challenges and Unresolved Core Areas (v0.1)

While OAP defines a robust execution and identity standard, several architectural challenges remain open for community RFCs.

### 14.1 State and Memory Portability

While the Persona Agent handles user context, the long-term memory of the agent itself remains a challenge.

- **The Vector Problem:** Agents rely heavily on vector databases and knowledge graphs. A truly portable agent must define a standard export/import format for its embedded memory (e.g., standardizing around Parquet or a universal SQLite-vss schema).
- **Thread History:** How are active conversation threads and intermediate reasoning states packaged and migrated without losing the agent's current train of thought?

> OAP v0.2 will need to address a standardized **State Manifest** alongside the Agent Manifest.

### 14.2 The Adoption Dilemma (Walled Gardens)

Incumbent AI platforms are building proprietary ecosystems to retain users and lack commercial incentives to adopt a standard that allows easy migration. OAP therefore assumes a **bottom-up** adoption strategy:

- **Open-Source First:** Initial adoption targets open-source and developer-first ecosystems: Ollama, HuggingFace, Vercel AI SDK, LangChain, and local-first AI IDEs.
- **The MCP Bridge:** OAP will provide a **Model Context Protocol (MCP) Server** to bridge the gap with proprietary platforms — exposing the OAPverse registry and OAP runtime via MCP so any proprietary client can seamlessly pull and interact with OAP agents natively.

---

## 15. Roadmap (Proposed)

### Phase 1 — Foundation & Open Source Adoption
- [ ] OAP Core Spec v0.1 & Manifest definition
- [ ] Minimal runtime adapter for local ecosystems (Ollama / Vercel AI SDK)
- [ ] Local registry prototype
- [ ] OAP-to-MCP Bridge: MCP server to expose OAP agents to proprietary platforms

### Phase 2 — Registry & Memory (State)
- [ ] OAPverse public beta (Community registry)
- [ ] OAP Messaging Layer definition
- [ ] RFC on Agent State & Memory portability (Vector DB agnostic migrations)

### Phase 3 — Identity & Ecosystem
- [ ] Persona Agent model & Permission enforcement
- [ ] Community governance setup
- [ ] Security audit

---

## Conclusion

The AI agent ecosystem is currently fragmented and platform-bound. OAP proposes a minimal but powerful standard to enable **portability**, **interoperability**, **composability**, and **security**.

The future of AI agents should not be siloed. It should be open.

**The Open Agentic Protocol is an invitation to build that future together.**

---

## 🤝 Get Involved (Request for Comments)

This repository is currently in the **Draft / RFC phase**. We are actively looking for feedback, critiques, and contributions from the community.

- 📋 Read the open **Issues** to join the discussion
- 🔀 Submit a **PR** to propose changes to the v0.1 specification
- 💬 Start a **Discussion** about State Memory or the MCP Bridge implementation
