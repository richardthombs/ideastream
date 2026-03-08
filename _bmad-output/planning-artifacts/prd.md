---
stepsCompleted:
  - step-01-init
  - step-02-discovery
  - step-02b-vision
  - step-02c-executive-summary
  - step-03-success
  - step-04-journeys
  - step-05-domain
  - step-06-innovation
  - step-07-project-type
  - step-08-scoping
  - step-09-functional
  - step-10-nonfunctional
  - step-11-polish
  - step-12-complete
inputDocuments:
  - _bmad-output/brainstorming/brainstorming-session-2026-03-07-171041.md
  - _bmad-output/planning-artifacts/research/technical-beads-dolt-llm-invocation-options-research-2026-03-08.md
workflowType: 'prd'
documentCounts:
  productBriefs: 0
  research: 1
  brainstorming: 1
  projectDocs: 0
  projectContext: 0
classification:
  projectType: developer_tool
  domain: general
  complexity: medium
  projectContext: greenfield
---

# Product Requirements Document - ideastream

**Author:** Richard
**Date:** 2026-03-08

## Executive Summary

Ideastream is a developer-focused productivity tool for individuals working across multiple projects, especially where some work may be executed through agentic workflows. Its core purpose is to help users remain organised as they switch between projects, track what has been done and what still needs attention, and ensure that to-dos are captured in the correct project context rather than becoming disconnected fragments of intent.

The product is designed to bridge a gap that existing tools tend to leave open. Traditional to-do and project management tools help users organise intent, while agentic systems help execute work, but neither category handles the full problem of staying in control while work is being dispatched across multiple projects with frequent context changes. Ideastream combines those concerns into one operating model: project-scoped organisation first, agentic execution second.

The initial value proposition is deliberately broad in accessibility. A user can adopt Ideastream purely as a project and to-do organisation system without using any agentic execution at all. As their confidence and needs grow, the same tool can be used to trigger workflows that act on that organised work, preserving continuity between planning, oversight, and execution.

### What Makes This Special

What makes Ideastream distinctive is its focus on high-level dispatch between projects rather than on isolated task capture or isolated agent interaction. The product treats organisation and execution as connected but separate layers: users first need confidence that work is correctly scoped, visible, and not being forgotten; only then does agentic execution become genuinely useful.

The key differentiator is the user experience of creating a new to-do and seeing it actioned correctly in the right project context, with an outcome that feels genuinely helpful rather than merely automated. That moment demonstrates that the system is not just storing tasks or exposing agents, but reliably converting organised intent into satisfying progress.

The core insight behind the product is that agentic workflows increase productivity while also increasing fragmentation. As users work across more projects and trigger more delegated work, the cognitive burden of context switching rises sharply. Ideastream is worth building because it reduces that burden: it provides a coherent view of multi-project work, preserves project context, and offers a gradual path from simple organisation to delegated execution.

## Project Classification

This product is currently classified as a greenfield developer tool in the general software domain with medium complexity. The complexity comes less from regulatory or compliance concerns and more from the need to combine project organisation, context management, and agentic workflow dispatch into a single coherent user experience.

## Success Criteria

### User Success

The product succeeds for its primary user when it makes day-to-day work meaningfully more productive across multiple active projects. That means the user completes more tasks, spends less time deciding what to do next, and can move from idea to action with less friction than in their current workflow.

A successful user experience also requires sustained organisational confidence. The user should be able to see clearly what is waiting to be done, what has already been completed, and what is currently being acted on, without feeling that important work is being lost between projects or buried by context switching.

The strongest success moment is when a user creates a to-do in free text, sees it assigned to the correct project, and then sees it progress through planning and execution in a way that feels trustworthy and useful rather than merely automated.

### Business Success

This product is not being developed as a revenue-driven SaaS offering, so business success is defined in terms of real adoption, retained usefulness, and practical value to its users.

