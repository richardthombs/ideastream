---
stepsCompleted: [1, 2, 3, 4]
inputDocuments: []
workflowType: 'research'
lastStep: 4
research_type: 'technical'
research_topic: 'beads-dolt-llm-invocation-options'
research_goals: 'Assess Steve Yegge\'s Beads project and Dolt capabilities, and determine practical options for invoking LLMs in this environment, including GitHub Copilot-style tooling versus direct API-based model or agent access.'
user_name: 'Richard'
date: '2026-03-08'
web_research_enabled: true
source_verification: true
---

# Research Report: technical

**Date:** 2026-03-08
**Author:** Richard
**Research Type:** technical

---

## Research Overview

This report evaluates three related technical questions:

1. What Beads is, specifically Steve Yegge's GitHub project, and what it is capable of.
2. What Dolt is and what capabilities it brings as the storage and versioning substrate underneath Beads, and under what circumstances it might also be useful separately.
3. How LLMs can be invoked in this environment, including whether the practical path is editor-mediated tooling such as GitHub Copilot, or direct programmatic access through an API.

Methodology:

- Current public documentation and repository metadata were checked live on 2026-03-08.
- Claims were cross-checked across upstream READMEs, vendor documentation, and repository metadata where possible.

---

## Technical Research Scope Confirmation

**Research Topic:** beads-dolt-llm-invocation-options
**Research Goals:** Assess Steve Yegge's Beads project and Dolt capabilities, and determine practical options for invoking LLMs in this environment, including GitHub Copilot-style tooling versus direct API-based model or agent access.

**Technical Research Scope:**

- Architecture Analysis - design patterns, frameworks, system architecture
- Implementation Approaches - development methodologies, coding patterns
- Technology Stack - languages, frameworks, tools, platforms
- Integration Patterns - APIs, protocols, interoperability
- Performance Considerations - scalability, optimization, patterns

**Research Methodology:**

- Current web data with rigorous source verification
- Multi-source validation for critical technical claims
- Confidence level framework for uncertain information
- Comprehensive technical coverage with architecture-specific insights

**Scope Confirmed:** 2026-03-08

## Technology Stack Analysis

### Programming Languages

The two core technologies under review are both strongly Go-centric. Beads is published as a Go-based project and its current GitHub language breakdown is dominated by Go, with smaller Python, Shell, JavaScript, and TypeScript components. That fits the product shape described in its README: a cross-platform CLI with surrounding tooling, install scripts, and MCP integration support. Dolt is likewise primarily a Go codebase, but with a broader supporting language footprint driven by packaging, tests, client examples, and platform tooling. This matters because both projects are operationally aligned with local binaries and CLI-first workflows rather than browser-only or hosted-SaaS-only usage.

For LLM invocation, the relevant distinction is between interactive agent surfaces and direct model APIs. GitHub Copilot and MCP-based tooling represent agent-facing and operator-facing interaction patterns, while GitHub Models represents direct programmable model access for application-side inference.

_Popular Languages:_ Beads: Go first, with Python and Shell support tooling. Dolt: Go first, with substantial shell tooling and smaller multi-language support surface. For direct LLM integration, GitHub Models provides language-specific generated examples and a REST path.
_Emerging Languages:_ No evidence from the upstream repositories suggests a migration away from Go for either Beads or Dolt; the surrounding ecosystem is instead expanding through protocol and tooling layers such as MCP, REST, and SDK generation.
_Language Evolution:_ Beads is new and moving quickly, but its packaging strategy already spans Homebrew, npm, Go install, and Python-based MCP tooling. Dolt is more mature and stable in its Go-first server-plus-CLI structure.
_Performance Characteristics:_ Go is a good fit for both tools because they need efficient local execution, concurrency, and straightforward cross-platform binary distribution. That is materially more suitable than scripting-only implementations for a local issue graph engine and a database with version-control semantics.
_Source: https://api.github.com/repos/steveyegge/beads_
_Source: https://api.github.com/repos/steveyegge/beads/languages_
_Source: https://api.github.com/repos/dolthub/dolt_
_Source: https://api.github.com/repos/dolthub/dolt/languages_
_Source: https://github.com/steveyegge/beads_

### Development Frameworks and Libraries

