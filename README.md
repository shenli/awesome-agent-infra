# Awesome Agent Infra [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated collection of infrastructure resources for building production AI agents: runtimes, workspaces, sandboxes, tool protocols, context systems, security, observability, and evaluation.

Last reviewed: 2026-07

This list focuses on the **systems layer below agent products and above foundation models**.

It is not a general "awesome AI agents" list. It is focused on the infrastructure needed to run agents safely and reliably in production.

Organized around one question, asked of every component: *what state is this, and where does it belong?*

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

| Concept               | Meaning                                                                                                            |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **Agent runtime**     | The execution layer that runs agent loops, manages state, retries, tools, and human interaction.                   |
| **Harness**           | The model-facing loop and scaffolding that turns model outputs into actions.                                       |
| **Workspace**         | The durable working state an agent reads and writes during a task. Not just a folder.                              |
| **Sandbox**           | The isolated compute environment where actions execute.                                                            |
| **Session / run**     | The ordered record of an agent execution attempt.                                                                  |
| **Tool protocol**     | The interface by which agents discover and call external tools or resources.                                       |
| **Policy**            | Runtime constraints over tools, data, paths, permissions, and publish actions.                                     |
| **Publish lifecycle** | The process of promoting candidate agent output into source-of-truth systems.                                      |
| **Observability**     | Traces, logs, metrics, costs, evals, and replay data for agent behavior.                                           |
| **Storage concern**   | The persistence needs around agent metadata, conversations, run events, workspaces, artifacts, memory, and traces. |

## Foundational Articles