Within one month, the primary success target is that the creator can use the product in real work rather than as a demonstration or experiment. Within three months, success includes at least one additional real user adopting it for their own workflow. Within twelve months, success means the product remains in active use by the creator and has evolved from a pet project into an essential part of daily life and work management.

### Technical Success

The MVP path must work to a high standard and be dependable enough for real use. Core technical success begins with correct assignment of a free-text to-do to the appropriate project, followed by reliable bead creation and dependable workflow behaviour.

Technical success also requires a simple end-to-end execution model that works cleanly for straightforward tasks. For simple to-dos, defined here as work that can be completed in one or two steps, the system must be able to create the corresponding git branch, carry the work through execution, and support the intended branch integration flow without breaking down.

The platform must also preserve trust. Reliable behaviour is not a secondary quality attribute in this product; it is part of the core value proposition, because the user must be willing to depend on the system for both organisation and delegated execution.

### Measurable Outcomes

The product should demonstrate measurable improvement in user productivity by increasing completed tasks, reducing time spent deciding what to do next, and shortening the path from captured intent to meaningful action.

By month one, the creator should be using the system for real personal project management and task dispatch. By month three, at least one additional person should be using it in practice. By month twelve, the creator should still rely on it regularly, indicating that it has crossed from experimental utility into durable personal importance.

Technically, the MVP must demonstrate successful end-to-end handling of a simple to-do: free-text capture, correct project assignment, bead creation, basic planning and execution, and git branch workflow completion.

## Product Scope

### MVP - Minimum Viable Product

The MVP includes the ability to capture a free-text to-do, assign it to the correct project, and create a bead representing that work. It must support a simple level of agentic planning and execution so that a task can move from captured intent into action rather than stopping at organisation.

The MVP also includes a practical git workflow for delegated work. The initial branch model can be deliberately simple: one long-lived branch per to-do, rather than early optimisation into branch-per-subtask orchestration. The goal at MVP stage is not maximum sophistication, but a dependable end-to-end flow that works for simple, real tasks.

### Growth Features (Post-MVP)

Post-MVP growth should improve the quality and flexibility of agentic execution. This includes specialised workflows based on task type, such as documentation-oriented flows, software-development flows, or other domain-specific execution patterns.

Growth features may also include the use of richer prompt libraries, BMAD-aligned workflow patterns, and more capable planning or routing mechanisms that improve execution quality without sacrificing the product's organisational clarity.

### Vision (Future)

The long-term vision is a rich, task-type-aware orchestration system that can deliver successful outcomes both for individual tasks and for the longer-running projects that contain them. In that future state, the product does not merely store tasks or initiate workflows; it understands the nature of the work, applies the right orchestration strategy, and helps the user maintain control across a portfolio of evolving projects.

The dream version of the product is an essential personal operating layer for multi-project work: a system that keeps the user organised, preserves context, and reliably dispatches the right kinds of agentic workflows to drive meaningful progress.

## User Journeys

### Journey 1: Primary User - Daily Capture and Dispatch Success Path

We meet the user in the middle of a normal working day, juggling several active projects and carrying a loose mental queue of things that need doing. In their current workflow, ideas arrive quickly but often get captured inconsistently, delayed, or lost while attention shifts elsewhere. The user wants a fast way to record a piece of work without having to stop and manually re-establish all the surrounding project context.

They enter a free-text to-do into Ideastream. Instead of becoming just another disconnected task in a flat list, the to-do is assigned to the correct project and turned into a bead that represents a real unit of work. The user immediately feels that the system understands the organisational context of what they meant, rather than merely storing the words they typed.

From there, the system supports simple planning and execution. For a straightforward item, the user sees the work move from captured intent into action, with the associated git branch workflow created and managed in a way that fits the task. The climax of the journey is the moment the user realises that they did not just record work; they successfully initiated progress. The resolution is a sense of relief and momentum: the task is no longer floating in memory, and the user can move on confidently.