Beads is not positioned as a general application framework. It is a task-memory and issue-graph system built around a CLI called `bd`, backed by Dolt, and extended into coding-agent environments through an MCP server called `beads-mcp`. Its integration guide for GitHub Copilot shows a practical framework stack of `bd` plus `beads-mcp` plus VS Code MCP configuration. That makes its main capability less about UI composition and more about structured task state, dependency tracking, claiming, closure, sync, and agent-facing tooling.

Dolt is similarly framework-adjacent rather than framework-centric. Its main interfaces are a Git-like CLI, SQL primitives, and a MySQL-compatible server. The most relevant associated platform pieces are DoltHub for hosted collaboration, DoltLab for self-hosting, and Doltgres for teams that prefer Postgres semantics. In other words, Dolt acts as a foundational data substrate that other systems can build on, rather than a conventional web framework.

For LLM usage, the practical framework options split into two categories. The first is editor-mediated interaction, where GitHub Copilot in VS Code consumes project instructions and optionally MCP tools such as Beads. The second is direct model access, where GitHub Models exposes generated example code, a REST API, and Azure AI Inference SDK compatibility for application-side integration.

_Major Frameworks:_ Beads stack: `bd` CLI plus `beads-mcp` via MCP. Dolt stack: `dolt` CLI plus `dolt sql-server`, with DoltHub/DoltLab as operational extensions. LLM stack options: GitHub Copilot inside the IDE, or GitHub Models via REST/SDK.
_Micro-frameworks:_ Beads' MCP server is the lightweight integration layer for agent tooling; it does not require embedding a large server platform into an application. Dolt can also be used locally as a single binary rather than a distributed service mesh.
_Evolution Trends:_ Beads explicitly documents Copilot integration and positions MCP as a first-class mechanism for natural-language tool invocation. GitHub Models is also converging on a playground-plus-code-generation approach so experimentation can move into direct API use with fewer translation steps.
_Ecosystem Maturity:_ Dolt is the more mature platform with a longer operating history and hosted variants. Beads is much newer, but it is clearly already building ecosystem surface area through CLI packaging, MCP, and community tools.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Database and Storage Technologies

This is the clearest technical relationship in the set: Beads is explicitly Dolt-powered. Beads describes itself as a distributed, git-backed graph issue tracker for AI agents, and its README calls out Dolt-powered version-controlled SQL storage with cell-level merge, native branching, and built-in sync via Dolt remotes. That means Beads is not inventing its own storage engine; it is leveraging Dolt as the durable state layer for issue graphs, task history, and multi-branch collaboration.

Dolt itself is a SQL database that versions tables the way Git versions files. It exposes version-control semantics in both CLI and SQL forms, including branching, merging, commit history, remotes, and conflict tooling. It also ships with a MySQL-compatible server, which means it can participate as a normal database from application code while still preserving commit-oriented history and branchable data state. In the context of this research, however, those capabilities matter first because they explain what Beads can inherit, not because they automatically imply a need for direct Dolt integration.

For LLM invocation, there is no single storage technology implied by the model API itself. If direct API-based invocation is paired with agent workflows, prompt storage, evaluation baselines, and agent state could plausibly be kept either in repository files or in a structured store such as Dolt depending on whether versioned operational state becomes a requirement.

_Relational Databases:_ Dolt is the dominant relational technology in scope here, primarily because it underpins Beads while still leaving open the option of separate direct use if a broader versioned-data requirement emerges.
_NoSQL Databases:_ No NoSQL system is core to the reviewed stack. Beads solves graph-like issue relationships on top of versioned SQL rather than by adopting a native graph database.
_In-Memory Databases:_ No upstream source positions Redis-like systems as central to either Beads or Dolt.
_Data Warehousing:_ Not a primary concern in the current scope, though Dolt's branching and history capabilities can support analytical workflows where dataset evolution matters.
_Source: https://github.com/steveyegge/beads_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://github.com/dolthub/dolt_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_

### Development Tools and Platforms

Beads is very clearly a toolchain product. It is installed system-wide rather than cloned into each repository, and then initialised per project with `bd init`. The supported installation routes are Homebrew, npm, and `go install`, while the MCP server is distributed separately through `uv`, `pip`, or `pipx`. In practice, that means Beads fits teams already comfortable with CLI tools and editor integrations rather than teams expecting a managed control plane out of the box.

