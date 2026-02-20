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

### 7.1 What OAPverse Is

**OAPverse** is the open, community-driven platform at the heart of the OAP ecosystem. It is the place where agents live, are discovered, built, shared, forked, improved, and executed — by anyone, from anywhere, on any OAP-compatible runtime.

If OAP is the protocol, OAPverse is the internet that runs on top of it.

The closest analogies are GitHub for source code, Docker Hub for containers, and the npm registry for packages — but OAPverse goes further than any of them, because agents are not just artifacts to distribute: they are living, executable, composable entities that can be launched directly from the platform into any connected runtime.

> OAPverse is not mandatory for OAP. But it is designed to become the gravitational center of the entire agent ecosystem.

---

### 7.2 The Core Problem OAPverse Solves

Today, great AI agents are trapped. A developer builds a brilliant research agent, a nuanced legal summarizer, or a perfectly tuned code reviewer — and it lives in a private ChatGPT workspace, inaccessible, non-forkable, non-improvable by anyone else. There is no App Store for agents that is open. There is no GitHub for agents that is standardized. There is no npm for agents that is portable.

OAPverse is the answer to that gap. It gives agents a home that is:
- **Open**: no vendor lock-in, no platform gatekeeping
- **Universal**: any agent published on OAPverse can run on any OAP-compatible runtime
- **Collaborative**: the community can read, fork, improve, and merge agents freely
- **Executable**: agents are not just stored, they are launchable directly from the platform

---

### 7.3 Agent Discovery: Finding the Right Agent

OAPverse provides a rich, multi-dimensional discovery experience designed to surface the right agent for any task.

#### Search and Filtering

Users can search agents by natural language query ("I need an agent that summarizes legal contracts in plain English"), or filter by structured attributes:

| Filter | Examples |
|--------|---------|
| **Category** | Productivity, Research, Development, Writing, Finance, Legal, Healthcare... |
| **Capabilities** | `web-search`, `code-execution`, `file-analysis`, `image-generation`... |
| **Compatible Runtimes** | Claude, OpenAI, Ollama, LangGraph... |
| **Required Permissions** | Agents with no network access, agents that don't touch the filesystem... |
| **LLM Agnostic** | Agents tested on multiple models vs optimized for one |
| **Persona Scopes** | What user context does the agent request? |
| **Trust Level** | Community, Verified, Official |
| **License** | MIT, Apache 2.0, CC-BY, Commercial... |

#### Agent Cards

Every agent has a rich public profile ("Agent Card") displaying:

- Name, description, version, author
- Live usage stats (runs, active users, weekly growth)
- Community ratings and reviews
- Capability badges
- Permission transparency panel ("This agent requests access to: network, `profile.work.projects`")
- Compatibility matrix (which runtimes it has been tested on)
- Changelog and version history
- Fork tree (visual graph of forks and lineage)
- Related agents ("Users who use this also use...")

#### Curated Collections

Beyond search, OAPverse surfaces agents through editorially curated collections:

- **Trending This Week** — agents gaining momentum
- **Staff Picks** — community council highlights
- **Starter Packs** — curated bundles for specific use cases (e.g., "The Developer Toolkit", "The Researcher Bundle")
- **New & Noteworthy** — freshly published agents worth watching
- **Most Forked** — agents the community is actively building on top of

---

### 7.4 Agent Publishing: From Manifest to the World

Any user can publish an agent to OAPverse. The publishing workflow is designed to be as frictionless as possible while maintaining quality standards.

#### Publishing Flow

```
1. Write your oap.yaml manifest (locally or in the web editor)
2. Run: oap publish
   → Validates manifest schema
   → Runs automated security scan
   → Checks permission declarations are complete
   → Generates agent card preview
3. Add metadata: description, tags, category, screenshots/demos
4. Choose visibility: Public / Unlisted / Private / Organization
5. Choose license
6. Publish → agent is live and immediately accessible via OAP from any connected runtime
```

#### Versioning

All agents are versioned with strict semantic versioning (`MAJOR.MINOR.PATCH`). OAPverse enforces:

- Immutable published versions (a published version cannot be silently overwritten)
- A clear deprecation workflow for old versions
- Automatic notification to users of an agent when a new version is published
- A `latest` tag that always resolves to the most recent stable version

#### The `oap` CLI

Publishing and consuming agents from OAPverse is possible via the `oap` command-line tool:

```bash
# Search for agents
oap search "legal document summarizer"

# Install an agent locally
oap install oapverse/legal-summarizer@2.1.0

# Run an agent directly
oap run oapverse/research-analyst --runtime ollama

# Publish your agent
oap publish ./my-agent/oap.yaml

# Fork an agent
oap fork oapverse/research-analyst my-custom-analyst
```