This journey reveals requirements for low-friction capture, correct project inference, bead creation, simple planning, execution triggering, and a trustworthy end-to-end branch workflow.

### Journey 2: Primary User - Multi-Project Review and Prioritisation

We meet the user at the start of a work session, facing several projects in different states of progress. Without a clear organising layer, the user would typically spend time reconstructing status from memory, scattered notes, repositories, or unfinished conversations. The deeper need here is not just seeing a task list, but regaining orientation across a portfolio of active work.

In Ideastream, the user reviews what is waiting, what is in progress, and what has already been completed across projects. The experience needs to reduce cognitive load rather than add another dashboard to interpret. The system helps the user understand where work belongs, what has already moved forward, and what still needs intervention.

The climax of this journey is not automation but clarity. The user can decide what to do next without a long period of reloading context. The resolution is a more directed workday: less time spent choosing, less risk of forgetting important work, and more confidence that tasks are staying connected to the right projects.

This journey reveals requirements for cross-project visibility, status clarity, project-scoped work views, prioritisation support, and a history or state model that makes progress legible.

### Journey 3: Primary User - Recovery and Troubleshooting

We meet the user when something does not go cleanly. A bead may not have progressed as expected, a task may appear stalled, or the resulting work may need inspection before the user trusts it. In most agentic systems, this is the point where confidence breaks down because the user can no longer tell what happened or what to do next.

In Ideastream, the same individual user shifts into a troubleshooting mode. They inspect the relevant project, the bead, and the execution state to understand what was attempted, what outcome was produced, and whether the task needs correction, rerouting, or completion by hand. The system must help the user answer practical questions quickly: What happened? What state is this in? What is the next safe move?

The climax of this journey is successful recovery of understanding. Even if the task outcome is imperfect, the user is not left confused about system behaviour. The resolution is preserved trust: the user can correct course, retry, or continue manually without losing the thread of the work.

This journey reveals requirements for execution traceability, clear state transitions, visible outcomes, error recovery paths, and inspection tools that support human understanding rather than hiding the underlying process.

### Journey 4: Primary User - Initial Project Setup and Operational Control

We meet the user when bringing a new project into the system or deciding how an existing project should participate in the workflow. Because this is an individual-focused tool, there is no separate admin role; the same user is responsible for both productive use and operational setup. They need the system to be powerful enough to manage real work, but not so operationally heavy that setup becomes its own burden.

The user creates or configures a project boundary, establishes the repository relationship where relevant, and expects future to-dos to land in the right place. For MVP, the user also needs confidence that the branch workflow is understandable and predictable, such as using one long-lived branch per to-do for simple delegated work.

The climax of this journey is the point where the user sees that project structure, task organisation, and execution mechanics align cleanly enough to support daily use. The resolution is operational confidence: the system is ready to serve as a real working layer rather than as an interesting experiment.

This journey reveals requirements for project creation and management, repository association, simple workflow configuration, transparent branch strategy, and enough control for the user to trust the setup they are relying on.

### Journey Requirements Summary

These journeys point to a product that must support four capability groups.

First, it needs strong organisational capabilities: free-text capture, project-scoped task assignment, cross-project visibility, and clear status views. Second, it needs dependable execution capabilities: bead creation, simple planning, agentic dispatch, and end-to-end handling of straightforward tasks. Third, it needs trust-preserving inspection capabilities: visible execution state, understandable outcomes, and recovery paths when work does not go as expected. Fourth, it needs lightweight operational capabilities: project setup, repository linkage, and a simple but reliable branching model that an individual user can understand and depend on.

## Domain-Specific Requirements

### Compliance & Regulatory

There are no formal compliance, regulatory, or certification requirements for the MVP. The product is operating in a general software and productivity domain rather than a regulated sector, so domain requirements should focus on safe system behaviour rather than external approval regimes.

### Technical Constraints

The most important technical constraint is repository safety. The contents of trunk must never be placed at risk by the product's orchestration behaviour. Any planning, execution, branching, or merge flow must preserve a clear boundary between in-progress work and accepted project state.