Dolt is also strongly tool-oriented. It ships as a standalone binary, supports Homebrew and Docker, and can run either as a CLI-driven local repository or a MySQL-compatible SQL server. That gives it a broader operational envelope than a library dependency, because it can serve both developer workstations and hosted/shared environments. For present purposes, though, that broader envelope is best treated as background capability rather than an immediate integration recommendation.

At the platform level, the important distinction is that Beads and Dolt are both tool-oriented rather than library-first products. Beads is consumed through CLI and MCP surfaces. Dolt is consumed through CLI, SQL server, and SQL-native version-control primitives. GitHub Models, by contrast, is consumed through playground and API surfaces.

_IDE and Editors:_ Beads adds optional VS Code MCP integration. GitHub Models also supports experimentation through Visual Studio Code via the AI Toolkit extension.
_Version Control:_ Git remains the project content layer, while Beads provides structured operational state and Dolt supplies the versioned database layer underneath it.
_Build Systems:_ Beads and Dolt both rely on standard CLI installation and local binary execution. GitHub Models is accessed through generated code, REST, or SDK-based integration rather than through a dedicated build system.
_Testing Frameworks:_ GitHub Models offers playground and evaluation capabilities for model comparison and prompt testing, while agent execution validation still needs to be handled by the surrounding toolchain or application.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Cloud Infrastructure and Deployment

Beads is primarily a local and repository-adjacent tool. Its deployment model is lightweight: install the CLI once, initialise per project, optionally connect an MCP server in the editor, and sync issue data through Dolt remotes. That is materially different from a centralised SaaS orchestration product. It reduces adoption friction, but it also means operational guarantees depend on how well the team manages local installs, sync policies, and conventions.

Dolt supports a wider range of deployment shapes. It can run as a local binary, as a MySQL-compatible server, in Docker images, or through hosted offerings such as DoltHub and Hosted Dolt, with DoltLab available for self-hosted collaboration. That makes Dolt viable both as a developer workstation technology and as a shared data platform.

For LLM invocation, GitHub Models supports browser-based playground experimentation, Visual Studio Code experimentation through the AI Toolkit extension, and API-based use in local or hosted applications. The documentation explicitly states that local use can be done with a GitHub personal access token carrying `models:read`, and that models can be called either through generated code, the Azure AI Inference SDK, or direct REST requests. GitHub also positions paid GitHub Models and BYOK as the production path once free experimentation limits are insufficient.

_Major Cloud Providers:_ The direct evidence in scope points most strongly to GitHub Models on top of Azure-managed inference infrastructure.
_Container Technologies:_ Dolt publishes official Docker images. Beads itself is primarily distributed as a CLI and MCP tool rather than as a container-first platform.
_Serverless Platforms:_ No primary evidence suggests serverless is the default path for these tools, though direct LLM API calls could be embedded in serverless applications later.
_CDN and Edge Computing:_ Not central to the current scope.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Technology Adoption Trends

The adoption pattern here is notable. Dolt is an established project created in 2019 with a large star base and a relatively mature hosted ecosystem. Beads is much newer, created in late 2025, but it already shows strong early adoption and is explicitly targeted at the coding-agent workflow space. That suggests a trend toward treating agent work as durable, branchable operational state rather than disposable chat history, with Dolt often serving as enabling infrastructure rather than the primary interface teams adopt first.

The LLM invocation trend is also bifurcating. Interactive work is moving toward editor-integrated and MCP-mediated experiences because they reduce friction for humans and let tools be invoked by natural language. Production-grade integration, however, still points toward direct API access, where authentication, rate limits, observability, and deterministic control are easier to manage. In other words: Copilot-style interaction is a strong operator interface, but it is not a substitute for an application integration boundary when you need a system to call models on demand.

The strategic takeaway is that these capabilities naturally separate into operator-facing interaction and application-facing invocation. Interactive work is trending toward editor-integrated and MCP-mediated experiences, while reproducible programmatic invocation continues to favour direct API access.

_Migration Patterns:_ A move from human-in-the-loop editor workflows to direct API invocation is typically additive, not a replacement for development-time agent tooling.
_Emerging Technologies:_ MCP-backed tool invocation and structured agent memory systems such as Beads are growing quickly around coding-agent workflows.
_Legacy Technology:_ Plain markdown task plans are being displaced by more structured state tools in agent-heavy workflows; Beads explicitly positions itself against that pattern.
_Community Trends:_ Both Beads and Dolt show active maintenance and strong public interest. GitHub Models is also pushing experimentation-to-production paths directly inside the GitHub ecosystem.
_Source: https://api.github.com/repos/steveyegge/beads_
_Source: https://api.github.com/repos/dolthub/dolt_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