| Resource                                                                                                                                                                 | Layer                           | Why it matters                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)                                                                     | Runtime                         | Practical guide arguing for simple composable agent patterns instead of over-engineered abstractions.                            |
| [Anthropic: Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)                              | Context / Runtime               | Good framing for context as runtime design rather than prompt stuffing.                                                          |
| [Anthropic: Writing Effective Tools for AI Agents](https://www.anthropic.com/engineering/writing-tools-for-agents)                                                       | Tooling                         | Useful for designing tool APIs agents can actually use.                                                                          |
| [Martin Fowler: Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html)                        | Coding agents / Context         | Strong developer-facing explanation of workspace files and repo context for coding agents.                                       |
| [Temporal: What Is Durable Execution?](https://temporal.io/blog/what-is-durable-execution)                                                                               | Durable execution               | Core concept for long-running, crash-resilient workflows.                                                                        |
| [DBOS: Durable Execution for Crashproof AI Agents](https://www.dbos.dev/blog/durable-execution-crashproof-ai-agents)                                                     | Durable execution               | Applies durable execution ideas directly to AI agents.                                                                           |
| [GitHub Blog: A practical guide on how to use the GitHub MCP server](https://github.blog/ai-and-ml/generative-ai/a-practical-guide-on-how-to-use-the-github-mcp-server/) | Tool protocol / GitHub workflow | Practical reference for MCP + GitHub integration.                                                                                |
| [Anthropic: Building with Claude Managed Agents](https://claude.com/blog/building-with-claude-managed-agents)                                                            | Runtime / memory                | First-party architecture note for managed agents: delegation, session continuity, credentials, and memory consolidation.         |
| [OpenAI: Sandbox Agents documentation](https://developers.openai.com/api/docs/guides/agents/sandboxes)                                                                   | Runtime / sandbox               | Clear harness-versus-compute split for agent systems, with credentials and control-plane work kept outside the sandbox boundary. |
| [OpenAI: The next evolution of the Agents SDK](https://openai.com/index/the-next-evolution-of-the-agents-sdk/)                                                           | Runtime / SDK                   | Official launch context for Sandbox Agents and the Agents SDK direction.                                                         |
| [Vercel: Agentic Infrastructure](https://vercel.com/blog/agentic-infrastructure)                                                                                         | Platform                        | Product-level framing of sandboxes, workflows, gateway, and observability as agent infrastructure components.                    |
| [HumanLayer: 12-Factor Agents](https://github.com/humanlayer/12-factor-agents)                                                                                           | Runtime / state                 | Strong articulation of agents as reducers over an append-only event log.                                                         |
| [Manus: Context Engineering for AI Agents](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus)                                          | Context / workspace             | Production note arguing for filesystem-backed context and stable append-only traces.                                             |
| [Microsoft Agent Framework at Build 2026](https://devblogs.microsoft.com/agent-framework/microsoft-agent-framework-at-build-2026-announce/)                              | Runtime / hosted agents         | First-party description of Agent Harness, hosted agents, per-session VM isolation, filesystem persistence, and OpenTelemetry.    |
| [OpenRath: Session-Centered Runtime State for Agent Systems](https://arxiv.org/abs/2606.19409)                                                                           | Runtime state                   | Makes the case for session as a first-class runtime value rather than incidental chat history.                                   |

## Runtime and Control Plane

### Projects

| Project                                                                                            | Type                         | Why it matters                                                                                                                               |
| -------------------------------------------------------------------------------------------------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| [LangGraph](https://github.com/langchain-ai/langgraph)                                             | Runtime framework            | Stateful graph runtime for long-running agents, persistence, human-in-the-loop, and durable execution.                                       |
| [LangGraph docs](https://docs.langchain.com/oss/python/langgraph/overview)                         | Docs                         | Good reference for durable agent orchestration concepts.                                                                                     |
| [OpenAI Agents SDK Python](https://github.com/openai/openai-agents-python)                         | SDK                          | Lightweight SDK for building agentic apps. Useful baseline for minimal abstractions.                                                         |
| [OpenAI Agents SDK TypeScript](https://openai.github.io/openai-agents-js/)                         | SDK                          | TypeScript version, useful for JS/TS infrastructure builders.                                                                                |
| [Omnigent](https://github.com/omnigent-ai/omnigent)                                                | Meta-harness / control plane | Common orchestration layer over coding agents and custom agents, with policies, sandboxing, shared sessions, and multi-device collaboration. |
| [LiteLLM Agent Platform](https://github.com/BerriAI/litellm-agent-platform)                        | Agent platform               | Self-hostable control plane for calling and managing coding agents with per-session isolation and shared proxy infrastructure.               |
| [LiteLLM Agent Runtime](https://github.com/BerriAI/litellm-agent-runtime)                          | Runtime                      | Coding-agent daemon designed to run inside per-session VMs, with customization layered through repo, team, and session config.               |
| [Microsoft Foundry Agent Service](https://devblogs.microsoft.com/foundry/agent-service-build2026/) | Hosted runtime               | Framework-agnostic hosted agent service with session isolation, durable state, tracing, evaluation, and production deployment hooks.         |
| [OpenHands](https://github.com/OpenHands/OpenHands)                                                | Agent platform               | Full open-source software-agent platform with sandboxed execution and developer workflows.                                                   |
| [OpenHands Software Agent SDK](https://github.com/OpenHands/software-agent-sdk)                    | SDK                          | Composable SDK for building software-development agents.                                                                                     |
| [SWE-agent](https://github.com/swe-agent/swe-agent)                                                | Coding-agent scaffold        | Simple and influential coding-agent scaffold for GitHub issue solving.                                                                       |
| [mini-SWE-agent](https://github.com/swe-agent/mini-swe-agent)                                      | Minimal agent                | Small baseline for understanding the minimal loop needed to solve coding tasks.                                                              |
| [Goose](https://github.com/aaif-goose/goose)                                                       | Local agent runtime          | General-purpose open-source agent with CLI, desktop, API, and MCP extension ecosystem.                                                       |
| [Semantic Kernel](https://github.com/microsoft/semantic-kernel)                                    | Enterprise SDK               | Enterprise-oriented orchestration and agent framework from Microsoft.                                                                        |
| [CrewAI](https://github.com/crewAIInc/crewAI)                                                      | Multi-agent framework        | Popular multi-agent orchestration framework.                                                                                                 |
| [AutoGen](https://github.com/microsoft/autogen)                                                    | Multi-agent framework        | Influential multi-agent framework. Useful historically and architecturally.                                                                  |
| [Letta](https://github.com/letta-ai/letta)                                                         | Stateful agents / memory     | Platform for stateful agents with advanced memory. Useful for understanding memory-first agent design.                                       |
| [Letta Code](https://github.com/letta-ai/letta-code)                                               | Coding agent / memory        | Memory-first coding agent. Useful contrast with workspace-first designs.                                                                     |

### Papers

| Paper                                                                                                           | Why it matters                                                                                           |
| --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| [Infrastructure for AI Agents](https://arxiv.org/abs/2501.10114)                                                | Defines agent infrastructure as external technical systems and protocols that mediate agent interaction. |
| [AI Runtime Infrastructure](https://arxiv.org/abs/2603.00495)                                                   | Proposes runtime infrastructure between model and application. Useful for control-plane framing.         |
| [OpenHands: An Open Platform for AI Software Developers as Generalist Agents](https://arxiv.org/abs/2407.16741) | Important system paper for software agents.                                                              |
| [The OpenHands Software Agent SDK](https://arxiv.org/abs/2511.03690)                                            | Architecture of a composable SDK for production software agents.                                         |
| [Agents Learn Their Runtime](https://arxiv.org/abs/2603.01209)                                                  | Shows that runtime persistence semantics affect agent behavior.                                          |

## Tool Protocols and Context Interfaces

### MCP

| Resource                                                                                                            | Type              | Why it matters                                                             |
| ------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------------------------------------------------------------------- |
| [Model Context Protocol official docs](https://modelcontextprotocol.io/docs/getting-started/intro)                  | Docs              | Main entry point for MCP.                                                  |
| [MCP specification](https://modelcontextprotocol.io/specification/draft)                                            | Spec              | Protocol details.                                                          |
| [MCP TypeScript SDK](https://github.com/modelcontextprotocol/typescript-sdk)                                        | SDK               | Official TypeScript SDK.                                                   |
| [MCP servers repository](https://github.com/modelcontextprotocol/servers)                                           | Repo              | Reference and community MCP server directory.                              |
| [GitHub MCP Server](https://github.com/github/github-mcp-server)                                                    | MCP server        | Important integration for coding-agent workflows.                          |
| [MCP security best practices](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices)      | Security docs     | Required reading for secure MCP host/server design.                        |
| [MCP Safety Audit](https://arxiv.org/abs/2504.03767)                                                                | Paper             | Demonstrates real security failures enabled by MCP-style tool integration. |
| [MCPSafetyScanner](https://github.com/johnhalloran321/mcpsafetyscanner)                                             | Tool              | Scanner for MCP server security issues.                                    |
| [NSA: Model Context Protocol Security](https://www.nsa.gov/Portals/75/documents/Cybersecurity/CSI_MCP_SECURITY.pdf) | Security guidance | Government security guidance for MCP adoption.                             |

### Context and Repo Guidance

| Resource                                                                              | Type        | Why it matters                                                                            |
| ------------------------------------------------------------------------------------- | ----------- | ----------------------------------------------------------------------------------------- |
| [AGENTS.md](https://agents.md/)                                                       | Open format | Simple repo-level instruction format for coding agents.                                   |
| [AGENTS.md GitHub repo](https://github.com/agentsmd/agents.md)                        | Repo        | Source for AGENTS.md examples and adoption.                                               |
| [Evaluating AGENTS.md](https://arxiv.org/abs/2602.11988)                              | Paper       | Important empirical warning: repo context files can reduce task success when overloaded.  |
| [Configuring Agentic AI Coding Tools](https://arxiv.org/abs/2602.14690)               | Paper       | Analyzes configuration mechanisms across Claude Code, Copilot, Cursor, Gemini, and Codex. |
| [OpenAI Codex AGENTS.md example](https://github.com/openai/codex/blob/main/AGENTS.md) | Example     | Real-world AGENTS.md usage in a coding-agent repo.                                        |

## Workspace and Runtime State

| Resource                                                                                                                         | Type               | Why it matters                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------- | ------------------ | --------------------------------------------------------------------------------- |
| [Resilient Write paper](https://arxiv.org/abs/2604.10842)                                                                        | Paper              | Durable write surface for coding agents. Very relevant to workspace design.       |
| [Resilient Write blog](https://sperixlabs.org/post/2026/04/resilient-write-giving-coding-agents-a-write-path-that-doesnt-break/) | Blog               | More engineering-oriented explanation of durable write paths.                     |
| [BranchFS](https://github.com/multikernel/branchfs)                                                                              | Filesystem project | FUSE-based copy-on-write branching workspace. Useful for fork/snapshot semantics. |
| [TClone](https://arxiv.org/abs/2605.17320)                                                                                       | Paper              | Low-latency forking of live GUI workspaces for computer-use agents.               |
| [Git worktree docs](https://git-scm.com/docs/git-worktree)                                                                       | Git docs           | Basic primitive for isolated local candidate workspaces.                          |
| [Git apply docs](https://git-scm.com/docs/git-apply)                                                                             | Git docs           | Basis for patch-based publish.                                                    |
| [Git format-patch docs](https://git-scm.com/docs/git-format-patch)                                                               | Git docs           | Basis for exporting deltas and patch bundles.                                     |
| [GitHub Pull Requests docs](https://docs.github.com/en/pull-requests)                                                            | Workflow docs      | Publish target for coding-agent output.                                           |
| [GitHub Actions docs](https://docs.github.com/en/actions)                                                                        | CI docs            | Common validation stage for agent-produced changes.                               |

## Sandbox and Execution

This section is intentionally larger than a provider list. For agent infrastructure, "sandbox" spans several layers:

| Layer                            | What it controls                                                                                                |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Managed agent sandboxes**      | Hosted or self-hosted environments for code execution, terminal access, files, and long-running agent tasks.    |
| **Browser / desktop sandboxes**  | Browser or GUI environments where agents click, type, inspect pages, and sometimes hand control back to humans. |
| **Container isolation**          | Namespaces, cgroups, seccomp, AppArmor/SELinux, rootless containers, and runtime configuration.                 |
| **MicroVM / VM isolation**       | Stronger isolation boundary for untrusted workloads, usually with higher operational complexity.                |
| **Kernel / process confinement** | Fine-grained syscall, filesystem, network, and process controls.                                                |
| **Orchestration**                | Scheduling, retries, quotas, lifecycle, volumes, networking, and cleanup for many sandbox runs.                 |

### Managed Agent Sandboxes

| Resource                                                                                                                               | Type               | Why it matters                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------- |
| [E2B docs](https://e2b.dev/docs)                                                                                                       | Cloud sandbox docs | Cloud sandbox for AI agents. Useful for remote execution, code interpreter, and agent runtime patterns.           |
| [E2B GitHub](https://github.com/e2b-dev/e2b)                                                                                           | Repo               | Open-source infrastructure for AI code execution sandboxes.                                                       |
| [E2B coding agents docs](https://e2b.dev/docs/use-cases/coding-agents)                                                                 | Use-case docs      | Shows how secure sandboxes are exposed to coding agents with terminal, filesystem, and Git access.                |
| [E2B cookbook](https://github.com/e2b-dev/e2b-cookbook)                                                                                | Examples           | Practical examples for using E2B SDKs.                                                                            |
| [E2B code interpreter](https://github.com/e2b-dev/code-interpreter)                                                                    | SDK / project      | Reference for safe code execution as a productized primitive.                                                     |
| [Daytona docs](https://www.daytona.io/docs/en/getting-started/)                                                                        | Sandbox docs       | Secure sandbox runtime for AI-generated code.                                                                     |
| [Daytona sandboxes docs](https://www.daytona.io/docs/en/sandboxes/)                                                                    | Sandbox docs       | Lifecycle and sandbox concepts.                                                                                   |
| [Daytona GitHub](https://github.com/daytonaio/daytona)                                                                                 | Repo               | Secure and elastic runtime for AI-generated code execution and agent workflows.                                   |
| [Daytona docs repo](https://github.com/daytonaio/docs)                                                                                 | Docs repo          | Useful for understanding their public API and docs structure.                                                     |
| [Modal](https://modal.com/)                                                                                                            | Serverless compute | Useful reference for fast, dynamic cloud execution, even if not agent-specific.                                   |
| [Modal docs](https://modal.com/docs)                                                                                                   | Docs               | Good reference for serverless execution, container images, sandboxes, secrets, and jobs.                          |
| [Modal Sandbox docs](https://modal.com/docs/guide/sandbox)                                                                             | Sandbox docs       | Useful example of exposing programmatic sandboxed command execution.                                              |
| [Modal: Code execution sandboxes for browser-use agents](https://modal.com/resources/best-code-execution-sandboxes-browser-use-agents) | Scale note         | Public production-scale numbers for agent sandbox concurrency and session volume.                                 |
| [Northflank: E2B vs Modal](https://northflank.com/blog/e2b-vs-modal)                                                                   | Comparison article | Helpful market and architecture comparison for AI code execution sandboxes.                                       |
| [Blaxel Sandboxes](https://docs.blaxel.ai/Sandboxes/Overview)                                                                          | Sandbox docs       | Distinguishes snapshot-backed standby from durable-volume persistence, a useful split for agent workspace design. |

### Browser, GUI, and Computer-Use Sandboxes

| Resource                                                                | Type                            | Why it matters                                                                             |
| ----------------------------------------------------------------------- | ------------------------------- | ------------------------------------------------------------------------------------------ |
| [Browserbase docs](https://docs.browserbase.com/)                       | Browser sandbox docs            | Cloud browser infrastructure for browser agents and automation.                            |
| [Browserbase](https://www.browserbase.com/)                             | Browser infrastructure          | Useful reference for running browser sessions remotely for agents.                         |
| [Stagehand docs](https://docs.stagehand.dev/)                           | Browser-agent framework docs    | Browser automation framework built around AI-assisted browser actions.                     |
| [Stagehand GitHub](https://github.com/browserbase/stagehand)            | Repo                            | Open-source browser automation framework for AI agents.                                    |
| [browser-use GitHub](https://github.com/browser-use/browser-use)        | Browser agent project           | Popular open-source project for browser-using agents.                                      |
| [browser-use docs](https://docs.browser-use.com/)                       | Docs                            | Practical browser-agent execution and automation patterns.                                 |
| [Microsoft Playwright MCP](https://github.com/microsoft/playwright-mcp) | MCP server                      | Browser automation through MCP using Playwright.                                           |
| [Playwright docs](https://playwright.dev/docs/intro)                    | Browser automation docs         | Useful lower-level browser automation primitive.                                           |
| [Scrapybara docs](https://docs.scrapybara.com/)                         | Browser / computer sandbox docs | Reference for hosted computer-use and browser sandboxes.                                   |
| [Scrapybara GitHub](https://github.com/scrapybara/scrapybara)           | Repo                            | Agent-facing computer-use sandbox project.                                                 |
| [BrowserArena](https://arxiv.org/abs/2510.02418)                        | Paper / eval                    | Live open-web agent evaluation platform; useful for understanding web-agent failure modes. |
| [FP-Agent](https://arxiv.org/abs/2605.01247)                            | Paper                           | Fingerprinting AI browsing agents; relevant for browser-agent detection and control.       |

### MicroVM and VM Isolation

| Resource                                                                                                                                                     | Type                  | Why it matters                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- | ------------------------------------------------------------------------------------- |
| [Firecracker](https://firecracker-microvm.github.io/)                                                                                                        | MicroVM docs          | Canonical microVM isolation technology.                                               |
| [Firecracker GitHub](https://github.com/firecracker-microvm/firecracker)                                                                                     | Repo                  | Source and architecture reference.                                                    |
| [Firecracker paper](https://assets.amazon.science/96/c6/302e527240a3b1f86c86c3e8fc3d/firecracker-lightweight-virtualization-for-serverless-applications.pdf) | Paper                 | System design behind Firecracker.                                                     |
| [Firecracker getting started](https://github.com/firecracker-microvm/firecracker/blob/main/docs/getting-started.md)                                          | Docs                  | Practical details of launching a microVM.                                             |
| [AWS Lambda MicroVMs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-microvms-guide.html)                                                               | AWS docs              | Shows how Firecracker-style microVMs are used in a production serverless environment. |
| [Cloud Hypervisor](https://www.cloudhypervisor.org/)                                                                                                         | VMM project           | Rust-based VMM focused on modern cloud workloads.                                     |
| [Cloud Hypervisor GitHub](https://github.com/cloud-hypervisor/cloud-hypervisor)                                                                              | Repo                  | Useful reference for VMM architecture and cloud VM lifecycle.                         |
| [QEMU](https://www.qemu.org/)                                                                                                                                | Emulator / VMM        | General-purpose virtualization and emulation baseline.                                |
| [KVM docs](https://www.linux-kvm.org/page/Main_Page)                                                                                                         | Kernel virtualization | Linux kernel virtualization foundation used by many VM and microVM systems.           |
| [Kata Containers](https://katacontainers.io/)                                                                                                                | Secure containers     | Combines container UX with VM isolation.                                              |
| [Kata Containers docs](https://katacontainers.io/docs/)                                                                                                      | Docs                  | Useful reference for VM-backed container isolation.                                   |
| [Kata Containers GitHub](https://github.com/kata-containers/kata-containers)                                                                                 | Repo                  | Implementation reference for container-like VM isolation.                             |

### Container Isolation and Runtime Hardening

| Resource                                                                  | Type                | Why it matters                                                                               |
| ------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------------------------------------- |
| [Docker Engine docs](https://docs.docker.com/engine/)                     | Runtime docs        | Container execution basics.                                                                  |
| [Docker Compose docs](https://docs.docker.com/compose/)                   | Local dev / runtime | Essential for local agent infra development and test stacks.                                 |
| [Docker security docs](https://docs.docker.com/engine/security/)          | Security docs       | Container security baseline: namespaces, capabilities, seccomp, rootless mode, daemon risks. |
| [Docker seccomp docs](https://docs.docker.com/engine/security/seccomp/)   | Security docs       | Default seccomp profile and syscall restrictions.                                            |
| [Docker rootless mode](https://docs.docker.com/engine/security/rootless/) | Security docs       | Useful for reducing daemon and root risk in local sandboxes.                                 |
| [Docker AppArmor docs](https://docs.docker.com/engine/security/apparmor/) | Security docs       | AppArmor profile support for Docker containers.                                              |
| [containerd](https://containerd.io/)                                      | Runtime             | Core container runtime used by many systems.                                                 |
| [containerd GitHub](https://github.com/containerd/containerd)             | Repo                | Implementation reference for container lifecycle.                                            |
| [runc](https://github.com/opencontainers/runc)                            | OCI runtime         | Low-level OCI container runtime used by Docker and containerd.                               |
| [OCI Runtime Spec](https://github.com/opencontainers/runtime-spec)        | Spec                | Standard interface for container runtimes.                                                   |
| [Podman](https://podman.io/)                                              | Container runtime   | Daemonless container engine, useful for rootless and local execution models.                 |
| [Podman docs](https://docs.podman.io/)                                    | Docs                | Rootless container and pod execution patterns.                                               |

### Linux Kernel and Process Confinement

| Resource                                                                             | Type                   | Why it matters                                                                                        |
| ------------------------------------------------------------------------------------ | ---------------------- | ----------------------------------------------------------------------------------------------------- |
| [Linux namespaces man page](https://man7.org/linux/man-pages/man7/namespaces.7.html) | Kernel docs            | Foundation for container isolation.                                                                   |
| [Linux cgroups v2 docs](https://docs.kernel.org/admin-guide/cgroup-v2.html)          | Kernel docs            | CPU, memory, IO, and process resource control.                                                        |
| [seccomp kernel docs](https://docs.kernel.org/userspace-api/seccomp_filter.html)     | Kernel docs            | Syscall filtering primitive.                                                                          |
| [AppArmor docs](https://apparmor.net/)                                               | LSM docs               | Mandatory access-control profiles for process confinement.                                            |
| [SELinux project](https://github.com/SELinuxProject)                                 | LSM project            | Mandatory access-control system; important conceptually for strong policy enforcement.                |
| [gVisor docs](https://gvisor.dev/docs/)                                              | Container sandbox docs | Userspace kernel that provides an additional isolation boundary for containers.                       |
| [gVisor GitHub](https://github.com/google/gvisor)                                    | Repo                   | Implementation of a sandboxed container runtime.                                                      |
| [gVisor architecture guide](https://gvisor.dev/docs/architecture_guide/)             | Architecture docs      | Explains how gVisor interposes between application and host kernel.                                   |
| [nsjail](https://github.com/google/nsjail)                                           | Process sandbox        | Linux namespaces, cgroups, seccomp-bpf, and resource limits in one tool.                              |
| [bubblewrap](https://github.com/containers/bubblewrap)                               | Unprivileged sandbox   | Commonly used by Flatpak; useful for lightweight local process isolation.                             |
| [Firejail](https://firejail.wordpress.com/)                                          | Linux sandbox          | SUID sandbox using namespaces and seccomp.                                                            |
| [Landlock LSM docs](https://docs.kernel.org/userspace-api/landlock.html)             | Kernel docs            | Unprivileged access-control mechanism for sandboxing.                                                 |
| [Sandlock paper](https://arxiv.org/abs/2605.26298)                                   | Paper                  | Confines AI agent code using unprivileged Linux primitives. Highly relevant to local-agent execution. |
| [Sandlock GitHub](https://github.com/multikernel/sandlock)                           | Repo                   | Companion implementation for the Sandlock paper.                                                      |

### Kubernetes and Cluster Execution

| Resource                                                                                                         | Type                | Why it matters                                                             |
| ---------------------------------------------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------------------- |
| [Kubernetes Pods](https://kubernetes.io/docs/concepts/workloads/pods/)                                           | Execution primitive | Smallest deployable unit in Kubernetes.                                    |
| [Kubernetes Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/)                                | Execution primitive | Useful for batch agent runs and retryable executions.                      |
| [Kubernetes Pod lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)                    | Lifecycle docs      | Useful for mapping agent run state to pod states.                          |
| [Kubernetes securityContext](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)         | Security docs       | Per-pod and per-container privilege, user, group, and capability settings. |
| [Kubernetes seccomp](https://kubernetes.io/docs/tutorials/security/seccomp/)                                     | Security docs       | Applying seccomp profiles to pods.                                         |
| [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)                   | Security docs       | Cluster-level pod security policy baseline.                                |
| [Kubernetes NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/network-policies/)            | Network policy      | Useful for sandbox egress control.                                         |
| [Kubernetes Resource Management](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/) | Resource limits     | CPU and memory quotas for sandbox runs.                                    |
| [Kueue](https://kueue.sigs.k8s.io/)                                                                              | Batch scheduler     | Useful for queued agent jobs and batch sandbox execution.                  |
| [Argo Workflows](https://argo-workflows.readthedocs.io/)                                                         | Workflow engine     | Kubernetes-native workflow execution; useful for multi-step sandbox jobs.  |

### Sandbox Security Papers and Measurement

| Resource                                                                                            | Type  | Why it matters                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [AI Code Sandboxes: Comparative Security Study](https://arxiv.org/abs/2606.08433)                   | Paper | Compares engine-level properties such as attack surface, leakage, stackability, CVE history, patch cadence, and fuzzing.                                       |
| [AI Sandboxes: Threat Model, Taxonomy, and Measurement Framework](https://arxiv.org/abs/2606.18532) | Paper | Gives a broad sandbox taxonomy and measurement framework for fidelity, controllability, observability, containment, reproducibility, and governance artifacts. |
| [Fault-Tolerant Sandboxing for AI Coding Agents](https://arxiv.org/abs/2512.12806)                  | Paper | Transactional sandboxing approach with policy interception and filesystem rollback.                                                                            |
| [ceLLMate: Sandboxing Browser AI Agents](https://arxiv.org/abs/2512.12594)                          | Paper | Browser-level sandboxing framework for reducing prompt-injection blast radius.                                                                                 |
| [AgentBay](https://arxiv.org/abs/2512.04367)                                                        | Paper | Hybrid interaction sandbox for agent and human takeover across Linux, Windows, Android, browser, and code-interpreter environments.                            |

### Sandbox Architecture Patterns

| Pattern                                              | Why it matters                                                                                                 |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Ephemeral compute, durable workspace**             | Sandbox lifetime should not define workspace lifetime.                                                         |
| **No host home mount by default**                    | Avoid leaking SSH keys, browser sessions, cloud credentials, and shell history.                                |
| **No Docker socket mount by default**                | Docker socket is usually equivalent to host root.                                                              |
| **Deny network by default for local code execution** | Many agent attacks rely on exfiltration or remote payload fetch.                                               |
| **Broker secrets outside the sandbox**               | Let the control plane perform privileged operations instead of exposing tokens.                                |
| **Snapshot before execution**                        | Enables rollback, diff, and audit.                                                                             |
| **Collect delta after execution**                    | Treat sandbox output as a candidate change, not a side effect.                                                 |
| **Per-run identity and quota**                       | Required for attribution, rate limiting, and abuse control.                                                    |
| **Separate browser sandbox from code sandbox**       | Browser agents face different risks: prompt injection, cookies, authenticated sessions, and web-origin policy. |
| **Policy as runtime guard**                          | The sandbox should enforce policy, not merely ask the model to follow instructions.                            |

## Security, Policy, and Governance

| Resource                                                                                                         | Type               | Why it matters                                                                |
| ---------------------------------------------------------------------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------- |
| [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) | Security checklist | Main LLM app threat categories.                                               |
| [OWASP Agentic AI Threats and Mitigations](https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/) | Security guidance  | Agent-specific threat model.                                                  |
| [Promptfoo docs](https://www.promptfoo.dev/docs/intro/)                                                          | Tool               | Practical eval and red-team framework.                                        |
| [Promptfoo OWASP Agentic AI docs](https://www.promptfoo.dev/docs/red-team/owasp-agentic-ai/)                     | Security eval      | Agentic application red-team presets.                                         |
| [Runtime Governance for Policy-Constrained Execution](https://arxiv.org/abs/2604.07833)                          | Paper              | Good argument for separating agent cognition from runtime policy enforcement. |
| [AgentWall: A Runtime Safety Layer for Local AI Agents](https://arxiv.org/abs/2605.16265)                        | Paper              | Runtime safety layer for local agents.                                        |
| [Security Engineering, Ross Anderson](https://www.cl.cam.ac.uk/archive/rja14/book.html)                          | Book               | Deep reference for security engineering, access control, and threat modeling. |
| MCP security best practices                                                                                      | Security docs      | Protocol-level security recommendations.                                      |
| MCP Safety Audit                                                                                                 | Paper              | Concrete MCP exploit cases.                                                   |

### Policy Patterns

| Pattern                        | Why it matters                                                                 |
| ------------------------------ | ------------------------------------------------------------------------------ |
| **Least-privilege tools**      | Tools should expose narrow actions, not broad shells.                          |
| **Workspace access grants**    | Short-lived scoped access to workspace paths and operations.                   |
| **Brokered secrets**           | Agents request operations; the platform uses secrets without exposing them.    |
| **Publish approval**           | Source-of-truth changes require explicit publish.                              |
| **Policy as transition guard** | Policy should protect state transitions, not only command execution.           |
| **Audit-first execution**      | Every action should be attributable and replayable.                            |

## Observability and Evaluation

| Resource                                                                                                            | Type                   | Why it matters                                         |
| ------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------------------------------------ |
| [OpenTelemetry](https://opentelemetry.io/)                                                                          | Observability standard | Vendor-neutral traces, metrics, and logs.              |
| [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)                                                 | Collector              | Standard telemetry pipeline.                           |
| [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/registry/attributes/gen-ai/) | Spec                   | Emerging schema for GenAI telemetry.                   |
| [OpenTelemetry GenAI semantic conventions repo](https://github.com/open-telemetry/semantic-conventions-genai)       | Repo                   | GenAI-specific conventions.                            |
| [Langfuse docs](https://langfuse.com/docs)                                                                          | OSS observability      | Open-source LLM tracing, eval, prompt management.      |
| [Langfuse GitHub](https://github.com/langfuse/langfuse)                                                             | Repo                   | Self-hostable observability platform.                  |
| [LangSmith observability](https://docs.langchain.com/langsmith/observability)                                       | Observability docs     | Good reference for full-stack LLM/agent observability. |
| [Promptfoo](https://github.com/promptfoo/promptfoo)                                                                 | Eval / red-team        | CLI and framework for LLM eval and red-teaming.        |
| [SWE-bench](https://www.swebench.com/)                                                                              | Benchmark              | Canonical benchmark for real GitHub issue resolution.  |
| [SWE-bench GitHub](https://github.com/swe-bench/SWE-bench)                                                          | Repo                   | Evaluation harness and datasets.                       |
| [SWE-agent experiments](https://github.com/swe-bench/experiments)                                                   | Eval logs              | Open predictions, logs, trajectories, and results.     |
| [AIDev: Studying AI Coding Agents on GitHub](https://arxiv.org/abs/2602.09185)                                      | Paper                  | Large-scale empirical study of real coding-agent PRs.  |

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

| Resource                                                                                                              | Type                   | Why it matters                                               |
| --------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------------------------------------------ |
| SWE-agent                                                                                                             | Agent scaffold         | Important baseline for issue-solving agents.                 |
| mini-SWE-agent                                                                                                        | Minimal implementation | Useful for understanding how small the loop can be.          |
| SWE-bench                                                                                                             | Benchmark              | Standard benchmark for GitHub issue resolution.              |
| AIDev                                                                                                                 | Paper                  | Real-world agent-authored PR study.                          |
| [OpenHands GitHub Action](https://docs.openhands.dev/openhands/usage/run-openhands/github-action)                     | Workflow docs          | Example of integrating a coding agent into GitHub workflows. |
| [OpenHands automated code review](https://docs.openhands.dev/openhands/usage/use-cases/code-review)                   | Workflow docs          | Coding-agent code review flow.                               |
| GitHub MCP Server                                                                                                     | MCP server             | Agent integration with GitHub issues, repos, and PRs.        |
| [GitHub Copilot: The agent awakens](https://github.blog/news-insights/product-news/github-copilot-the-agent-awakens/) | Product / workflow     | Useful view into mainstream coding-agent workflows.          |
| OpenAI Codex AGENTS.md example                                                                                        | Repo config            | Example context file for a coding-agent project.             |

## Data Layer and Storage

Agent infrastructure usually combines several storage concerns: control-plane records, conversation and run history, workspace state, artifacts, memory, and observability data. This section focuses on reusable storage ideas rather than generic application frameworks.

### Control-Plane Metadata

Agent definitions, identity, permissions, config, source references, and low-volume control-plane state usually fit normal OLTP systems well.

| Resource                                                                                   | Why it matters                                                                                      |
| ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| [PostgreSQL](https://www.postgresql.org/)                                                  | Strong default metadata store for identity, config, policy, workspace specs, and source references. |
| [PostgreSQL JSONB docs](https://www.postgresql.org/docs/current/datatype-json.html)        | Useful when specs and policy need typed relational fields plus flexible structured payloads.        |
| [PostgreSQL advisory locks](https://www.postgresql.org/docs/current/explicit-locking.html) | Practical primitive for workspace locks, publish locks, and idempotent control-plane operations.    |

### Conversation and Run History

Agent runs are easiest to debug and replay when prompts, model calls, tool calls, decisions, file changes, and checkpoints are recorded as ordered history. Some frameworks implement replay and branching at the framework layer; storage choices need to preserve the semantics those features depend on.

| Resource                                                                                                                                    | Why it matters                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| [LangGraph persistence and time travel](https://docs.langchain.com/oss/python/langgraph/persistence)                                        | Framework-level checkpointing, replay, and forking show concrete requirements for durable run history.    |
| [HumanLayer: Factor 12, Stateless Reducer](https://github.com/humanlayer/12-factor-agents/blob/main/content/factor-12-stateless-reducer.md) | Frames agent execution as deterministic reduction over persisted events.                                  |
| OpenRath: Session-Centered Runtime State for Agent Systems                                                                                  | Programming-model argument for treating sessions as first-class state rather than incidental transcripts. |
| [Claude Code commands: `/branch`](https://code.claude.com/docs/en/commands)                                                                 | Product example where branching a conversation/session is exposed as a native workflow.                   |

### Workspace and Artifact State

Coding agents and computer-use agents often need durable files, snapshots, forked workspaces, generated artifacts, and discardable candidate output. This is where storage design meets sandbox lifecycle.

| Resource                                                                         | Why it matters                                                                                                           |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| [Replit snapshot engine](https://replit.com/blog/inside-replits-snapshot-engine) | Shows a compute-and-storage fabric where filesystem state is durable and addressable independently of any one container. |
| [Cloudflare Sandboxes GA](https://blog.cloudflare.com/sandbox-ga/)               | Sandboxes are addressed by name, sleep at zero compute cost, and wake with state intact; only compute is disposable.     |
| BranchFS                                                                         | Copy-on-write branching filesystem aimed directly at fork/snapshot workspace semantics.                                  |
| Resilient Write                                                                  | Treats writes as a durable, auditable surface rather than invisible local side effects.                                  |

### Memory

Long-running agents may need memory beyond a single run. The important infrastructure questions are provenance, branching, compaction, retention, and whether memory is editable or only append-derived.

| Resource                                                                                                                                     | Why it matters                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [AWS Bedrock AgentCore Memory](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-agentcore-memory-building-context-aware-agents/) | Treats memory branching as a named capability for message edits, what-if exploration, and divergent context paths. |
| Anthropic: Building with Claude Managed Agents                                                                                               | Describes background memory consolidation for managed agents.                                                      |
| Letta                                                                                                                                        | Open-source platform centered on stateful agents and memory management.                                            |

### Observability and Analytics Storage

Trace-shaped analytical reads are a well-understood storage problem, but they have different needs than conversation replay or workspace state.

| Resource                                                                              | Why it matters                                                                                                 |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| OpenTelemetry                                                                         | Standard event, trace, metric, and log model for instrumenting agent runs.                                     |
| [ClickHouse](https://clickhouse.com/)                                                 | Common storage engine for high-volume analytical telemetry and trace-style reads.                              |
| [ClickHouse async inserts](https://clickhouse.com/docs/optimize/asynchronous-inserts) | Useful reference for the visibility and batching tradeoffs that come with high-throughput analytics ingestion. |
| Langfuse                                                                              | Self-hostable LLM observability stack backed by analytical storage patterns.                                   |

## Books

| Book                                                                                                                                         | Why it matters                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [Designing Data-Intensive Applications](https://dataintensive.net/)                                                                          | State, consistency, durability, lineage, logs, storage, and systems tradeoffs. |
| [Designing Data-Intensive Applications, O'Reilly](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781098119058/) | Publisher page.                                                                |
| [Google SRE Books](https://sre.google/books/)                                                                                                | Reliability, operations, incident response, SLOs, and production discipline.   |
| [Site Reliability Engineering table of contents](https://sre.google/sre-book/table-of-contents/)                                             | Free online SRE book.                                                          |
| Security Engineering                                                                                                                         | Security, access control, threat modeling, and system design.                  |
| [Operating Systems: Three Easy Pieces](https://pages.cs.wisc.edu/~remzi/OSTEP/)                                                              | Processes, virtualization, concurrency, persistence, and filesystems.          |
| [Distributed Systems, Maarten van Steen](https://www.distributed-systems.net/index.php/books/ds4/)                                           | Naming, replication, consistency, coordination, and fault tolerance.           |

## Videos and Talks

### MCP and Tool Protocol

| Video                                                                                                      | Why watch                               |
| ---------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| [The Model Context Protocol](https://www.youtube.com/watch?v=CQywdSdi5iA)                                  | Good MCP overview.                      |
| [Building Agents with Model Context Protocol - Full Workshop](https://www.youtube.com/watch?v=kQmXtrmQ5Zg) | Practical MCP workshop.                 |
| [MCP 201 - Code w/ Claude](https://www.youtube.com/watch?v=HNzH5Us1Rvg)                                    | More advanced MCP talk.                 |
| [Why we built-and donated-the Model Context Protocol](https://www.youtube.com/watch?v=PLyCki2K0Lg)         | Standardization and governance context. |
| [The Creators of Model Context Protocol](https://www.youtube.com/watch?v=m2VqaNKstGc)                      | Interview-style protocol background.    |

### Runtime and Durable Execution

| Video                                                                                           | Why watch                           |
| ----------------------------------------------------------------------------------------------- | ----------------------------------- |
| [LangGraph: Intro](https://www.youtube.com/watch?v=5h-JBkySK34)                                 | Intro to graph-based agent runtime. |
| [LangGraph Essentials](https://www.youtube.com/watch?v=B_BCeWhyD5Q)                             | Higher-level overview of LangGraph. |
| [LangGraph Crash Course](https://www.youtube.com/watch?v=uWLJAtMOVT0)                           | Practical walkthrough.              |
| [Durable AI Agents: LangGraph.js](https://www.youtube.com/watch?v=22Zv8VQ8PuI)                  | Durable execution in LangGraph.js.  |
| [Building Durable, Long-Running Autonomous Agents](https://www.youtube.com/watch?v=aYSl1hbuPfs) | Durable agent workflows.            |

### Sandbox Videos

| Video                                                                                               | Why watch                                        |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| [AWS re:Invent Firecracker talk](https://www.youtube.com/watch?v=yDplzXEdBTI)                       | Firecracker architecture and motivation.         |
| [Firecracker: Secure and Fast microVM](https://www.youtube.com/watch?v=PAEMGa-i2lU)                 | MicroVM isolation details.                       |
| [Face off: VMs vs Containers vs Firecracker](https://www.youtube.com/watch?v=pTQ_jVYhAoc)           | Isolation tradeoffs.                             |
| [How AWS's Firecracker virtual machines work](https://www.youtube.com/watch?v=BIRv2FnHJAg)          | Explainer on Firecracker.                        |
| [How AI Agents Execute Code](https://www.youtube.com/watch?v=5FCu6YqWA6U)                           | Runtime environment for AI code execution.       |
| [On Stream: AI Agents Running Containers with Daytona](https://www.youtube.com/watch?v=zsFMmv9ge4Y) | Practical AI-agent container runtime discussion. |
| [A cracking time: Exploring Firecracker & MicroVMs](https://www.youtube.com/watch?v=CYCsa5e2vqg)    | MicroVM concepts and demos.                      |
| [Firecracker/microVM support for Jenkins Slaves](https://www.youtube.com/watch?v=LSUVBGfzf3s)       | Example of CI-style microVM worker isolation.    |

### Observability Videos

| Video                                                                                                 | Why watch                             |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------- |
| [OpenTelemetry for GenAI and OpenLLMetry](https://www.youtube.com/watch?v=JnQXEMHh3aw)                | GenAI observability concepts.         |
| [How OpenTelemetry Helps Generative AI](https://www.youtube.com/watch?v=92oGRCC8ktA)                  | Practical OTel and GenAI framing.     |
| [Making GenAI Observable with OpenTelemetry](https://www.youtube.com/watch?v=RNaa_48LWBY)             | GenAI telemetry talk.                 |
| [How To Debug AI Agents: Tracing, Observability & Evals](https://www.youtube.com/watch?v=nWNWrtCDqaY) | Debugging agent systems.              |
| [Promptfoo Red Team Tutorial](https://www.youtube.com/watch?v=KghDstjwwNA)                            | Practical red-team and eval tutorial. |

### Coding Agents

| Video                                                                                                                    | Why watch                                   |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
| [Software Development Agents: What Works and What Doesn't](https://www.youtube.com/watch?v=o_hhkJtlbSs)                  | Practical OpenHands perspective.            |
| [OpenHands Community: Agent Control Plane](https://www.youtube.com/watch?v=20HNd4cb2vA)                                  | Agent control-plane discussion.             |
| [Dynamic Workflows using OpenHands SDK](https://www.youtube.com/watch?v=PtbrKTgj3X8)                                     | SDK workflow concepts.                      |
| [OpenAI Codex Tutorial: AGENTS.md](https://www.youtube.com/watch?v=NlNuoH5PPl4)                                          | Coding-agent repo guidance file usage.      |
| [Code w/ Claude Developer Conference playlist](https://www.youtube.com/playlist?list=PLf2m23nhTg1P5BsOHUOXyQz5RhfUSSVUi) | Claude Code, MCP, and agent workflow talks. |

### Chinese-language Supplements

| Resource                                                          | Why include                           |
| ----------------------------------------------------------------- | ------------------------------------- |
| [MCP 核心架构解析](https://www.bilibili.com/opus/1022254559229116469)   | Chinese overview of MCP architecture. |
| [\[中文字幕\] MCP 快速入门](https://www.bilibili.com/video/BV1pHdnYyE8v/) | Chinese MCP intro video.              |
| [MCP 作者详解 MCP 协议](https://www.bilibili.com/video/BV1NwQhYeES3/)   | Bilingual MCP explanation.            |

## Related Awesome Lists

| List                                                                                                  | Focus                                                         |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| [awesome-agentic-ai](https://github.com/mfornos/awesome-agentic-ai)                                   | Broad principles, standards, and technologies for agentic AI. |
| [awesome-production-agentic-systems](https://github.com/EthicalML/awesome-production-agentic-systems) | Production-oriented libraries and systems.                    |
| [awesome-harness-engineering](https://github.com/ai-boost/awesome-harness-engineering)                | Harness engineering, tools, evals, memory, MCP, permissions.  |
| [awesome-agents](https://github.com/kyrolabs/awesome-agents)                                          | General list of AI agents.                                    |
| [awesome-ai-agents](https://github.com/e2b-dev/awesome-ai-agents)                                     | General autonomous agent list.                                |
| [awesome-ai-sandboxes](https://github.com/tizkovatereza/awesome-ai-sandboxes)                         | AI sandbox providers and runtime environments.                |
| [awesome-agent-orchestration](https://github.com/vivy-yi/awesome-agent-orchestration)                 | Agent orchestration and multi-agent systems.                  |
| [awesome-ai-agent-papers](https://github.com/VoltAgent/awesome-ai-agent-papers)                       | Papers on AI agents.                                          |

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

- Git worktree docs
- Resilient Write
- BranchFS
- TClone

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

- Temporal durable execution
- Git apply
- GitHub Pull Requests

### Brokered Secrets

Agents should not receive long-lived provider credentials by default.

```text
agent produces candidate output
platform reviews and approves
publish broker uses secret from vault
agent never sees raw token
```

Useful resources:

- MCP security best practices
- Security Engineering
- OWASP Agentic AI threats

### Runtime Governance

Policy should be outside the model loop.

```text
model proposes action
runtime checks policy
tool executes only if approved
event is recorded
```

Useful resources:

- Runtime Governance for Policy-Constrained Execution
- MCP Safety Audit
- Promptfoo

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

- AGENTS.md
- Evaluating AGENTS.md
- Configuring Agentic AI Coding Tools

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

- OpenTelemetry
- OpenTelemetry GenAI semantic conventions
- Langfuse
- LangSmith observability

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
