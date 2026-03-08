---
stepsCompleted: [1, 2, 3, 4]
inputDocuments: []
session_topic: 'Agentic multi-project to-do list'
session_goals: 'Explore how to design a multi-project to-do system spanning trivial reminder items and complex repository-backed work involving artefacts, planning, orchestration, and version-controlled evolution.'
selected_approach: 'ai-recommended'
techniques_used: ['First Principles Thinking', 'Morphological Analysis', 'Constraint Mapping']
ideas_generated: ['Project-Scoped To-Dos', 'Version Outcomes Not Instructions', 'Projects as Memory Containers', 'Git as Concurrency Substrate', 'To-Do as State Change Request', 'Progressive Elaboration', 'Repository as Ambient Context', 'Natural Language Capture with Optional Metadata', 'Adaptive Branching Policy', 'Capability-Tagged Execution Graph', 'Split Authorities: Beads for Orchestration, Git for Outcomes', 'Transactional Closure for Agent Work', 'Conservative Project Inference', 'Ephemeral Do-Scoped State', 'Project Content vs System Memory', 'Beads as Handoff Memory', 'Repo for Material Working State', 'Commit-Referenced Task Handoffs', 'Project-Native Verification Hierarchy', 'Managed Remediation To-Dos', 'Folder-Scoped Verification Policies', 'Markdown Verification Policies', 'Conventional Policy Filename .verify.md', 'Policy Contradictions Are Configuration Errors', 'Git Determines Whether Verification Is Needed', 'Final Merge Candidate Determines Verification Scope', 'Project Memory Exempt Except Policy Files', 'Root .memory Folder', 'Lightweight Conventions for .memory', 'Stable Facts vs Conventions in .memory', 'Separate Memory Files by Trust Class', 'Selective Memory Reading']
context_file: ''
session_active: false
workflow_completed: true
---

# Brainstorming Session Results

**Facilitator:** Richard
**Date:** 2026-03-07 17:10:41

## Session Overview

**Topic:** Agentic multi-project to-do list
**Goals:** Explore how to design a multi-project to-do system spanning trivial reminder items and complex repository-backed work involving artefacts, planning, orchestration, and version-controlled evolution.

### Session Setup

The session is focused on a to-do system that needs to handle a wide spectrum of work. At one end are simple reminder-style items that mainly exist to keep the project owner aware of something that must be done manually. At the other end are higher-complexity initiatives that need structured planning, generated artefacts, and coordination of actions over time.

The user expects some projects to represent applications, tools, or documents that evolve under version control. The repository boundary is therefore not incidental; it is part of the operating model for how complex work is represented, changed, and governed.

## Technique Selection

**Approach:** AI-Recommended Techniques
**Analysis Context:** Agentic multi-project to-do list with focus on supporting trivial reminders, human-only actions, and complex repository-backed work that evolves through version control.

**Recommended Techniques:**

- **First Principles Thinking:** Rebuild the problem from fundamental truths so reminders, projects, repositories, and agent-capable work are modelled cleanly.
- **Morphological Analysis:** Explore a broad solution space by combining independent design dimensions instead of converging too early.
- **Constraint Mapping:** Pressure-test the model against hard boundaries such as human-only tasks, git suitability, and orchestration limits.

**AI Rationale:** The problem is architectural rather than merely functional. This sequence starts by clarifying irreducible concepts, then expands the design space systematically, and finally narrows it using operational constraints.

## Technique Execution Results

**First Principles Thinking:**

- **Interactive Focus:** Identify the true parent object in the system, separate the evolving project from the lightweight to-do, and clarify what should and should not be version controlled.
- **Key Breakthroughs:** The project is the long-lived unit, to-dos only exist inside a project, and version control belongs to project outcomes and memory rather than to the to-do items themselves.

**Key Ideas Generated:**