## Integration Patterns Analysis

### Interface Boundaries and Integration Surfaces

The three technologies in scope expose very different integration boundaries, and that difference is the main architectural takeaway. Beads is primarily a local tool integration. Its first-class surfaces are the `bd` CLI and the `beads-mcp` MCP server, which allows an editor agent such as GitHub Copilot Chat to call Beads operations through natural-language workflows. Dolt is primarily a data-system integration. Its surfaces are the `dolt` CLI, a MySQL-compatible SQL server, and SQL-native version-control procedures and functions. GitHub Models is primarily an application integration. Its surfaces are a hosted playground for experimentation plus direct API access through REST or the Azure AI Inference SDK.

That means these tools sit at different layers rather than competing directly. Beads is best understood as the primary operator-facing workflow and memory layer. Dolt is the structured persistence and branchable state layer underneath Beads. GitHub Models is the inference layer when code needs to call models directly. In practical terms, a human or coding agent can use Copilot plus MCP to manipulate Beads, Beads can persist its structured state in Dolt, and application code can separately call GitHub Models when runtime model inference is needed.

_Primary Interfaces:_ Beads: CLI and MCP tools. Dolt: underlying CLI, MySQL wire-compatible server, and SQL procedures/functions. GitHub Models: playground, generated code samples, REST, Azure AI Inference SDK.
_Boundary Type:_ Beads integrates into the developer workflow; Dolt primarily integrates as Beads' persistence substrate unless a separate data need justifies direct use; GitHub Models integrates into application-side inference.
_Interoperability Implication:_ These tools compose cleanly if Beads remains the main operational interface, Dolt remains behind it by default, and direct Dolt usage is introduced only for clearly separate requirements.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.dolthub.com/sql-reference/version-control/branches_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Beads Integration Patterns

Beads currently supports two practical integration modes. The first is direct terminal usage through the `bd` CLI. This is the lower-friction path for scripts, deterministic task manipulation, bulk operations, and workflows where precise command semantics matter. The second is MCP-based tool access from Copilot Chat. In that mode, VS Code reads `.vscode/mcp.json` or user-level MCP config, loads `beads-mcp`, and exposes a set of tools such as `beads_ready`, `beads_create`, `beads_show`, `beads_update`, `beads_close`, and `beads_dolt_push`.

The important distinction is that MCP does not turn Beads into a general-purpose application API. It turns Beads into an editor-available tool surface for humans and coding agents. It is a strong fit for project operations such as finding ready work, creating or closing tasks, checking dependencies, and keeping structured issue state in sync. It is not the right abstraction if a deployed service needs to call into task memory during runtime. For that case, a system would either need to shell out deliberately to the CLI in a controlled environment or interact with the underlying data layer more directly.

The Beads docs explicitly recommend using both modes together: MCP for conversational discovery and workflow assistance, CLI for scripting, speed, and precision.

_API Shape:_ Tool-style RPC via MCP, plus local CLI commands.
_Protocol Layer:_ MCP between Copilot and Beads, shell process invocation for CLI usage.
_Best Fit:_ Human-in-the-loop development workflows, coding-agent memory, structured issue management.
_Constraint:_ No evidence of a stable general-purpose HTTP or embedded library API intended for application runtime integration.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_

### Dolt Integration Patterns

Dolt exposes a rich interoperability surface because it can be used both as a local version-control-aware database and as a conventional SQL server. At the lowest level, teams can use the `dolt` CLI with Git-like commands such as clone, branch, checkout, merge, push, and pull. At the application level, Dolt can be started with `dolt sql-server` and then accessed by standard MySQL clients and drivers. At the SQL layer, version-control features are available through database revision specifiers, stored procedures, functions, and system tables.

The branch integration model is especially relevant. Dolt allows clients to connect to a particular branch or revision using connection strings such as `mysql://127.0.0.1:3306/mydb/feature-branch`, and it supports switching heads inside SQL sessions with `USE` statements or procedures such as `DOLT_CHECKOUT()`. It also supports fully-qualified cross-branch references in SQL. This is materially more powerful than a standard relational database when the product needs isolated experimental data states, auditability, or branch-per-feature data workflows.

