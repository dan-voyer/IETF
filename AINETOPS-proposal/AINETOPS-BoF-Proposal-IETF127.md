# AINETOPS BoF Proposal — IETF 127

**Draft for discussion on ainetops@ietf.org. Not submitted.**

## Required details

**Name of proposed BoF:** AI-enabled Network Operations (AINETOPS)  
**Type:** WG-forming  
**Area:** Operations and Management  
**Responsible AD:** Mahesh Jethanandani  
**BoF chairs:** TBD; to be appointed by the responsible AD  
**Expected attendance:** 80–120 people  
**Session length:** 2 hours  
**Conflicts to avoid:** NMOP, OPSAWG, NETCONF, NETMOD, ANIMA, BMWG, NMRG, DAWN, AGENTPROTO, and AUDIT  
**Area Director support:** To be confirmed before submission

## Information for the IAB and IESG

### What protocols or practices already exist in this space?

NETCONF, RESTCONF, YANG, NACM, YANG-Push, and other telemetry mechanisms already provide access to network configuration and operational state. The ANIMA work also provides relevant autonomic-networking concepts: GRASP is defined in RFC 8990, and Section 7 of RFC 9222 discusses the lifecycle of Autonomic Service Agents.

Work elsewhere in the IETF is addressing agent discovery, communication, workload identity, authorization, delegation, and traceability. Implementations may also use external agent frameworks such as MCP or A2A. AINETOPS will reuse this work; it will not define another general-purpose agent protocol.

What is missing is a common operational approach for supervising an AI-based agent that can act on a production network. Implementations expose different ways to constrain an agent, observe its activity, intervene in a running task, and relate its actions to the operator's original objective and policy decisions.

### What changes to existing protocols or practices are required?

The proposed work will define data models, operations, notifications, and required behavior for agent lifecycle management and task supervision, using existing protocols and security mechanisms. Requirements and gap analysis will guide model development in parallel. Extensions to existing protocols or models owned by other working groups will be developed with those groups.

### What entirely new protocols or practices are required?

The initial charter commits to two Standards Track specifications: agent operational state and lifecycle, and agent task supervision and intervention. Each will define at least one mandatory interoperable binding using existing protocols; no new transport or general-purpose agent protocol is proposed. An operational framework and requirements document and implementation-informed operational guidance will support this work.

### What implementation experience exists?

The Agent Observability for Network Management Operations project at the IETF 126 Hackathon exercised an observability framework for network-management agents and informed the ICON problem-statement and requirements drafts. The BoF should also include operational experience from organizations deploying or evaluating agents that can take network actions.

## Problem statement

AI-based systems are moving beyond advising network operators. They can now plan and execute multi-step operational tasks, including making changes through existing management systems and protocols.

Consider an operator using agents and management tools from several vendors. The operator needs to know which devices, resources, data, and actions an agent is allowed to use; which task and policy authorized an action; what the agent is doing now; and how to approve, restrict, suspend, redirect, or stop the task. Afterward, the operator needs a record that relates the agent's actions and the resulting network changes to the original objective.

Today, those controls and records are implementation-specific. Existing network-management protocols expose the network, but they do not by themselves provide a common way to supervise the autonomous, multi-step behavior of the system using them. This makes safe multi-vendor deployment difficult and weakens operational accountability when something goes wrong.

AINETOPS will standardize the management interface between a supervising management system and network-management agents from different vendors. The interface will provide consistent agent state, task operations, and notifications using bindings to existing protocols.

AINETOPS addresses that operational gap. Its scope is the boundary between an AI-based agent and the network-management environment—not the agent's internal model, prompts, training, or reasoning method.

## Why the IETF, and why a new working group?

The problem occurs when agent-based systems use IETF management protocols, data models, and security mechanisms to observe or change networks. A useful approach must work across vendors while preserving the authority of existing access-control, security, and change-management systems.

NMOP and OPSAWG cover related operational work. The case for AINETOPS is a focused work program that keeps the management models, operational framework, and deployment practices consistent across agents, tools, and controllers. For example, suspending an agent task must have a clear operational meaning when a controller is already applying a network change. A dedicated group would own that consistency while developing the scoped agent-supervision models and coordinating changes to existing protocols and models with their responsible working groups.