The product should also avoid creating a false sense of security around privacy or intellectual property protection. Ideastream may orchestrate work, but the responsibility for secure repository hosting, private infrastructure, and appropriate model tenancy remains with the user. If a user wants to protect sensitive intellectual property or private data, they must configure their repositories and agent/model providers accordingly.

### Integration Requirements

The MVP does not require external integrations for compliance purposes. The key integration boundary is with the user's chosen repositories and the agentic systems that Ideastream dispatches to. Those integrations must be designed so that sensitive work is only sent to environments the user has explicitly chosen and trusts.

### Risk Mitigations

The primary domain-specific risk is unsafe repository automation that could damage or contaminate trunk. This should be mitigated through a strict operational model in which delegated work happens away from trunk, with clear visibility into what is proposed before accepted state is changed.

A second risk is misplaced trust in the orchestration layer as a security boundary. This should be mitigated by making responsibilities explicit: Ideastream coordinates work, but users remain responsible for selecting secure repository hosting, private infrastructure, and appropriately tenanted model providers.

A third risk is silent or opaque agent behaviour that makes it difficult for the user to understand what happened. This should be mitigated through clear traceability of dispatched work, visible outcomes, and understandable recovery paths when execution does not proceed as expected.

## Innovation & Novel Patterns

### Detected Innovation Areas

Ideastream challenges the assumption that task managers are inherently passive systems that only organise intent. Its core innovation is the idea that a to-do list can, whenever appropriate, move beyond storage and coordination into actual execution. In this model, a task is not just something to remember; it can also become something the system helps progress or complete.

The product is also innovative in the way it combines project-scoped organisation, cross-project dispatch, and optional agentic execution into a single operating model. Rather than forcing the user to manage tasks in one tool and trigger delegated work in another, Ideastream aims to make project management and action part of the same workflow.

A further innovation is its graduated adoption path. The product does not require the user to commit immediately to full automation. It is useful first as an organisational and project-dispatch tool, and only then expands into agentic execution. That lowers adoption friction while preserving a path to much greater leverage over time.

### Market Context & Competitive Landscape

The current market generally separates task management from agentic execution. Traditional task managers and project tools are designed to capture, organise, and prioritise work, but they do not usually attempt to complete that work. Agentic tools, by contrast, can execute specific workflows but often sit outside the user's main system of project organisation and require separate interaction patterns.

Ideastream's opportunity is to reduce reliance on that split-tool model. If successful, users should no longer need an external task manager for ordinary multi-project organisation and should reduce their dependence on separate agentic tools for a meaningful share of everyday delegated work. At the same time, the product does not assume it can replace every specialist workflow. More complex, dialogue-heavy processes may still require dedicated systems such as BMAD.

### Validation Approach

The innovation should be validated through practical replacement and dependency reduction rather than abstract novelty claims. The strongest validation signal is that users can manage their active work inside Ideastream without needing a separate task manager, while also using external agentic tools less often for routine workflows.

A second validation signal is behavioural trust. Users should feel comfortable creating a to-do in free text, letting the system attach it to the right project, and relying on the product to move it forward appropriately. If users continue to treat Ideastream only as a list-making tool and still default to separate agentic systems for ordinary work, then the innovation has not fully landed.

### Risk Mitigation

The primary innovation risk is overreaching: trying to replace every external tool and every complex workflow too early. This should be mitigated by keeping the product honest about its scope and by focusing first on the class of work that can be safely and usefully delegated.

A second risk is that the agentic promise may be stronger than the execution quality can support. This should be mitigated through a staged product model in which Ideastream remains valuable even if full task completion only works well for a subset of tasks.

The fallback product value is clear. Even if the more ambitious innovation does not fully land, Ideastream still succeeds as a strong project-scoped productivity and dispatch tool that helps users stay organised across multiple projects and route work more effectively.

## Developer Tool Specific Requirements