In this document, the default interpretation should be that Dolt remains an implementation detail underneath Beads, where Beads owns the schema and task operations and all routine interaction happens through the Beads CLI. Direct Dolt usage only becomes compelling if a separate requirement emerges, such as versioned prompt libraries, evaluation datasets, agent memory snapshots, or other branchable operational state not naturally owned by Beads.

_API Shape:_ CLI commands, MySQL-compatible SQL access, SQL procedures/functions/system tables.
_Protocol Layer:_ MySQL wire protocol plus local command execution.
_Best Fit:_ Structured state that benefits from branching, merging, history inspection, and reproducible data revisions, especially when Beads is not already the more appropriate interface.
_Constraint:_ Multi-branch transactional semantics are intentionally restricted; Dolt will not commit transactions that modify more than one branch at a time.
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.dolthub.com/introduction/what-is-dolt_
_Source: https://docs.dolthub.com/sql-reference/version-control/branches_

### Direct LLM Invocation Patterns

The clearest answer to the user's LLM question is that GitHub Copilot and GitHub Models serve different purposes. Copilot is an interactive development and agent surface. Current GitHub documentation describes Copilot coding agent as an autonomous system that works in the background, uses an ephemeral GitHub Actions-powered environment, can explore code, make changes, and execute automated tests and linters before opening a pull request for review. GitHub also documents MCP as the mechanism for extending Copilot with external tools and data sources. GitHub Models, by contrast, is explicitly documented as an API-accessible model platform for experimentation and application-side inference. GitHub's documentation states that free experimentation can be done via the playground and via direct API usage, and that local API calls require a personal access token with `models:read` scope.

GitHub Models also documents two direct integration styles. One is raw REST, where the model is called through the GitHub Models REST API endpoint. The other is SDK-based, where the Azure AI Inference SDK can be used across all models, and some models additionally support other SDKs. GitHub's playground can generate example code for the selected language and SDK, which lowers the cost of moving from experiment to implementation. Once usage needs exceed the free preview limits, GitHub positions either paid GitHub Models or BYOK as the production path.

The crucial limitation is that GitHub Models gives you inference, not a complete agent runtime. Its documented surface is model selection, playground evaluation, REST calls, and SDK-based requests. It does not by itself provide the higher-level control loop needed to inspect a repository, choose tools, modify files, run shell commands, execute tests, and iteratively recover from failures. Those agent capabilities live elsewhere: in Copilot coding agent, IDE agent mode, MCP-enabled tool ecosystems, or a custom agent application built around direct model APIs.

From an architecture standpoint, this is the practical dividing line: if a product needs deterministic, code-driven model invocation, it should use GitHub Models or another explicit provider API, but it should not mistake that for a full autonomous agent substrate. If it needs task execution with tool use, file mutation, and validation loops, it needs either a GitHub-hosted agent surface such as Copilot coding agent, an IDE-local agent workflow with MCP tools, or a custom orchestration layer built around direct model APIs. Trying to automate Copilot chat itself would still be the wrong abstraction because it couples runtime behaviour to an interactive tool surface instead of a stable application boundary.

_API Shape:_ Direct REST requests or Azure AI Inference SDK calls, authenticated by GitHub token.
_Protocol Layer:_ HTTPS API calls rather than editor mediation.
_Best Fit:_ Application runtime inference, evaluation pipelines, controlled programmatic model access.
_Constraint:_ Free usage is preview-rate-limited, and the platform provides inference rather than end-to-end agent execution.
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_
_Source: https://docs.github.com/en/rest/models?apiVersion=2022-11-28_
_Source: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent_
_Source: https://docs.github.com/en/copilot/concepts/context/mcp_

### Practical Integration Options

There are four credible composition patterns for teams evaluating these technologies.

Pattern 1 is a development-workflow pattern: keep Copilot as the human and agent interface, optionally add Beads via MCP for persistent structured work tracking, and leave direct model invocation outside the application boundary.

Pattern 2 is an operational-memory pattern: add Beads plus its MCP integration for development workflows, let Beads continue to use Dolt under the hood, and keep model invocation separate. This gives a team durable, branchable work state without prematurely committing application code to a specific inference provider or introducing direct Dolt integration unnecessarily.