---

### 7.5 Collaboration: The GitHub Model for Agents

OAPverse adopts a collaboration model inspired by GitHub, adapted for the unique properties of agents.

#### Forking

Any public agent can be forked in one click. A fork creates an independent copy under your namespace while preserving the full lineage history. The fork tree is publicly visible, allowing the community to understand how an agent has evolved and branched over time.

Forks are first-class citizens: they have their own Agent Card, their own version history, their own community. A fork can diverge entirely from its parent or stay closely aligned and regularly merge upstream changes.

#### Pull Requests (Agent PRs)

If you improve a fork, you can submit a **Pull Request** back to the parent agent. The agent's maintainer reviews the proposed changes to the manifest, the instructions, the tool definitions, or the permission model. PRs can be:

- Discussed inline (line-by-line comments on the manifest)
- Tested by the maintainer before merging
- Automatically run through the OAPverse CI pipeline (validation, security scan, regression tests)
- Merged, rejected, or kept open for iteration

#### Issues and Discussions

Every agent has an issue tracker and a discussion board. Users can report unexpected behaviors, propose improvements, ask questions, and engage with maintainers and the broader community. Issues can be tagged as `bug`, `enhancement`, `question`, `security`, `breaking-change`.

#### Agent Merge

Beyond simple forking, OAPverse provides an experimental **Agent Merge** tooling: a workflow to intelligently combine two compatible agents into a new composite agent. The merge tool diffs the two manifests, identifies conflicts (overlapping tool definitions, permission clashes, contradictory instructions), and surfaces them for the user to resolve. The result is a new, versioned agent combining the capabilities of both parents.

---

### 7.6 The Trust and Verification System

Because agents can request permissions and execute actions, trust is a critical concern. OAPverse implements a layered trust model.

#### Trust Levels

| Level | Badge | Criteria |
|-------|-------|---------|
| **Community** | 🟡 | Published by any user, not externally reviewed |
| **Verified Creator** | 🔵 | Author identity verified, consistent publishing history, no security flags |
| **Audited** | 🟢 | Agent has undergone a community security audit, all permissions reviewed |
| **Official** | ⚪ | Published by the OAP core team or a recognized institutional partner |

#### Cryptographic Signatures

Every published agent manifest is cryptographically signed by its author. Users and runtimes can verify the signature before loading an agent, ensuring:

- The agent has not been tampered with since publication
- The author's identity is tied to the manifest
- Version integrity is mathematically verifiable

#### Automated Security Scanning

On every publish and every update, OAPverse runs automated scans checking:

- Declared permissions match actual tool usage in the manifest
- No known prompt injection patterns in the instructions
- No attempt to request undeclared scopes
- No obfuscated or encoded instruction payloads

Agents that fail security scans are flagged or blocked from publication until resolved.

#### Community Flagging

Any user can flag an agent for review. Flags are triaged by the OAPverse Safety Council (a community-elected body). Flagged agents display a warning banner until the review is complete. Agents confirmed as malicious or deceptive are removed and their authors face account suspension.

---

### 7.7 Launching Agents Across Connected Runtimes

This is where OAPverse goes beyond any existing registry: **agents are not just stored, they are executable from within the platform, on any connected OAP runtime.**

#### One-Click Launch

From any Agent Card, a user can click **"Run this Agent"** and immediately select their preferred runtime:

```
Run "research-analyst v2.1.0" on:
  ● Claude (connected)
  ● Ollama – llama3 (connected)
  ○ OpenAI GPT-4o (not connected — add runtime)
  ○ Local custom runtime (configure)

[ Launch ]
```

The agent manifest is fetched from OAPverse, validated, and injected into the selected runtime via the OAP Runtime Interface. The user's Persona (if consented) is loaded. The session begins immediately.

#### Runtime Connections

Users connect their runtimes to OAPverse once, via API keys or OAuth. Connected runtimes appear in the launcher for every agent. This means a user can discover an agent on OAPverse and run it on their local Ollama instance, their Claude account, or their company's private LLM deployment — without any copy-paste or manual configuration.

#### In-Browser Sandbox

For quick testing without connecting a runtime, OAPverse offers a **sandboxed in-browser execution environment** powered by a lightweight OAP runtime. This sandbox is intentionally limited (no network access, no filesystem, no persona injection by default) but allows users to test an agent's behavior, instructions, and personality before committing to a full deployment.

#### Runtime-Specific Previews

Agent Cards display compatibility information per runtime: community-submitted test results indicating whether an agent works well on a given LLM, along with notes on behavioral differences across models ("This agent performs significantly better on Claude than on GPT-3.5 for multi-step reasoning tasks").