### Project-Type Overview

Ideastream is a developer tool delivered as a standalone CLI for repository-level task organisation and agentic dispatch. It is intentionally language-agnostic: the product does not depend on a particular application stack and does not require language-specific optimisation in its initial form. Instead, it operates at the level of project context, repository state, and workflow orchestration.

Repository-specific behaviour may be shaped by project-local instruction files such as `agents.md` and related conventions. This allows the product to remain general while still supporting per-project adaptation of agent behaviour.

### Technical Architecture Considerations

The core architecture should centre on a command-line interface as the single authoritative interaction surface. Human users can invoke Ideastream directly through the CLI, and agents can also invoke the same CLI commands when carrying out work. This keeps the execution model explicit and reduces the risk of hidden integration behaviour.

The system should not require deep IDE-specific functionality in MVP. Instead, the integration model should resemble Beads-style agent support: agents are given clear instructions for when and how to call the CLI in order to create to-dos, create or update beads, and progress work through the system.

Distribution should support the environments most likely to be used by the target audience. The initial packaging model should include npm distribution, Homebrew installation, and a practical Windows installation path.

### Installation Methods

The product should be installable as a standalone CLI through common developer-facing channels. At minimum, this includes npm and Homebrew, with Windows support also required through an appropriate platform-native path.

Installation should be simple enough that an individual user can get from zero to first use quickly, without needing a complex platform setup beyond the prerequisites required by the product's repository and agent workflow model.

### Language Matrix

The product should be explicitly positioned as language-agnostic. It works at repository level rather than language-runtime level, and its core value should not depend on whether a project is written in JavaScript, Python, Go, or another stack.

Where project-specific behaviour is needed, that behaviour should be expressed through repository-local instructions and conventions rather than hard-coded language support logic.

### API Surface

The primary public interface is the CLI command set. The command surface should be designed for both direct human use and predictable invocation by agents.

This implies that commands should be stable, understandable, and composable enough for agents to use safely. The CLI should expose the main operational actions required by the MVP, including creating and organising to-dos, associating them with projects, creating or updating beads, and supporting the repository workflow needed to move delegated work forward.

### Code Examples and Templates

The product should provide concrete examples and templates that help users understand how Ideastream is meant to be applied in real work. The most useful initial examples are not language-specific code samples, but workflow-oriented templates tied to task types.

Two high-value template categories are:
- document authorship workflows
- software development workflows

These examples should help users see how the same core system can support different types of delegated work while remaining grounded in a consistent project and repository model.

### Implementation Considerations

MVP implementation should prioritise clarity and reliability over breadth of integration. The CLI must be well-documented and safe enough to serve as the foundation for both manual use and agent invocation.

Essential documentation for MVP includes an installation guide, quick start, project setup guide, and CLI command reference. Together, these materials should be sufficient for a new user to install the tool, configure a project, understand the command model, and begin using the product without needing bespoke support.

The implementation should also preserve the product's central design principle: agents do not need a special hidden integration layer if they can be instructed to use the CLI directly and predictably.

## Project Scoping & Phased Development

### MVP Strategy & Philosophy

**MVP Approach:** Problem-solving MVP focused on proving that an individual user can manage multi-project work and safely move simple tasks from intent to execution within a single system.

**Resource Requirements:** The MVP is feasible as a primarily solo effort, but it requires capability across CLI/tooling design, repository workflow design, agent orchestration, and enough UX/documentation work to make the command model understandable and usable in practice.

The purpose of the MVP is not to establish a broad workflow platform upfront. It is to validate that Ideastream can solve a concrete daily problem: capturing work in free text, assigning it to the correct project, turning it into a bead, and supporting a safe and useful path into delegated execution.

### MVP Feature Set (Phase 1)

**Core User Journeys Supported:**
- Daily capture and dispatch for simple tasks
- Multi-project review and prioritisation at a basic but useful level
- Recovery and troubleshooting for simple delegated work
- Initial project setup and repository association

