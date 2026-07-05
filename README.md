# Awesome Agent Infra

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

> A curated collection of infrastructure resources for building production AI agents: runtimes, workspaces, sandboxes, tool protocols, context systems, security, observability, and evaluation.

This list focuses on the **systems layer below agent products and above foundation models**.

It is not a general "awesome AI agents" list. It is focused on the infrastructure needed to run agents safely and reliably in production.

## Contents

- [Scope](#scope)
- [Core Concepts](#core-concepts)
- [Foundational Articles](#foundational-articles)
- [Runtime and Control Plane](#runtime-and-control-plane)
- [Tool Protocols and Context Interfaces](#tool-protocols-and-context-interfaces)
- [Workspace and Runtime State](#workspace-and-runtime-state)
- [Sandbox and Execution](#sandbox-and-execution)
- [Security, Policy, and Governance](#security-policy-and-governance)
- [Observability and Evaluation](#observability-and-evaluation)
- [Coding-Agent Workflows](#coding-agent-workflows)
- [Data Layer and Storage](#data-layer-and-storage)
- [Books](#books)
- [Videos and Talks](#videos-and-talks)
- [Related Awesome Lists](#related-awesome-lists)
- [Patterns](#patterns)
- [Contributing](#contributing)
- [License](#license)

## Scope

Included:

- Agent runtimes and control planes
- Durable execution
- Workspace and runtime state
- Sandbox and execution environments
- Tool protocols such as MCP
- Context files and repo-level guidance
- Security, permissions, and policy
- Observability, tracing, and evaluation
- Coding-agent workflows
- Relevant systems books and videos

Not included:

- Prompt collections
- General AI app directories
- Chatbot UI tools
- Generic RAG tools unless they are directly relevant to agent infrastructure
- End-user agent products without clear infrastructure lessons

## Core Concepts

| Concept | Meaning |
|---|---|
| **Agent runtime** | The execution layer that runs agent loops, manages state, retries, tools, and human interaction. |
| **Harness** | The model-facing loop and scaffolding that turns model outputs into actions. |
| **Workspace** | The durable working state an agent reads and writes during a task. Not just a folder. |
| **Sandbox** | The isolated compute environment where actions execute. |
| **Session / run** | The ordered record of an agent execution attempt. |
| **Tool protocol** | The interface by which agents discover and call external tools or resources. |
| **Policy** | Runtime constraints over tools, data, paths, permissions, and publish actions. |
| **Publish lifecycle** | The process of promoting candidate agent output into source-of-truth systems. |
| **Observability** | Traces, logs, metrics, costs, evals, and replay data for agent behavior. |

## Foundational Articles

| Resource | Layer | Why it matters |
|---|---|---|
| [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) | Runtime | Practical guide arguing for simple composable agent patterns instead of over-engineered abstractions. |
| [Anthropic: Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Context / Runtime | Good framing for context as runtime design rather than prompt stuffing. |
| [Anthropic: Writing Effective Tools for AI Agents](https://www.anthropic.com/engineering/writing-tools-for-agents) | Tooling | Useful for designing tool APIs agents can actually use. |
| [Martin Fowler: Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) | Coding agents / Context | Strong developer-facing explanation of workspace files and repo context for coding agents. |
| [Temporal: What Is Durable Execution?](https://temporal.io/blog/what-is-durable-execution) | Durable execution | Core concept for long-running, crash-resilient workflows. |
| [DBOS: Durable Execution for Crashproof AI Agents](https://www.dbos.dev/blog/durable-execution-crashproof-ai-agents) | Durable execution | Applies durable execution ideas directly to AI agents. |
| [GitHub Blog: A practical guide on how to use the GitHub MCP server](https://github.blog/ai-and-ml/generative-ai/a-practical-guide-on-how-to-use-the-github-mcp-server/) | Tool protocol / GitHub workflow | Practical reference for MCP + GitHub integration. |

## Runtime and Control Plane

### Projects

| Project | Type | Why it matters |
|---|---|---|
| [LangGraph](https://github.com/langchain-ai/langgraph) | Runtime framework | Stateful graph runtime for long-running agents, persistence, human-in-the-loop, and durable execution. |
| [LangGraph docs](https://docs.langchain.com/oss/python/langgraph/overview) | Docs | Good reference for durable agent orchestration concepts. |
| [OpenAI Agents SDK Python](https://github.com/openai/openai-agents-python) | SDK | Lightweight SDK for building agentic apps. Useful baseline for minimal abstractions. |
| [OpenAI Agents SDK TypeScript](https://openai.github.io/openai-agents-js/) | SDK | TypeScript version, useful for JS/TS infrastructure builders. |
| [OpenHands](https://github.com/OpenHands/OpenHands) | Agent platform | Full open-source software-agent platform with sandboxed execution and developer workflows. |
| [OpenHands Software Agent SDK](https://github.com/OpenHands/software-agent-sdk) | SDK | Composable SDK for building software-development agents. |
| [SWE-agent](https://github.com/swe-agent/swe-agent) | Coding-agent scaffold | Simple and influential coding-agent scaffold for GitHub issue solving. |
| [mini-SWE-agent](https://github.com/swe-agent/mini-swe-agent) | Minimal agent | Small baseline for understanding the minimal loop needed to solve coding tasks. |
| [Goose](https://github.com/aaif-goose/goose) | Local agent runtime | General-purpose open-source agent with CLI, desktop, API, and MCP extension ecosystem. |
| [Semantic Kernel](https://github.com/microsoft/semantic-kernel) | Enterprise SDK | Enterprise-oriented orchestration and agent framework from Microsoft. |
| [CrewAI](https://github.com/crewAIInc/crewAI) | Multi-agent framework | Popular multi-agent orchestration framework. |
| [AutoGen](https://github.com/microsoft/autogen) | Multi-agent framework | Influential multi-agent framework. Useful historically and architecturally. |
| [Letta](https://github.com/letta-ai/letta) | Stateful agents / memory | Platform for stateful agents with advanced memory. Useful for understanding memory-first agent design. |
| [Letta Code](https://github.com/letta-ai/letta-code) | Coding agent / memory | Memory-first coding agent. Useful contrast with workspace-first designs. |

### Papers

| Paper | Why it matters |
|---|---|
| [Infrastructure for AI Agents](https://arxiv.org/abs/2501.10114) | Defines agent infrastructure as external technical systems and protocols that mediate agent interaction. |
| [AI Runtime Infrastructure](https://arxiv.org/abs/2603.00495) | Proposes runtime infrastructure between model and application. Useful for control-plane framing. |
| [OpenHands: An Open Platform for AI Software Developers as Generalist Agents](https://arxiv.org/abs/2407.16741) | Important system paper for software agents. |
| [The OpenHands Software Agent SDK](https://arxiv.org/abs/2511.03690) | Architecture of a composable SDK for production software agents. |
| [Agents Learn Their Runtime](https://arxiv.org/abs/2603.01209) | Shows that runtime persistence semantics affect agent behavior. |

## Tool Protocols and Context Interfaces

### MCP

| Resource | Type | Why it matters |
|---|---|---|
| [Model Context Protocol official docs](https://modelcontextprotocol.io/docs/getting-started/intro) | Docs | Main entry point for MCP. |
| [MCP specification](https://modelcontextprotocol.io/specification/draft) | Spec | Protocol details. |
| [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk) | SDK | Official TypeScript SDK. |
| [MCP servers repository](https://github.com/modelcontextprotocol/servers) | Repo | Reference and community MCP server directory. |
| [GitHub MCP Server](https://github.com/github/github-mcp-server) | MCP server | Important integration for coding-agent workflows. |
| [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices) | Security docs | Required reading for secure MCP host/server design. |
| [MCP Safety Audit](https://arxiv.org/abs/2504.03767) | Paper | Demonstrates real security failures enabled by MCP-style tool integration. |
| [MCPSafetyScanner](https://github.com/johnhalloran321/mcpsafetyscanner) | Tool | Scanner for MCP server security issues. |
| [NSA: Model Context Protocol Security](https://www.nsa.gov/Portals/75/documents/Cybersecurity/CSI_MCP_SECURITY.pdf) | Security guidance | Government security guidance for MCP adoption. |

### Context and Repo Guidance

| Resource | Type | Why it matters |
|---|---|---|
| [AGENTS.md](https://agents.md/) | Open format | Simple repo-level instruction format for coding agents. |
| [AGENTS.md GitHub repo](https://github.com/agentsmd/agents.md) | Repo | Source for AGENTS.md examples and adoption. |
| [Evaluating AGENTS.md](https://arxiv.org/abs/2602.11988) | Paper | Important empirical warning: repo context files can reduce task success when overloaded. |
| [Configuring Agentic AI Coding Tools](https://arxiv.org/abs/2602.14690) | Paper | Analyzes configuration mechanisms across Claude Code, Copilot, Cursor, Gemini, and Codex. |
| [OpenAI Codex AGENTS.md example](https://github.com/openai/codex/blob/main/AGENTS.md) | Example | Real-world AGENTS.md usage in a coding-agent repo. |

## Workspace and Runtime State

| Resource | Type | Why it matters |
|---|---|---|
| [Resilient Write paper](https://arxiv.org/abs/2604.10842) | Paper | Durable write surface for coding agents. Very relevant to workspace design. |
| [Resilient Write blog](https://sperixlabs.org/post/2026/04/resilient-write-giving-coding-agents-a-write-path-that-doesnt-break/) | Blog | More engineering-oriented explanation of durable write paths. |
| [BranchFS](https://github.com/multikernel/branchfs) | Filesystem project | FUSE-based copy-on-write branching workspace. Useful for fork/snapshot semantics. |
| [TClone](https://arxiv.org/abs/2605.17320) | Paper | Low-latency forking of live GUI workspaces for computer-use agents. |
| [Git worktree docs](https://git-scm.com/docs/git-worktree) | Git docs | Basic primitive for isolated local candidate workspaces. |
| [Git apply docs](https://git-scm.com/docs/git-apply) | Git docs | Basis for patch-based publish. |
| [Git format-patch docs](https://git-scm.com/docs/git-format-patch) | Git docs | Basis for exporting deltas and patch bundles. |
| [GitHub Pull Requests docs](https://docs.github.com/en/pull-requests) | Workflow docs | Publish target for coding-agent output. |
| [GitHub Actions docs](https://docs.github.com/en/actions) | CI docs | Common validation stage for agent-produced changes. |

### Workspace Review Questions

- Is workspace state durable beyond the sandbox?
- Is the source repo directly mutable?
- Can workspace state be forked?
- Are snapshots and deltas first-class?
- Can agent output be discarded safely?
- Is publish idempotent?
- Are artifacts stored separately from source changes?
- Is context materialized as files, prompts, or both?
- Are secrets excluded from workspace state?
- Can the system replay or audit what happened?

## Sandbox and Execution

| Resource | Type | Why it matters |
|---|---|---|
| [E2B docs](https://e2b.dev/docs) | Cloud sandbox docs | Cloud sandbox for AI agents. Useful for remote execution patterns. |
| [E2B GitHub](https://github.com/e2b-dev/e2b) | Repo | Open-source infrastructure for AI code execution sandboxes. |
| [Daytona docs](https://www.daytona.io/docs/en/getting-started/) | Sandbox docs | Secure sandbox runtime for AI-generated code. |
| [Daytona sandboxes docs](https://www.daytona.io/docs/en/sandboxes/) | Sandbox docs | Lifecycle and sandbox concepts. |
| [Firecracker](https://firecracker-microvm.github.io/) | MicroVM docs | Canonical microVM isolation technology. |
| [Firecracker GitHub](https://github.com/firecracker-microvm/firecracker) | Repo | Source and architecture reference. |
| [Firecracker paper](https://assets.amazon.science/96/c6/302e527240a3b1f86c86c3e8fc3d/firecracker-lightweight-virtualization-for-serverless-applications.pdf) | Paper | System design behind Firecracker. |
| [Docker Compose docs](https://docs.docker.com/compose/) | Local dev / runtime | Essential for local agent infra development and test stacks. |
| [Docker Engine docs](https://docs.docker.com/engine/) | Runtime docs | Container execution basics. |
| [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/) | Execution primitive | Smallest deployable unit in Kubernetes. |
| [Kubernetes Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/) | Execution primitive | Useful for batch agent runs and retryable executions. |

## Security, Policy, and Governance

| Resource | Type | Why it matters |
|---|---|---|
| [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Security checklist | Main LLM app threat categories. |
| [OWASP Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/) | Security guidance | Agent-specific threat model. |
| [Promptfoo docs](https://www.promptfoo.dev/docs/intro/) | Tool | Practical eval and red-team framework. |
| [Promptfoo OWASP Agentic AI docs](https://www.promptfoo.dev/docs/red-team/owasp-agentic-ai/) | Security eval | Agentic application red-team presets. |
| [Runtime Governance for Policy-Constrained Execution](https://arxiv.org/abs/2604.07833) | Paper | Good argument for separating agent cognition from runtime policy enforcement. |
| [AgentWall: A Runtime Safety Layer for Local AI Agents](https://arxiv.org/abs/2605.16265) | Paper | Runtime safety layer for local agents. |
| [Security Engineering, Ross Anderson](https://www.cl.cam.ac.uk/archive/rja14/book.html) | Book | Deep reference for security engineering, access control, and threat modeling. |
| [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices) | Security docs | Protocol-level security recommendations. |
| [MCP Safety Audit](https://arxiv.org/abs/2504.03767) | Paper | Concrete MCP exploit cases. |

### Policy Patterns

- **Least-privilege tools:** tools should expose narrow actions, not broad shells.
- **Workspace access grants:** short-lived scoped access to workspace paths and operations.
- **Brokered secrets:** agents request operations; the platform uses secrets without exposing them to the agent.
- **Publish approval:** source-of-truth changes require explicit publish.
- **Policy as transition guard:** policy should protect state transitions, not only command execution.
- **Audit-first execution:** every action should be attributable and replayable.

## Observability and Evaluation

| Resource | Type | Why it matters |
|---|---|---|
| [OpenTelemetry](https://opentelemetry.io/) | Observability standard | Vendor-neutral traces, metrics, and logs. |
| [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) | Collector | Standard telemetry pipeline. |
| [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) | Spec | Emerging schema for GenAI telemetry. |
| [OpenTelemetry GenAI semantic conventions repo](https://github.com/open-telemetry/semantic-conventions-genai) | Repo | GenAI-specific conventions. |
| [Langfuse docs](https://langfuse.com/docs) | OSS observability | Open-source LLM tracing, eval, prompt management. |
| [Langfuse GitHub](https://github.com/langfuse/langfuse) | Repo | Self-hostable observability platform. |
| [LangSmith observability](https://docs.langchain.com/langsmith/observability) | Observability docs | Good reference for full-stack LLM/agent observability. |
| [Promptfoo](https://github.com/promptfoo/promptfoo) | Eval / red-team | CLI and framework for LLM eval and red-teaming. |
| [SWE-bench](https://www.swebench.com/) | Benchmark | Canonical benchmark for real GitHub issue resolution. |
| [SWE-bench GitHub](https://github.com/swe-bench/SWE-bench) | Repo | Evaluation harness and datasets. |
| [SWE-agent experiments](https://github.com/swe-bench/experiments) | Eval logs | Open predictions, logs, trajectories, and results. |
| [AIDev: Studying AI Coding Agents on GitHub](https://arxiv.org/abs/2602.09185) | Paper | Large-scale empirical study of real coding-agent PRs. |

### Observability Checklist

A production agent run should record:

- Run ID
- Workspace ID
- Model and harness
- Tool calls
- File changes
- Command execution
- Cost and latency
- Policy decisions
- Publish attempts
- External references such as PR URLs
- Error and retry history
- Final outcome

## Coding-Agent Workflows

| Resource | Type | Why it matters |
|---|---|---|
| [SWE-agent](https://github.com/swe-agent/swe-agent) | Agent scaffold | Important baseline for issue-solving agents. |
| [mini-SWE-agent](https://github.com/swe-agent/mini-swe-agent) | Minimal implementation | Useful for understanding how small the loop can be. |
| [SWE-bench](https://www.swebench.com/) | Benchmark | Standard benchmark for GitHub issue resolution. |
| [AIDev](https://arxiv.org/abs/2602.09185) | Paper | Real-world agent-authored PR study. |
| [OpenHands GitHub Action](https://docs.openhands.dev/openhands/usage/run-openhands/github-action) | Workflow docs | Example of integrating a coding agent into GitHub workflows. |
| [OpenHands automated code review](https://docs.openhands.dev/openhands/usage/use-cases/code-review) | Workflow docs | Coding-agent code review flow. |
| [GitHub MCP Server](https://github.com/github/github-mcp-server) | MCP server | Agent integration with GitHub issues, repos, and PRs. |
| [GitHub Copilot: The agent awakens](https://github.blog/news-insights/product-news/github-copilot-the-agent-awakens/) | Product / workflow | Useful view into mainstream coding-agent workflows. |
| [OpenAI Codex AGENTS.md example](https://github.com/openai/codex/blob/main/AGENTS.md) | Repo config | Example context file for a coding-agent project. |

## Data Layer and Storage

| Resource | Type | Why it matters |
|---|---|---|
| [PostgreSQL](https://www.postgresql.org/) | Database | Strong default metadata store for agent infra. |
| [PostgreSQL JSONB docs](https://www.postgresql.org/docs/current/datatype-json.html) | Docs | Useful for storing workspace specs, policy, and source references. |
| [PostgreSQL advisory locks](https://www.postgresql.org/docs/current/explicit-locking.html) | Docs | Useful for workspace locks and publish locks. |
| [PostgreSQL license](https://www.postgresql.org/about/licence/) | License | Permissive license background. |
| [Kysely](https://kysely.dev/) | TypeScript SQL builder | Good explicit SQL-shaped query layer. |
| [Kysely GitHub](https://github.com/kysely-org/kysely) | Repo | Type-safe query builder. |
| [AWS SDK v3 S3 examples](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/javascript_s3_code_examples.html) | Docs | Reference for S3-compatible object storage integration. |
| [AWS SDK JS v3 GitHub](https://github.com/aws/aws-sdk-js-v3) | Repo | SDK implementation. |
| [MinIO docs](https://docs.min.io/aistor/) | Docs | S3-compatible object storage reference. |
| [Docker Compose](https://docs.docker.com/compose/) | Local dev | Useful for local Postgres, object store, and telemetry stacks. |
| [Fastify](https://fastify.io/) | Node.js server | Good API server candidate for TypeScript infra. |
| [Zod](https://zod.dev/) | Validation | TypeScript-first validation for specs and API payloads. |

## Books

| Book | Why it matters |
|---|---|
| [Designing Data-Intensive Applications](https://dataintensive.net/) | State, consistency, durability, lineage, logs, storage, and systems tradeoffs. |
| [Designing Data-Intensive Applications, O'Reilly](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/) | Publisher page. |
| [Google SRE Books](https://sre.google/books/) | Reliability, operations, incident response, SLOs, and production discipline. |
| [Site Reliability Engineering table of contents](https://sre.google/sre-book/table-of-contents/) | Free online SRE book. |
| [Security Engineering](https://www.cl.cam.ac.uk/archive/rja14/book.html) | Security, access control, threat modeling, and system design. |
| [Operating Systems: Three Easy Pieces](https://pages.cs.wisc.edu/~remzi/OSTEP/) | Processes, virtualization, concurrency, persistence, and filesystems. |
| [Distributed Systems, Maarten van Steen](https://www.distributed-systems.net/index.php/books/ds4/) | Naming, replication, consistency, coordination, and fault tolerance. |

## Videos and Talks

### MCP and Tool Protocol

| Video | Why watch |
|---|---|
| [The Model Context Protocol](https://www.youtube.com/watch?v=CQywdSdi5iA) | Good MCP overview. |
| [Building Agents with Model Context Protocol - Full Workshop](https://www.youtube.com/watch?v=kQmXtrmQ5Zg) | Practical MCP workshop. |
| [MCP 201 - Code w/ Claude](https://www.youtube.com/watch?v=HNzH5Us1Rvg) | More advanced MCP talk. |
| [Why we built-and donated-the Model Context Protocol](https://www.youtube.com/watch?v=PLyCki2K0Lg) | Standardization and governance context. |
| [The Creators of Model Context Protocol](https://www.youtube.com/watch?v=m2VqaNKstGc) | Interview-style protocol background. |

### Runtime and Durable Execution

| Video | Why watch |
|---|---|
| [LangGraph: Intro](https://www.youtube.com/watch?v=5h-JBkySK34) | Intro to graph-based agent runtime. |
| [LangGraph Essentials](https://www.youtube.com/watch?v=B_BCeWhyD5Q) | Higher-level overview of LangGraph. |
| [LangGraph Crash Course](https://www.youtube.com/watch?v=uWLJAtMOVT0) | Practical walkthrough. |
| [Durable AI Agents: LangGraph.js](https://www.youtube.com/watch?v=22Zv8VQ8PuI) | Durable execution in LangGraph.js. |
| [Building Durable, Long-Running Autonomous Agents](https://www.youtube.com/watch?v=aYSl1hbuPfs) | Durable agent workflows. |

### Sandbox Videos

| Video | Why watch |
|---|---|
| [AWS re:Invent Firecracker talk](https://www.youtube.com/watch?v=yDplzXEdBTI) | Firecracker architecture and motivation. |
| [Firecracker: Secure and Fast microVM](https://www.youtube.com/watch?v=PAEMGa-i2lU) | MicroVM isolation details. |
| [Face off: VMs vs Containers vs Firecracker](https://www.youtube.com/watch?v=pTQ_jVYhAoc) | Isolation tradeoffs. |
| [How AWS's Firecracker virtual machines work](https://www.youtube.com/watch?v=BIRv2FnHJAg) | Explainer on Firecracker. |
| [How AI Agents Execute Code](https://www.youtube.com/watch?v=5FCu6YqWA6U) | Runtime environment for AI code execution. |

### Observability Videos

| Video | Why watch |
|---|---|
| [OpenTelemetry for GenAI and OpenLLMetry](https://www.youtube.com/watch?v=JnQXEMHh3aw) | GenAI observability concepts. |
| [How OpenTelemetry Helps Generative AI](https://www.youtube.com/watch?v=92oGRCC8ktA) | Practical OTel and GenAI framing. |
| [Making GenAI Observable with OpenTelemetry](https://www.youtube.com/watch?v=RNaa_48LWBY) | GenAI telemetry talk. |
| [How To Debug AI Agents: Tracing, Observability & Evals](https://www.youtube.com/watch?v=nWNWrtCDqaY) | Debugging agent systems. |
| [Promptfoo Red Team Tutorial](https://www.youtube.com/watch?v=KghDstjwwNA) | Practical red-team and eval tutorial. |

### Coding Agents

| Video | Why watch |
|---|---|
| [Software Development Agents: What Works and What Doesn't](https://www.youtube.com/watch?v=o_hhkJtlbSs) | Practical OpenHands perspective. |
| [OpenHands Community: Agent Control Plane](https://www.youtube.com/watch?v=20HNd4cb2vA) | Agent control-plane discussion. |
| [Dynamic Workflows using OpenHands SDK](https://www.youtube.com/watch?v=PtbrKTgj3X8) | SDK workflow concepts. |
| [OpenAI Codex Tutorial: AGENTS.md](https://www.youtube.com/watch?v=NlNuoH5PPl4) | Coding-agent repo guidance file usage. |
| [Code w/ Claude Developer Conference playlist](https://www.youtube.com/playlist?list=PLf2m23nhTg1P5BsOHUOXyQz5RhfUSSVUi) | Claude Code, MCP, and agent workflow talks. |

### Chinese-language Supplements

| Resource | Why include |
|---|---|
| [MCP 核心架构解析](https://www.bilibili.com/opus/1022254559229116469) | Chinese overview of MCP architecture. |
| [[中文字幕] MCP 快速入门](https://www.bilibili.com/video/BV1pHdnYyE8v/) | Chinese MCP intro video. |
| [MCP 作者详解 MCP 协议](https://www.bilibili.com/video/BV1NwQhYeES3/) | Bilingual MCP explanation. |

## Related Awesome Lists

| List | Focus |
|---|---|
| [awesome-agentic-ai](https://github.com/mfornos/awesome-agentic-ai) | Broad principles, standards, and technologies for agentic AI. |
| [awesome-production-agentic-systems](https://github.com/EthicalML/awesome-production-agentic-systems) | Production-oriented libraries and systems. |
| [awesome-harness-engineering](https://github.com/ai-boost/awesome-harness-engineering) | Harness engineering, tools, evals, memory, MCP, permissions. |
| [awesome-agents](https://github.com/kyrolabs/awesome-agents) | General list of AI agents. |
| [awesome-ai-agents](https://github.com/e2b-dev/awesome-ai-agents) | General autonomous agent list. |
| [awesome-ai-sandboxes](https://github.com/tizkovatereza/awesome-ai-sandboxes) | AI sandbox providers and runtime environments. |
| [awesome-agent-orchestration](https://github.com/vivy-yi/awesome-agent-orchestration) | Agent orchestration and multi-agent systems. |
| [awesome-ai-agent-papers](https://github.com/VoltAgent/awesome-ai-agent-papers) | Papers on AI agents. |

## Patterns

### Candidate Workspace

Agents should work in a candidate workspace, not directly in the source repo.

```text
source repo
  -> candidate workspace
  -> agent modifies candidate
  -> diff / tests / review
  -> publish or discard
```

Useful resources:

- [Git worktree docs](https://git-scm.com/docs/git-worktree)
- [Resilient Write](https://arxiv.org/abs/2604.10842)
- [BranchFS](https://github.com/multikernel/branchfs)
- [TClone](https://arxiv.org/abs/2605.17320)

### Publish / Discard

Agent output should not automatically become source-of-truth.

A publish operation should record:

- Idempotency key
- Target type
- Target branch or PR
- External URL
- Status
- Error if failed
- Associated workspace delta
- Actor or approval

Useful resources:

- [Temporal durable execution](https://temporal.io/blog/what-is-durable-execution)
- [Git apply](https://git-scm.com/docs/git-apply)
- [GitHub Pull Requests](https://docs.github.com/en/pull-requests)

### Brokered Secrets

Agents should not receive long-lived provider credentials by default.

```text
agent produces candidate output
platform reviews and approves
publish broker uses secret from vault
agent never sees raw token
```

Useful resources:

- [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)
- [Security Engineering](https://www.cl.cam.ac.uk/archive/rja14/book.html)
- [OWASP Agentic AI threats](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/)

### Runtime Governance

Policy should be outside the model loop.

```text
model proposes action
runtime checks policy
tool executes only if approved
event is recorded
```

Useful resources:

- [Runtime Governance for Policy-Constrained Execution](https://arxiv.org/abs/2604.07833)
- [MCP Safety Audit](https://arxiv.org/abs/2504.03767)
- [Promptfoo](https://www.promptfoo.dev/docs/intro/)

### Context Provenance

Record what context the agent saw.

Examples:

- AGENTS.md version
- Task prompt
- Issue or PR source
- Context documents
- Selected files
- Injected memory
- Policy profile
- Workspace snapshot
- Tool list

Useful resources:

- [AGENTS.md](https://agents.md/)
- [Evaluating AGENTS.md](https://arxiv.org/abs/2602.11988)
- [Configuring Agentic AI Coding Tools](https://arxiv.org/abs/2602.14690)

### Observability by Default

Each run should emit traces and events for:

- Model calls
- Tool calls
- Command execution
- File changes
- Policy decisions
- Workspace snapshots
- Publish attempts
- Errors and retries

Useful resources:

- [OpenTelemetry](https://opentelemetry.io/)
- [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/)
- [Langfuse](https://langfuse.com/docs)
- [LangSmith observability](https://docs.langchain.com/langsmith/observability)

## Contributing

Contributions are welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) before opening a pull request.

A resource belongs here if it helps answer at least one of these questions:

- How should an agent runtime manage state?
- How should tools be exposed safely?
- How should workspace changes be isolated and published?
- How should sandboxes execute untrusted or semi-trusted actions?
- How should agent runs be traced, evaluated, and replayed?
- How should secrets, permissions, and policy be enforced?
- How should coding agents integrate with repos, issues, PRs, and CI?

A resource does not belong here if it is only:

- A generic prompt engineering article
- An end-user chatbot product
- A generic AI app directory
- A model leaderboard with no infrastructure implications
- A shallow tutorial with no reusable systems insight

## License

Apache-2.0. See [LICENSE](LICENSE).