---

### 7.8 Organizations and Teams

OAPverse supports organizational accounts for companies, open-source projects, and communities.

#### Organization Features

- **Private namespaces**: agents published under `org/agent-name` are accessible only to organization members, unless explicitly made public
- **Role-based access control**: Owner, Maintainer, Contributor, Viewer roles per agent or per organization
- **Internal registries**: organizations can self-host a private OAPverse mirror that syncs with the public registry while keeping proprietary agents internal
- **Audit logs**: every action on an organization's agents is logged (publishes, forks, permission changes, API key usage)
- **SSO integration**: organizations can enforce Single Sign-On for all members

#### The Company Use Case

A company can maintain a curated internal library of agents — customer support agent, internal knowledge base agent, HR onboarding agent — all versioned, audited, and accessible to employees on their preferred runtime (Claude, Copilot, internal LLM), without any agent ever leaving the company's private OAPverse mirror.

---

### 7.9 The Ecosystem Layer: Collections, Bundles, and Pipelines

Beyond individual agents, OAPverse supports higher-order compositions.

#### Collections

A Collection is a curated list of agents grouped around a theme or workflow, maintained by a user or organization. Collections can be:

- Public (browsable by anyone)
- Followed (users receive updates when agents in the collection are updated)
- Forked (the entire collection, including its curation logic, can be forked)

Example collections: *"The Full-Stack Developer Toolkit"*, *"Academic Research Suite"*, *"Customer Support Stack"*, *"Content Creation Pipeline"*.

#### Bundles

A Bundle is an installable package of multiple agents designed to work together. Installing a Bundle adds all constituent agents to your local OAP environment in one command:

```bash
oap install-bundle oapverse/bundles/developer-toolkit
# Installs: code-reviewer, test-writer, docs-generator, pr-summarizer
```

#### Pipelines (v0.3+)

A longer-term feature planned for OAPverse is **visual pipeline building**: a UI where users can chain agents together — Agent A's output becomes Agent B's input — and publish the resulting pipeline as a new composite agent. This effectively turns OAPverse into a no-code agent orchestration layer on top of OAP.

---

### 7.10 The OAPverse API

Every feature of OAPverse is accessible via a public REST and GraphQL API, enabling developers to integrate OAPverse into their own tools, IDEs, and platforms.

```http
# Fetch agent manifest
GET /api/v1/agents/{namespace}/{name}@{version}

# Search agents
GET /api/v1/agents/search?q=legal+summarizer&capabilities=web-search

# Get agent versions
GET /api/v1/agents/{namespace}/{name}/versions

# Launch agent on a connected runtime (authenticated)
POST /api/v1/agents/{namespace}/{name}/launch
{
  "runtime": "anthropic-claude",
  "persona_scope": ["profile.basic", "profile.work"]
}
```

This API is what powers the **OAP-to-MCP Bridge**: an MCP server that exposes OAPverse to proprietary platforms like Claude and ChatGPT, allowing users to browse and launch OAPverse agents from within those platforms natively — even if the platform has not implemented a full OAP adapter.

---

### 7.11 Decentralization and Mirrors

OAPverse is designed to be **decentralized by architecture**. The public OAPverse instance is the canonical community registry, but it is not the only possible registry.

Anyone can run an OAPverse mirror or a private OAPverse instance. All OAP tooling (`oap` CLI, runtime adapters) supports pointing to alternative registries:

```yaml
# ~/.oap/config.yaml
registries:
  - name: public
    url: https://registry.oapverse.dev
    default: true
  - name: company
    url: https://agents.internal.mycompany.com
    auth: token
```

Agents can be cross-published across registries. The public OAPverse instance federates with verified community mirrors to improve resilience and geographic distribution.

This means **no single point of failure**, and **no single point of control** — consistent with OAP's founding principle that the ecosystem must not be owned by any one party.

---

### 7.12 Governance of OAPverse

OAPverse is governed by the **OAP Community Council**, a body of elected community representatives. The Council is responsible for:

- Curating the Trust and Verification standards
- Electing the Safety Council
- Approving changes to OAPverse's core policies
- Managing the public OAPverse infrastructure budget (funded by optional sponsorships and organizational tier subscriptions)
- Arbitrating disputes between users and organizations

The Council operates transparently: all decisions are published, all votes are recorded, all meeting notes are public. The governance model is explicitly designed to prevent any single company — including the original OAP authors — from gaining disproportionate influence over the registry.

> OAPverse belongs to the community. Its governance model is designed to keep it that way permanently.

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