**Must-Have Capabilities:**
- Free-text to-do capture
- Correct project assignment
- Bead creation in the correct project
- Basic cross-project visibility into what is waiting, in progress, and completed
- Simple planning and execution flow for straightforward tasks
- Safe repository workflow using a simple one-branch-per-to-do model
- Traceable execution state so the user can understand what happened when work progresses or fails
- CLI-first operation with documentation sufficient for real use

The absolute smallest useful core is the path from free-text to-do to bead creation in the correct project. However, the real MVP should go further than that and prove the full product thesis for simple tasks by including a safe and dependable execution path.

### Post-MVP Features

**Phase 2 (Post-MVP):**
- Better quality and flexibility of agentic execution
- Improved planning and routing for delegated work
- Richer visibility into progress and execution outcomes
- Workflow-oriented templates for common task categories
- Expanded examples and operational guidance for real-world usage

**Phase 3 (Expansion):**
- Rich task-type-aware orchestration
- More specialised workflow paths for different kinds of work
- Stronger integration of prompt libraries and BMAD-aligned execution patterns
- Broader support for long-running project orchestration beyond simple delegated tasks
- A more mature personal operating layer for multi-project execution and oversight

### Risk Mitigation Strategy

**Technical Risks:** The highest technical risk is the repository workflow, especially ensuring that delegated execution never places trunk at risk. This should be mitigated by keeping the MVP branch model simple, constraining execution to straightforward tasks, and validating end-to-end branch handling before broadening orchestration sophistication.

**Market Risks:** The largest market risk is that users may still prefer separate task managers and separate agentic tools, leaving Ideastream as an interesting hybrid without a compelling reason to replace either. The MVP addresses this by focusing on the narrow but high-value workflow where project-scoped organisation and safe delegated action clearly belong together.

**Resource Risks:** If implementation capacity is tighter than expected, the first features to cut should be advanced task-type templates and other early generalisation efforts. The MVP should protect the core loop first: capture, assignment, bead creation, simple execution, and safe repository handling.

## Functional Requirements

### Project and Work Organization

- FR1: Users can create and manage projects that act as the primary containers for related to-dos, beads, and execution history.
- FR2: Users can associate a project with its relevant repository context where delegated work will occur.
- FR3: Users can view all active projects and understand the current state of work within each project.
- FR4: Users can capture a free-text to-do without first manually decomposing it into structured fields.
- FR5: Users can have a captured to-do assigned to the appropriate project context.
- FR6: Users can review and correct project assignment before or after work progresses.
- FR7: Users can create a bead from a captured to-do so the work becomes a trackable execution unit.
- FR8: Users can view the relationship between a to-do, its project, and its associated bead.

### Task Intake and Dispatch

- FR9: Users can submit a to-do for organisational handling without immediately dispatching it to an agent.
- FR10: Users can choose to trigger planning or execution for a bead when the work is suitable for delegation.
- FR11: Users can distinguish between work that is only captured, work that is planned, work that is in progress, and work that is completed.
- FR12: Users can route work through a simple delegated workflow appropriate to straightforward tasks.
- FR13: Users can see whether a to-do is being handled manually, awaiting action, or being progressed through an agentic workflow.
- FR14: Agents can invoke product capabilities through the public command model when acting on behalf of the user.
- FR15: Users can control whether a given task remains organisational only or proceeds into delegated execution.

### Planning and Execution Management

- FR16: Users can have a simple task translated into an actionable unit of work suitable for execution.
- FR17: Users can inspect the current execution state of a bead at any point in its lifecycle.
- FR18: Users can see what work was attempted, what outcome was produced, and what next action is available.
- FR19: Users can retry, reroute, or complete work manually when delegated execution does not produce an acceptable result.
- FR20: Users can use the product for simple delegated workflows without requiring a separate agentic tool for every routine task.
- FR21: Users can keep more complex or dialogue-heavy workflows outside the product when the task is not suitable for in-product delegation.