Pattern 3 is a full application-integration pattern: keep Copilot and optionally Beads for development, but add a dedicated service or library layer that calls GitHub Models directly through REST or the Azure AI Inference SDK. This is the cleanest path if the product itself needs to invoke LLMs for inference. In that design, Copilot remains a developer tool, Beads remains an optional structured memory tool, and GitHub Models becomes the application inference dependency.

Pattern 4 is an explicit custom-agent pattern: keep direct model access for inference, but add an orchestration layer that owns planning, tool selection, file mutations, command execution, state persistence, and validation. In that model, Beads can provide structured operational memory, the chosen model API provides reasoning and generation, and Dolt remains behind Beads unless a distinct non-Beads requirement justifies direct adoption. This is the only pattern in the set that directly addresses the user's concern that task execution requires more than inference alone.

Pattern 1 is the lowest-friction option when the primary need is human-in-the-loop development support. Pattern 2 is the natural extension when structured, branchable work memory becomes valuable. Pattern 3 is the right move when runtime inference becomes a product requirement, but it should be understood as inference plumbing rather than agent execution. Pattern 4 is the correct architectural direction when a team needs its own autonomous task-executing agent rather than just model calls. Across all four patterns, direct Dolt integration should be treated as optional and justified by a separate need rather than assumed from the outset.

_Recommended Near-Term Integration:_ Copilot plus optional Beads MCP for development operations, with Beads CLI as the main operational interface.
_Recommended Product Integration Path:_ GitHub Models direct API or SDK if a product needs programmatic inference, with a separate orchestration layer if it needs agentic execution.
_Architectural Warning:_ Do not treat Copilot chat as a substitute for a runtime model API, do not treat a model inference API as a substitute for an agent runtime, and do not promote Dolt to a first-class interface unless it is solving a distinct need beyond Beads.
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_
_Source: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent_
_Source: https://docs.github.com/en/copilot/concepts/context/mcp_

## Architectural Patterns and Design

### System Architecture Patterns

The strongest architectural pattern in this stack is layered separation rather than a single unified platform. Beads should be treated as the primary workflow and memory layer, exposed through the `bd` CLI and optionally through MCP for conversational access. Dolt sits underneath that layer as the storage and versioning engine. GitHub Models sits beside that stack as an inference service rather than inside it. That produces a clean architecture with three distinct concerns: operator interaction, durable structured state, and model execution.

The practical implication is that Beads should own the operational contract for issue state, dependency tracking, and long-horizon task memory. Dolt should not normally leak upward into everyday workflows; it is the persistence mechanism that gives Beads branching, mergeability, and sync semantics. Direct model APIs should remain outside the Beads/Dolt boundary, because inference and task-memory persistence are separate responsibilities with different scaling, security, and observability concerns.

From an architectural style perspective, this favours a tools-plus-services composition over a monolith. The CLI acts as the explicit command boundary. MCP acts as an optional natural-language tool invocation boundary. Direct model APIs act as application-side service dependencies. That is a more defensible design than trying to make one layer do everything.

_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Design Principles and Best Practices

The main design principle is interface discipline. If Beads is adopted, all normal operational interactions should go through the Beads CLI, because that preserves one authoritative behavioural surface for creating, updating, linking, claiming, and closing work. Treating Dolt as a direct peer interface too early would split responsibility across two abstractions and make the operational model harder to reason about.

The second principle is separation of inference from orchestration. GitHub Models gives a product a model-calling boundary, but it does not provide the complete architecture for autonomous work execution. If autonomous execution is required, the control loop must live in a separate orchestration layer that decides when to call models, when to use tools, when to mutate files, and how to validate outcomes.

The third principle is explicit human oversight at the edges of autonomy. GitHub's coding-agent architecture reinforces this by placing autonomous execution in a constrained environment, surfacing results through pull requests, and requiring review. Even if a team does not use Copilot coding agent directly, the pattern is useful: autonomous work should be observable, reviewable, and bounded.

_Source: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://docs.github.com/en/copilot/concepts/context/mcp_

### Scalability and Performance Patterns

The architecture is naturally scalable because the layers scale differently. Beads scales primarily as an operational coordination tool: issue graphs, dependency management, and structured task memory grow with team and project complexity. Dolt scales as a branchable data substrate, which is valuable when state evolution, diffability, and merge semantics matter more than raw high-throughput transactional workload. GitHub Models scales independently as an inference endpoint with its own quota and billing model.

