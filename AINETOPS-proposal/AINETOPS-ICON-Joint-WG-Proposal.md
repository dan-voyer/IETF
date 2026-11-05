# AINETOPS and ICON: Proposal for a Common Working Group

5 November 2026

> **For discussion with AINETOPS and ICON participants.** This proposal does not represent community or IETF consensus. The working group name and document adoption remain open.

## 1. Why bring the work together?

An operator needs to know what an agent has been asked to do, which limits apply, what it has actually done, and whether it can be stopped when necessary. AINETOPS and ICON approach these questions from different directions. AINETOPS emphasizes task exchange and the operational management of agents; ICON emphasizes observing and controlling their behavior, including intervention when an agent cannot be relied on to respond. These responsibilities involve distinct interfaces, but share information about tasks, constraints, actions, and results.

Both efforts address aspects of task progress, human oversight, and intervention. For example, when an operator asks to stop a task that has already initiated a network change, the system handling the task and the system supervising it need to identify the same operation, understand what has happened, and report what remains in progress. Different terminology should not lead to incompatible definitions of these shared concepts.

We propose developing this shared information and the related interfaces in one working group while preserving the separation between task execution and independent supervision. Agent lifecycle management and supervision during execution would remain distinct parts of the work. The initial scope below selects work from both efforts; it does not include every requirement in the current drafts.

The proponents will discuss placement with the relevant Area Directors, NMOP, and OPSAWG. Existing groups remain possible homes for parts of the work. The reason to consider a common group is to keep the related specifications consistent throughout development and implementation.

## 2. Proposed charter

### Purpose

Network operators need agents, controllers, and supervising systems from different implementations to exchange tasks and results consistently. Operators also need to observe what agents do, constrain their actions, and intervene when necessary.

The working group will standardize the information and interfaces needed for these interactions in network management. It will develop data models and profiles of existing protocols so that systems agree on the task, the affected resources, the permitted actions, and the reported outcome. The specifications will apply independently of an agent's internal reasoning technology.

### Scope

The initial work will cover:

- **Assessment and planning:** diagnosis, capacity planning, or simulation without changing the operational network.
- **Authorized network changes:** proposing, checking, and executing changes to identified resources through existing management systems, then reporting and verifying their effects.

Tasks will identify their objectives, target resources, constraints, and completion criteria. Results will distinguish completion of an analysis, execution of a change, and achievement of the operational objective. Supporting evidence will identify the relevant inputs, time or state revision, checks performed, and limitations.

Agent lifecycle management will cover capabilities and operational state, including onboarding, enablement, and retirement. Runtime supervision will cover activity reporting, operating constraints, and intervention. Intervention will include approval, restriction, suspension, resumption, and termination where supported. Specifications will distinguish controls on an individual task from controls on the agent itself, and identify where those controls are enforced. The work will support supervision and enforcement that do not depend on the executing agent responding.

An accepted intervention request does not establish that its intended effect occurred. Reports will distinguish acceptance, enforcement, and observed effects, including partial or unknown outcomes. Stopping an agent task does not automatically stop a controller operation or reverse a completed network change. Recovery actions require appropriate authorization and separate reporting.

The work will use consistent identifiers and definitions across these interfaces while allowing separate components, data models, encodings, and domain-specific extensions.

### Deliverables

1. **Operational framework and requirements — Informational.** Describe the operational problem, roles, interface boundaries, representative workflows, and gaps in existing mechanisms. Operator reports, surveys, and implementation experience will inform this work. It will proceed alongside the Standards Track specifications.

2. **Network task and evidence models — Standards Track.** Define machine-readable representations of task scope, constraints, results, and supporting evidence. Include a concrete encoding and a mapping to at least one existing protocol, with a limited set of initial application profiles.

3. **Network-management skill interface profiles — Standards Track.** Define how a caller identifies and uses the supported inputs, outputs, and evidence formats of an operation exposed by an agent. Cover interface versions, compatibility, and machine-readable errors using existing communication and schema mechanisms.

4. **Agent lifecycle, observability, control, and intervention — Standards Track.** Define YANG models, operations, and notifications for agent operational state and lifecycle, activity reporting, constraints, supervision, and intervention outcomes. Distinguish lifecycle management from runtime supervision; these functions may be specified in separate modules. Specify their use with NETCONF or RESTCONF and existing notification mechanisms, reusing the task and evidence definitions.

Document boundaries may be adjusted within this scope. The specifications will define conformance requirements and error behavior. Implementation work will test interoperability across the interfaces.

### Boundaries and coordination

The working group will reuse existing network and service models, telemetry, identity, authorization, and audit mechanisms. Task constraints and delegation will not themselves grant access rights. Specifications will address security and privacy, including stale evidence, duplicate requests, and loss of visibility.

Coordination will include NMOP and OPSAWG on operational models and related work; NETMOD, NETCONF, and relevant domain groups on management models and protocols; AgentProto and DAWN on agent communication and discovery; and WIMSE, OAuth, and the AUDIT effort on identity, authorization, and traceability. Generic mechanisms and changes to externally maintained protocols will be taken to their responsible groups or maintainers.

The initial charter excludes AI training, prompting, internal reasoning, benchmarking methods, software-deployment systems, and general-purpose agent orchestration. It will not require disclosure of private internal reasoning traces or define a universal risk taxonomy, new agent communication or discovery protocol, or new cross-domain transaction, locking, or automatic rollback framework. Existing recovery and coordination mechanisms may be used.

### Proposed milestones

These are discussion targets relative to charter approval; calendar dates will be agreed during chartering.

| Target | Milestone |
| --- | --- |
| 6 months | Adopt initial drafts covering the framework and three Standards Track deliverables. |
| 12 months | Review implementation results and refine the initial application profiles. |
| 18 months | Submit the framework and requirements for Informational publication. |
| 24 months | Submit the Standards Track specifications for publication as Proposed Standards. |

## 3. Decisions for the joint discussion

1. Does this scope address the shared operational problem and give both efforts a useful common home?
2. Which scope limits need adjustment, particularly internal reasoning disclosure, recovery behavior, and cross-domain coordination?
3. Who can contribute as editors, implementers, and operator reviewers for each deliverable?

## Background

The following are inputs for discussion; their inclusion does not imply adoption:

- AINETOPS: [problem statement](https://datatracker.ietf.org/doc/draft-rqd-ainetops-problem-statement/), [task and evidence model](https://datatracker.ietf.org/doc/draft-sun-ainetops-task-and-evidence-model/), and [skill schema interfaces](https://datatracker.ietf.org/doc/draft-huang-ainetops-agent-schema-interfaces/).
- ICON: [problem statement](https://datatracker.ietf.org/doc/draft-wnd-opsawg-icon-ps/) and [architecture and requirements](https://datatracker.ietf.org/doc/draft-mcw-opsawg-icon-requirements/).