| Concern | Primary venue | AINETOPS relationship |
|---|---|---|
| Existing network-management protocols and models | NETCONF, NETMOD, and relevant model-owning WGs | Reuses mechanisms; coordinates extensions and YANG review |
| Operator requirements and management integration | NMOP | Coordinates and uses operational experience |
| Cross-cutting operational guidance | OPSAWG | Coordinates and avoids duplicate documents |
| Agent discovery and naming | DAWN | Reuses |
| Agent-to-agent communication | AGENTPROTO | Reuses |
| Workload identity, authorization, and delegation | WIMSE, OAuth, and relevant Security-area WGs | Reuses |
| Generic agent delegation and interaction traceability | Related Security-area work, including the AUDIT effort | Coordinates with proponents; reuses applicable mechanisms without depending on a future AUDIT WG |
| Benchmarking terminology and methodology | BMWG | Coordinates; dispatches benchmarking work |
| AI-native architectures and research | NMRG and other IRTF groups | Coordinates; does not standardize |
| Supervision of agents acting on networks | Proposed AINETOPS, subject to the BoF venue decision | Develops agent-supervision specifications and supporting guidance |

AINETOPS will not standardize AI algorithms, models, training methods, prompts, chain-of-thought or other internal reasoning, general-purpose agent discovery or communication, MCP, A2A, or autonomous policy that bypasses existing security and change-management controls.

## What needs to be standardized?

Existing agent protocols and open-source automation platforms provide task management, lifecycle controls, and observability. AINETOPS will build on this experience to define a common management interface and operational semantics that operators can use across independently developed products, without depending on a particular automation platform.

The initial standards work will specify how a supervising management system can:

- Determine an agent’s operational state and supported supervision capabilities.
- Associate agent tasks with the network operations and resources they affect.
- Request intervention and distinguish acceptance of the request from its actual effect.
- Identify operations that remain in progress after a task is suspended or terminated.
- Report confirmed network changes, failures, and outcomes that remain unknown.

The specifications will define the data models, operations, notifications, protocol bindings, and required behavior needed for interoperable implementations. They will reuse existing task, identity, authorization, and telemetry mechanisms, with explicit mappings where applicable.

The intended result is a common specification that operators can reference in procurement and that vendors can implement and test against. Operator deployment scenarios and implementation experience will guide the work, with new definitions limited to demonstrated interoperability needs.

**Open question for the BoF:** Do existing mechanisms allow a supervising system to determine consistently across implementations which network operations have completed, which remain in progress, and which outcomes are unknown after an agent task is suspended or terminated? If not, what additional information or behavior requires standardization?

## Proposed working-group deliverables

The work is organized into three groups: operational experience and requirements, Standards Track specifications, and operational guidance. These activities will proceed in parallel, with operational evidence and implementation feedback informing the specifications as they develop.

### 1. Operational experience and requirements

**A. Report on existing operational approaches**

Collect and document how network operators, vendors, and open-source developers deploy or plan to use AI-based agents in network management.

Contributions will use a short common template covering the operational problem, deployment stage, participating components, management interfaces and boundaries, applicable policies, and experience with existing mechanisms or workarounds. Reports will distinguish production experience, trials, and planned capabilities.

The collection will preserve contributors’ terminology and architectural choices without requiring a unified taxonomy. Inclusion does not imply working-group endorsement.

**B. Survey of operational experience and needs**

Use the initial reports in 1.A and existing survey work to develop and refine a structured questionnaire for broader participation by network operators, vendors, and open-source developers.

The survey will collect comparable responses about deployments, plans, supervision mechanisms, integration difficulties, and unmet needs. It will distinguish observed problems from anticipated needs and capture cases where existing mechanisms are sufficient.

A summary will describe the respondent population, collection method, findings, and limitations. The reports and survey results will be maintained as supporting material; separate RFC publication is not required.

**C. Operational Framework and Requirements**

An Informational document defining the operational problem, roles, management boundaries, and requirements supporting the Standards Track work. Drawing on the reports and survey findings, it will identify existing mechanisms to reuse and interoperability gaps requiring additional specification.

This document will develop alongside the specifications. Completion of the reports or survey is not a prerequisite for starting Standards Track work.

### 2. Standards Track specifications

**A. Agent Operational State and Lifecycle**

A Standards Track specification defining supported management capabilities, administrative and operational state, and lifecycle management of network-management agents.

YANG is the leading candidate for the data model, with the choice evaluated against operator requirements and implementation experience. The specification will include at least one mandatory interoperable binding to an existing protocol. It will reuse existing identity and access-control mechanisms and will not define general agent discovery or internal AI-model management.

**B. Agent Task Supervision and Intervention**

A Standards Track specification defining data models, operations, notifications, and required behavior for task scope and constraints, progress and outcome reporting, approval, suspension, resumption, and termination.

It will distinguish an intervention request, its acceptance or rejection, and its observed effect. It will report associated network operations that have completed, remain in progress, have failed, or have unknown outcomes, and provide references correlating tasks with resulting actions and network changes.

The work will evaluate YANG-based management, reuse of existing task protocols, and an HTTP/JSON interface against the requirements. The specification will include at least one mandatory interoperable binding selected during the initial work. New definitions will be limited to demonstrated interoperability gaps.

### 3. Operational guidance