This separation matters for performance. The CLI-first Beads model keeps the task-management surface lightweight and local. MCP adds convenience, but with more token and protocol overhead than direct CLI use. Direct model invocation should therefore be reserved for actual reasoning or generation tasks, not for basic task-state manipulation that the Beads CLI already handles deterministically.

The main performance pattern, then, is to keep deterministic state transitions on the Beads side and probabilistic reasoning on the model side. That reduces unnecessary inference calls, improves repeatability, and avoids turning the model into a mediator for operations that already have an exact tool interface.

_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Integration and Communication Patterns

The communication architecture should be boundary-specific. Human or agent requests that manipulate work state should flow through the Beads CLI or Beads MCP tools. Model inference requests should flow through HTTPS calls to GitHub Models or another provider API. Those boundaries should not be collapsed unless there is a strong reason to do so.

For agentic systems, this supports a hub-and-spoke pattern. The orchestrator or agent runtime becomes the hub. Beads CLI is one spoke for structured work-state operations. The model API is another spoke for reasoning and generation. Optional additional tools can be attached through MCP or direct process execution. Dolt remains below the Beads spoke by default rather than becoming an equal spoke itself.

This pattern keeps failure domains cleaner. If inference fails, task state remains intact. If Beads operations fail, the model layer is unaffected. If Dolt-level concerns arise, they can usually be handled within the Beads operational boundary rather than infecting the higher-level agent interface.

_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://docs.github.com/en/copilot/concepts/context/mcp_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_

### Security Architecture Patterns

The relevant security pattern is constrained autonomy. GitHub's coding agent documentation is useful here because it shows a production-grade agent design that constrains execution environment, network reach, branch permissions, and review flow. That is the right mindset for any system that combines model reasoning with code or file mutation.

For a Beads-centric architecture, the safest default is to keep Beads interactions explicit and tool-driven, not inferred indirectly through free-form model behaviour. The CLI gives deterministic operations and auditability. MCP can still be used, but only as a tool invocation mechanism layered over explicit operations. Direct model APIs should remain limited to reasoning and generation unless wrapped in orchestration logic with validation and approval boundaries.

If a team later introduces direct Dolt usage for a separate need, that should be treated as a new security surface, with its own access, schema, remote-sync, and governance considerations, rather than as a transparent extension of Beads.

_Source: https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_

### Data Architecture Patterns

The preferred data architecture is layered ownership. Beads owns the operational schema and lifecycle for issue graphs, dependencies, status transitions, audit trails, and related task-memory constructs. Dolt owns the storage mechanics that make those records versionable, mergeable, and synchronisable. That keeps the conceptual model clean: users and agents think in Beads terms, not Dolt tables.

This design also preserves future optionality. If a separate need emerges for versioned datasets, evaluation records, or branchable prompt assets that are not naturally part of the Beads issue graph, Dolt could then be introduced as a direct data architecture component in its own right. But that should be a deliberate expansion of scope, not the default starting point.

The architectural rule is therefore simple: use Beads' data model for work memory, and only surface Dolt directly when the problem is no longer fundamentally a Beads problem.

_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_
_Source: https://docs.dolthub.com/sql-reference/version-control/branches_

### Deployment and Operations Architecture

Operationally, the architecture is well suited to incremental adoption. Beads is installed as a system-wide CLI, initialised per project, and optionally connected to editor tooling through MCP. That makes it easy to adopt as a team workflow layer without committing immediately to a larger application architecture change. GitHub Models can likewise be introduced independently when there is a concrete need for direct inference calls.

This supports a staged operating model. Stage one is CLI-first Beads adoption, with optional MCP for conversational workflows. Stage two is adding direct model inference only where the product genuinely needs it. Stage three, if required, is adding a custom orchestration layer for agentic execution. At each stage, Dolt can remain behind Beads unless a distinct direct data requirement appears.

That staged architecture is preferable to premature consolidation. It keeps the operational contract clear, the adoption path reversible, and the system easier to evolve without overcommitting to direct database integration or overloading the model layer with responsibilities it should not own.

_Source: https://raw.githubusercontent.com/steveyegge/beads/main/README.md_
_Source: https://raw.githubusercontent.com/steveyegge/beads/main/docs/COPILOT_INTEGRATION.md_
_Source: https://docs.github.com/en/github-models/use-github-models/prototyping-with-ai-models_
_Source: https://raw.githubusercontent.com/dolthub/dolt/main/README.md_