### Cross-Project Visibility and Prioritization

- FR22: Users can view what work is waiting, in progress, and completed across multiple projects.
- FR23: Users can identify what requires attention next without reconstructing status from multiple external sources.
- FR24: Users can review progress history so that completed and ongoing work remains legible across project switches.
- FR25: Users can use the product as their primary organisational view for everyday multi-project work.
- FR26: Users can avoid losing track of work as they move between projects and contexts.

### Repository and Workflow Safety

- FR27: Users can have delegated work performed away from trunk so accepted project state remains protected.
- FR28: Users can have simple delegated tasks associated with a dedicated branch workflow appropriate to that task.
- FR29: Users can see the relationship between delegated work and its repository workflow state.
- FR30: Users can inspect proposed work before accepted project state changes.
- FR31: Users can rely on the product to preserve a clear boundary between in-progress work and accepted repository state.
- FR32: Users can recover safely from delegated-work failures without losing track of branch or task state.

### Traceability, Inspection, and Recovery

- FR33: Users can inspect the history of a bead to understand how work progressed over time.
- FR34: Users can understand why a task is stalled, failed, or awaiting further action.
- FR35: Users can view execution outcomes in enough detail to decide whether to accept, revise, retry, or replace them.
- FR36: Users can troubleshoot task progress without needing a separate support role or hidden system knowledge.
- FR37: Users can preserve trust in the product by understanding what happened when automation succeeds or fails.

### CLI, Guidance, and Adoption Support

- FR38: Users can install the product as a standalone CLI through supported distribution channels.
- FR39: Users can set up a project for use with the product using documented guidance.
- FR40: Users can discover and use the available command surface through a CLI command reference.
- FR41: Users can adopt the product first as an organisational tool before using delegated execution capabilities.
- FR42: Users can apply repository-local instructions and conventions to shape how agents behave within a project.
- FR43: Users can start from workflow examples or templates for at least document authorship and software development use cases.
- FR44: Agents can be instructed how to use the CLI directly as part of repository-local workflow guidance.

## Non-Functional Requirements

### Performance

Free-text capture and project assignment must feel fast enough that they do not interrupt the user's flow of thought. The product should support rapid transition from idea to recorded work without introducing noticeable friction at the point of capture.

Cross-project status views must also be responsive enough to support regular prioritisation and orientation. The user should be able to inspect what is waiting, in progress, and completed across projects quickly enough that the product reduces context-switch overhead rather than becoming another source of delay.

### Reliability

The system must not fail silently. If a task cannot be assigned, a bead cannot be created, or delegated work cannot proceed, the user must be able to see clearly that the operation did not complete successfully.

Repository workflows must either complete safely or stop in a way that leaves no ambiguity about current state. The user should always be able to determine whether work is pending, in progress, failed, or ready for the next step.

Task and execution state must remain legible throughout the lifecycle of a bead so that users can trust the system during both successful automation and failure recovery.

### Security

The product must preserve a strict separation between accepted repository state and in-progress delegated work. Trunk must not be placed at risk by the orchestration model, and work in progress must remain clearly isolated from accepted project state.

The product should eliminate avoidable risky operations through its workflow design rather than relying on frequent confirmation prompts. Safety should come from constrained operating patterns, visible state boundaries, and predictable repository handling.

The system must not create misleading assumptions about privacy or intellectual property protection. Where external repositories, agents, or models are involved, the product should make it clear that users are responsible for choosing secure hosting, infrastructure, and model tenancy appropriate to their work.

### Integration

Repository and agent integrations must provide clear error reporting when operations fail or cannot proceed. Users should not need hidden system knowledge to understand that an integration failed or what to do next.

Integration failures must be recoverable. The system should preserve enough state and traceability that a user can retry, reroute, or continue manually without losing the thread of work.

The product must provide explicit visibility into what external repository or agent-related action was requested, so users can understand how delegated work moved through the system and what dependencies were involved.