An Informational document covering least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment, informed by operational reports, survey findings, and implementation experience.

The guidance will explain how to apply the supervision mechanisms defined in Group 2, including their limitations. Suspending or terminating an agent task does not necessarily stop or reverse a network operation already accepted by a tool or controller. The guidance will address continuing operations and uncertain outcomes without implying automatic rollback.

The initial charter includes Standards Track specifications for agent operational state and lifecycle, and for task supervision and intervention. The choice of data-model language and protocol binding will be evaluated separately for each deliverable, without deferring standards work to a future recharter. AINETOPS will develop these specifications in coordination with NETMOD, NETCONF, NMOP, and relevant model-owning working groups, reusing existing models and mechanisms where applicable. Changes to existing management protocols or models owned by other working groups will be developed with those groups. New transport protocols, general-purpose agent protocols, and work beyond this agent-supervision scope require rechartering.

The ICON problem-statement and requirements drafts, the [agent lifecycle management draft](https://datatracker.ietf.org/doc/draft-sun-nmop-agent-lifecycle-management/), the [NMA A2U YANG draft](https://datatracker.ietf.org/doc/draft-zhao-nmop-nma-a2u-yang/), and the AINETOPS use-case inventory are potential inputs. The BoF will discuss their fit to the two Standards Track work items; naming them does not endorse their complete scope or design. Listing a draft as an input does not imply working-group adoption.

Draft charter: https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-Proposed-Charter.md

## Proposed agenda (120 minutes)

| Time | Topic | Presenter |
|---:|---|---|
| 10 min | Note Well, agenda, BoF purpose, and desired outcomes | Chairs |
| 15 min | Problem statement: the multi-vendor operator gap | Operator |
| 20 min | Production or trial deployment experience | Operator(s) |
| 10 min | Existing IETF building blocks and scope boundaries | Chairs |
| 10 min | IETF 126 Hackathon implementation report | Implementers |
| 10 min | Proposed charter and Standards Track deliverables | Proponents |
| 15 min | Candidate models, protocol bindings, and implementation interest | Authors and implementers |
| 20 min | Charter discussion and resolution of open issues | Chairs |
| 10 min | Sense of the room and next steps | Chairs and AD |

The agenda puts operator experience before proposed solutions and discusses the boundaries with adjacent work before the deliverables.

## Questions for the room

1. Is there a clear operational need for interoperable supervision of network-management agents across vendors, including reporting their actions and intervening in running tasks?
2. Is the proposed boundary—between supervising management systems and network-management agents—clear and sufficiently focused?
3. Is there support for developing each of the following Standards Track work items?

   - Agent operational state and lifecycle management.
   - Agent task supervision and intervention.

4. Is YANG an appropriate leading candidate for agent operational state and lifecycle? For task supervision and intervention, which approach best meets the requirements: YANG-based management, reuse of an existing task protocol, or an HTTP/JSON interface? Each work item will include at least one mandatory interoperable binding.
5. Should this work proceed in a dedicated AINETOPS working group, or within an existing working group such as NMOP or OPSAWG?
6. Who is willing to contribute text or review the specifications, and for which work item?
7. Who is willing to implement the specifications and participate in interoperability testing?
8. Which operators can contribute deployment scenarios, requirements, and implementation feedback?

The chairs should distinguish objections to the problem, scope, technical approach, and organizational venue. Support for the two Standards Track work items should be assessed separately, and specific contributor commitments should be recorded.

These questions should be posted to the mailing list before the BoF and refined with the chairs and responsible AD, following RFC 5434.

## Links

- Mailing list: https://mailman3.ietf.org/mailman3/lists/ainetops.ietf.org/
- Archive: https://mailarchive.ietf.org/arch/browse/ainetops/
- AI in OPS coordination page: https://wiki.ietf.org/en/group/ops/aiops
- Draft charter: https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-Proposed-Charter.md
- Related document inventory: https://github.com/IETF-OPS-AD/AINETOPS
- IETF 127 important dates: https://datatracker.ietf.org/meeting/127/important-dates/

## Open items before submission

The initial IETF 127 BoF request is due **18 September 2026**. Revised requests are due to Area Directors by **2 October 2026**, and Area Director approval is due by **9 October 2026**.

Before submission:

- Confirm AD support and the submission path with Mahesh.
- Identify credible chair candidates privately for consideration by the AD.
- Confirm at least two named operator or implementer presenters with deployment experience.
- Coordinate with proponents of related security and agent work, including AUDIT. The AUDIT BoF request was resubmitted for IETF 127 and is included as a scheduling conflict; AINETOPS does not depend on the formation of an AUDIT working group.
- Confirm candidate-model authors and implementers for the two Standards Track work items, and coordinate ownership with the relevant chairs and ADs.
- Confirm the expected attendance and session-conflict list.