**[Category #1]**: Project-Scoped To-Dos
_Concept_: A to-do is not a standalone object. It only has meaning inside a project, which acts as the durable context for intent, execution, and outcomes. This makes the project the primary unit of truth and turns to-dos into project-scoped work cues.
_Novelty_: Most task systems treat tasks as globally first-class and optionally grouped; this reverses that and makes project membership mandatory.

**[Category #2]**: Version Outcomes Not Instructions
_Concept_: The repository versions artefacts, plans, memory, and other evolving project outputs, while the to-do item remains lightweight and mostly immutable. A to-do may trigger work that changes the repo, but the instruction itself is not what evolves.
_Novelty_: This avoids overloading task objects with change history and keeps version control attached to durable outcomes rather than ephemeral prompts.

**[Category #3]**: Projects as Memory Containers
_Concept_: Even relatively simple projects can justify persistent storage if they accumulate useful reference material over time, such as addresses, schedules, and recurring contextual facts. This expands the role of a project from delivery container to long-term memory boundary.
_Novelty_: It suggests that repositories may be useful not only for building artefacts, but also for preserving structured situational memory around a domain of responsibility.

**[Category #4]**: Git as Concurrency Substrate
_Concept_: The repository is not merely where files live; it is the operational layer that allows multiple agents to work on the same project independently and merge their changes coherently. Branches, diffs, and merges become core primitives for agent collaboration.
_Novelty_: This treats git as the execution integration layer for agentic work, not just as archival version control.

**[Category #5]**: To-Do as State Change Request
_Concept_: A to-do represents a piece of work that needs completing within a project and, when completed, will change the state of that project. The to-do therefore defines intended delta rather than standing alone as a free-form reminder.
_Novelty_: It reframes to-dos as declarative requests for project evolution rather than generic checklist items.

**[Category #6]**: Progressive Elaboration
_Concept_: To-dos should be simple to capture and only gain richer fields such as acceptance criteria, dependencies, and decomposition when the work becomes complex or agent-delegated. This preserves a low-friction interface without sacrificing rigour where it matters.
_Novelty_: Instead of forcing every task into a full specification, the system lets structure emerge in proportion to execution complexity.

**[Category #7]**: Repository as Ambient Context
_Concept_: Agents should not rely solely on the to-do text; they should also use the current repository contents, notes, memories, and artefacts as working context. The project repository becomes a live context field that informs interpretation and execution.
_Novelty_: This shifts context from being embedded in each task to being largely inherited from project state, reducing input burden on the user.

**[Category #8]**: Natural Language Capture with Optional Metadata
_Concept_: The ideal interface accepts natural-language requests, infers the relevant project, and extracts optional signals such as due date, urgency, or delegation intent when they are present. Users can provide more structure when they want to, but are not forced to do so.
_Novelty_: This combines conversational capture with opportunistic parsing, allowing the system to stay simple for the human while still producing structured work objects.

**[Category #9]**: Adaptive Branching Policy
_Concept_: The integration model should be selected based on inferred complexity at capture time, then revised during planning once decomposition and dependency structure are understood. Branching policy is therefore an execution consequence of the planned work graph rather than a fixed repository rule.
_Novelty_: This replaces one-size-fits-all workflow policy with proportionate execution control tied to actual work shape.

**[Category #10]**: Capability-Tagged Execution Graph
_Concept_: Planning should produce an execution graph with nodes that describe work items, dependencies, complexity, and required capabilities, but not named agents. A separate routing layer can then assign those nodes to available agents dynamically.
_Novelty_: It decouples durable planning from transient resource assignment, which makes the system more robust to changing agent pools.

**[Category #11]**: Split Authorities: Beads for Orchestration, Git for Outcomes
_Concept_: Live orchestration state can be owned by Beads and Dolt, while the repository remains authoritative for project content, memory, and accepted outcomes. The two systems have different responsibilities and should interoperate explicitly rather than pretending to be one store.
_Novelty_: This embraces dual authority boundaries deliberately, reducing confusion about whether planning/runtime state or project artefacts are the source of truth for a given concern.

**[Category #12]**: Transactional Closure for Agent Work
_Concept_: Agent-completed work should not close its orchestration bead until the corresponding repository integration has succeeded. The execution lifecycle therefore needs a distinction between work being produced and work being accepted into project state.
_Novelty_: This introduces a practical consistency guarantee only where the system can actually enforce it, rather than pretending all work is equally controllable.

**[Category #13]**: Conservative Project Inference
_Concept_: Natural-language project inference should only proceed automatically at very high confidence. If confidence is not extremely high, the system must ask which project is intended before the to-do is created or executed.
_Novelty_: It explicitly optimises for avoiding wrong-project execution, accepting higher confirmation friction as the safer failure mode.

**[Category #14]**: Ephemeral Do-Scoped State
_Concept_: Complex decomposed work may need transient execution state that records what happened in earlier stages so later stages can proceed correctly. That state is useful during execution but may become disposable once the to-do is complete and the durable project changes have landed.
_Novelty_: It separates temporary orchestration memory from durable project memory, preventing execution scaffolding from polluting the long-term repository.

**[Category #15]**: Project Content vs System Memory
_Concept_: The repository should distinguish between primary project content and additional system memory that exists mainly to support agents. These are both durable, but they serve different purposes and should likely be stored and governed differently.
_Novelty_: This introduces an internal memory taxonomy rather than treating all repository files as equally trustworthy context.

**[Category #16]**: Beads as Handoff Memory
_Concept_: Downstream tasks can inspect completed upstream beads and read compact handoff information there, rather than relying on hidden repository state for all execution context. Beads becomes the place where execution meaning is published and inherited across dependent tasks.
_Novelty_: It uses the orchestration graph itself as the carrier for inter-task understanding, reducing the need to force workflow metadata into git history.

**[Category #17]**: Repo for Material Working State
_Concept_: The repository should carry real project artefacts and any intermediate material outputs that later tasks must build on directly, while Beads carries compact summaries and pointers. This preserves git for things that are genuinely file-like and keeps orchestration metadata out of the content store.
_Novelty_: It distinguishes execution metadata from material work product instead of treating both as the same kind of transient state.

**[Category #18]**: Commit-Referenced Task Handoffs
_Concept_: When an upstream task completes, its handoff should include a compact summary plus a commit reference pointing to the repository state it produced. Downstream tasks can then recover exact context by inspecting that commit in git rather than trusting duplicated path summaries.
_Novelty_: This creates a lightweight but precise bridge between orchestration state in Beads and concrete project state in git.

**[Category #19]**: Project-Native Verification Hierarchy
_Concept_: Final verification should be derived primarily from repository configuration and repository-native checks, then supplemented by project memory and conventions, with the original to-do text used only as a fallback when the project itself does not define validation strongly enough.
_Novelty_: It makes correctness emerge from the project's own standards rather than from the user's phrasing of a task.

**[Category #20]**: Managed Remediation To-Dos
_Concept_: If parent-level verification fails, the system should keep the parent open and automatically create linked remediation to-dos inside the same Beads graph, allowing one automatic repair pass before further escalation.
_Novelty_: It ensures failure recovery remains visible, dependency-aware, and governed by the same orchestration model as all other work.

**[Category #21]**: Folder-Scoped Verification Policies
_Concept_: Repositories can define explicit verification policy files at project level and within specific subfolders. When work touches a subfolder with its own policy, that local policy also applies, allowing validation rules to follow repository structure.
_Novelty_: This introduces hierarchical, path-aware verification so different parts of a project can enforce different standards without forcing one global policy to fit everything.

**[Category #22]**: Markdown Verification Policies
_Concept_: Verification policy should be written as agent-ingested markdown rather than a rigid config schema. A policy file can describe commands to run, architectural constraints to respect, and other free-form instructions that help an agent decide how to validate work in that scope.
_Novelty_: This treats verification policy as human-readable operational guidance for agents, preserving flexibility across software, writing, research, and mixed-content projects.

**[Category #23]**: Conventional Policy Filename `.verify.md`
_Concept_: Verification guidance should be discovered through a conventional hidden markdown filename placed in any folder whose contents need local validation rules. Agents can then deterministically walk up the folder hierarchy, loading each applicable `.verify.md` from deepest scope to project root.
_Novelty_: It provides deterministic policy discovery without introducing a separate manifest or schema system.

**[Category #24]**: Policy Contradictions Are Configuration Errors
_Concept_: All applicable `.verify.md` files should be considered, with deeper policies treated as more specific. If policies genuinely contradict each other, verification must fail and report a project configuration error rather than guessing which rule to follow.
_Novelty_: This treats conflicting validation guidance as a broken project contract instead of silently choosing an unsafe interpretation.

**[Category #25]**: Git Determines Whether Verification Is Needed
_Concept_: Whether repository verification is required can be decided at parent completion time by inspecting the branch state. If the branch contains no changed files, no repository verification is necessary; git is the source of truth for whether project state actually changed.
_Novelty_: This avoids speculative classification and lets completion logic depend on observed repository reality rather than on earlier planning guesses.

**[Category #26]**: Final Merge Candidate Determines Verification Scope
_Concept_: Only the final merge candidate relative to trunk should be considered when deciding whether verification is necessary. Temporary execution artefacts or reverted work on the branch do not matter if they are absent from the final integration candidate.
_Novelty_: It bases verification on what is actually about to land rather than on everything that happened during execution.

**[Category #27]**: Project Memory Exempt Except Policy Files
_Concept_: Changes confined to project memory should not trigger repository verification by themselves, because they do not necessarily alter the primary project outcome. An exception exists for `.verify.md` policy files: changing verification policy should itself trigger verification.
_Novelty_: This distinguishes supportive memory updates from meaningful changes to project validation rules, preventing unnecessary checks while preserving policy integrity.

**[Category #28]**: Root `.memory` Folder
_Concept_: Durable project memory should live in a conventional root-level `.memory` folder. This gives agents a deterministic location for long-term supporting context and provides a clear exemption boundary for verification triggers.
_Novelty_: It makes project memory an explicit first-class repository area rather than an inferred collection of files.

**[Category #29]**: Lightweight Conventions for `.memory`
_Concept_: The `.memory` folder should start with lightweight conventions rather than a rigid schema. Agents can expect it to contain durable supporting context, but the project can evolve its internal structure over time without being locked into a strict format.
_Novelty_: It balances discoverability with flexibility, allowing real usage patterns to shape future structure.

**[Category #30]**: Stable Facts vs Conventions in `.memory`
_Concept_: Project memory should distinguish between stable facts and conventions. Stable facts capture enduring truths about the project or domain, while conventions capture preferred ways of working, validating, or interpreting the project.
_Novelty_: This separates hard reference knowledge from softer operational guidance, helping agents treat each class with the right level of trust.

**[Category #31]**: Separate Memory Files by Trust Class
_Concept_: Stable facts and conventions should live in separate files within `.memory` rather than being mixed in the same document. This gives agents an explicit trust boundary when reading and updating project memory.
_Novelty_: It removes ambiguity about whether a given file is authoritative reference or softer operational guidance.

**[Category #32]**: Selective Memory Reading
_Concept_: Agents should not read all project memory by default. They should selectively load only the `.memory` files relevant to the current to-do, avoiding memory bloat and preserving focus.
_Novelty_: It treats project memory as a discoverable knowledge base rather than as mandatory context to ingest wholesale.

### Creative Facilitation Narrative

The session began by separating projects from to-dos and establishing that to-dos only exist within a project. From there, the architecture sharpened around a split authority model: Beads and Dolt own live orchestration state, while git repositories own durable project content, memory, and accepted outcomes. The discussion then moved into execution structure, adaptive branching, compact handoffs, hierarchical verification, and project memory design until the core operating model stabilised.

### Session Highlights

**User Creative Strengths:** The user repeatedly corrected over-generalised models with precise operational distinctions, especially around project scope, repository authority, and low-friction interaction design.
**AI Facilitation Approach:** The facilitation alternated between first-principles clarification, morphology across architecture options, and constraint mapping to resolve safety, verification, and memory-boundary questions.
**Breakthrough Moments:** Mandatory project scope for every to-do, Beads as live orchestration authority, commit-referenced handoffs, hierarchical `.verify.md` policies, and the root `.memory` folder with semantic retrieval.
**Energy Flow:** The session maintained steady depth, with the user preferring progressively sharper architectural commitments over broad ideation once the core model emerged.

## Idea Organization and Prioritization

**Thematic Organization:**

**Theme 1: Core Domain Model**
_Focus: defining the primary objects and relationships in the system._

- **Project-Scoped To-Dos:** To-dos only exist within projects, and projects are the durable unit of meaning.
- **To-Do as State Change Request:** A to-do asks for a project state change rather than existing as a standalone reminder.
- **Version Outcomes Not Instructions:** Git versions outcomes, artefacts, and memory, not the task text itself.

**Theme 2: Orchestration and Execution**
_Focus: how work is planned, routed, decomposed, and integrated._

- **Capability-Tagged Execution Graph:** Planning produces graph nodes with dependencies and required capabilities.
- **Adaptive Branching Policy:** Branching strategy depends on complexity and decomposition shape.
- **Transactional Closure for Agent Work:** Agent-completed work should not close until the repository integration succeeds.
- **Managed Remediation To-Dos:** Failed verification creates linked follow-up work inside the same graph.

**Theme 3: Authority Boundaries and Handoffs**
_Focus: separating orchestration truth from project truth._

- **Split Authorities: Beads for Orchestration, Git for Outcomes:** Beads and Dolt own live orchestration state; git owns accepted project state.
- **Beads as Handoff Memory:** Upstream task meaning is recorded in Beads for downstream tasks.
- **Commit-Referenced Task Handoffs:** Beads stores compact execution summaries and links to the relevant git commit when work produces repository changes.

**Theme 4: Verification and Safety**
_Focus: deciding when and how work is considered valid._

- **Project-Native Verification Hierarchy:** Verification should come first from repo policy and native checks, then project memory, then task text as fallback.
- **Folder-Scoped Verification Policies:** `.verify.md` files apply by folder hierarchy from deepest scope outward.
- **Policy Contradictions Are Configuration Errors:** Conflicting policies should fail verification rather than be guessed through.
- **Git Determines Whether Verification Is Needed:** Only actual final merge-candidate changes trigger verification.

**Theme 5: Repository Memory Design**
_Focus: durable supporting context and how agents should consume it._

- **Root `.memory` Folder:** Durable project memory lives in an explicit root folder.
- **Stable Facts vs Conventions in `.memory`:** Memory separates authoritative facts from working conventions.
- **Separate Memory Files by Trust Class:** Facts and conventions live in different files.
- **Selective Memory Reading:** Agents use semantic retrieval instead of loading all memory by default.

**Prioritization Results:**

- **Top Priority Ideas:** project-scoped to-dos, split authority between Beads and git, adaptive branching and execution graphs, project-native verification, and `.memory` plus `.verify.md` as explicit repository primitives.
- **Quick Win Opportunities:** define the minimal repo layout (`.memory`, `.verify.md`), specify the Beads handoff format, and sketch the parent/child branch workflow.
- **Breakthrough Concepts:** verification driven by final merge candidate reality, hierarchical markdown verification policies, and treating Beads as execution meaning while git remains material truth.

**Action Planning:**

1. Define the minimal repository contract: visible project content, root `.memory`, and conventional `.verify.md` files.
2. Specify the Beads task schema additions or conventions needed for compact handoffs, commit references, and remediation linking.
3. Design the planning output: capability-tagged execution graph, complexity revision stage, and branching-policy selection logic.
4. Draft the completion pipeline for parent tasks: child closure, parent integration, verification, and remediation creation on failure.
5. Create example `.verify.md` and `.memory` documents for at least one software project and one writing or research project.

## Session Summary and Insights

**Key Achievements:**

- Established a coherent operating model for a multi-project, agentic to-do system.
- Clarified the system boundary between Beads orchestration and git-backed project outcomes.
- Defined a practical verification model driven by repository structure, policy, and actual merge candidates.
- Identified explicit repository primitives for durable memory and scoped verification.

**Session Reflections:**

The strongest outcomes emerged when the design was forced to respect both low-friction capture and high-rigour execution. The user consistently pushed the model toward explicit boundaries, conservative safety rules, and repository-native truth, which made the architecture materially stronger.
