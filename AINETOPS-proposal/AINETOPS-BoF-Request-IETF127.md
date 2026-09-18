# AINETOPS BoF Request — IETF 127

> **Submission-ready draft for the IETF Datatracker.**
>
> Proposed BoF: **AI-enabled Network Operations (AINETOPS)**
>
> Status: **WG-forming**
>
> This document is intended to be copied into the IETF BoF Request Tool and refined with the responsible Area Director. Items marked **TBD before submission** require confirmation.

## Name

**AI-enabled Network Operations (AINETOPS)**

## Description

AI-based systems are moving beyond assisting network operators. They are increasingly able to plan and execute multi-step operational tasks, including making changes through existing network-management systems and protocols.

Existing IETF protocols provide access to network configuration and operational state, but they were not designed to provide a common way to supervise an autonomous agent carrying out a multi-step operational task. In a multi-vendor environment, an operator may not have a consistent way to determine what an agent is allowed to do, follow and attribute the actions it takes, intervene while a task is running, or relate resulting network changes to the original objective and policy decision.

AINETOPS proposes to standardize the management interface between a supervising management system and network-management agents from different vendors. The interface would provide consistent agent state, task operations, notifications, and operational semantics using existing IETF management protocols and security mechanisms wherever possible.

The proposed scope is deliberately narrow. AINETOPS focuses on the boundary between an AI-based network-management agent and the network-management environment. It does not standardize AI algorithms, models, prompts, training methods, internal reasoning, general-purpose agent discovery, agent-to-agent communication, or a new transport protocol.

The goal of this WG-forming BoF is to determine whether there is IETF consensus on the operational problem, the proposed scope, the initial Standards Track deliverables, and the appropriate venue for the work.

## Required Details

- **Status:** WG-forming
- **Area:** Operations and Management
- **Responsible AD:** Mahesh Jethanandani — **confirm before submission**
- **BoF chairs:** **TBD with responsible AD**
- **BoF proponents:** **TBD before submission — add confirmed names and email addresses**
- **Number of people expected to attend:** 80–120
- **Length of session:** 2 hours

### Conflicts

**Chair conflicts:** TBD after chairs are selected.

**Technology overlap / conflicts to avoid:**

- NMOP
- OPSAWG
- NETCONF
- NETMOD
- ANIMA
- BMWG
- NMRG
- DAWN
- AGENTPROTO

**Key participant conflicts:** **TBD before submission**, based on confirmed presenters, proponents, and chairs.

## Information for the IAB and IESG

### What protocols or practices already exist in this space?

NETCONF, RESTCONF, YANG, NACM, YANG-Push, and other telemetry mechanisms already provide access to network configuration and operational state. ANIMA also provides relevant autonomic-networking concepts, including GRASP and the lifecycle concepts for Autonomic Service Agents.

Work elsewhere in the IETF is addressing adjacent topics such as agent discovery, communication, workload identity, authorization, delegation, and traceability. Implementations may also use external agent frameworks such as MCP or A2A. AINETOPS is intended to reuse applicable work rather than define another general-purpose agent protocol.

What is missing is a common operational approach for supervising an AI-based agent that can act on a production network. Implementations expose different ways to constrain an agent, observe its activity, intervene in a running task, and relate its actions to the operator's original objective and policy decisions.

### Which modifications to existing protocols or practices are required?

The proposed work will define the information models, data models, operations, notifications, protocol bindings, and required behavior needed for agent lifecycle management and task supervision.

The work will reuse existing IETF protocols and security mechanisms wherever possible. Requirements and gap analysis will guide model development in parallel. If extensions to existing protocols or data models owned by other working groups are necessary, those changes will be developed in coordination with the responsible working groups.

### Which entirely new protocols or practices are required?

No new transport or general-purpose AI-agent protocol is proposed.

The initial charter proposes two Standards Track specifications:

1. **Agent Operational State and Lifecycle**
2. **Agent Task Supervision and Intervention**

Each specification will define at least one mandatory interoperable binding using an existing protocol. The choice of data-model language and binding will be evaluated against operator requirements, existing IETF mechanisms, and implementation experience rather than predetermined for every work item.

An Operational Framework and Requirements document and implementation-informed Operational Guidance document will support the Standards Track work.

### Open-source projects or implementation experience

The **Agent Observability for Network Management Operations** project at the IETF 126 Hackathon exercised an observability framework for network-management agents and informed related problem-statement and requirements work.

The BoF should also include operational or implementation experience from organizations deploying, prototyping, or evaluating agents capable of taking network-management actions.

**TBD before final revision:** add confirmed open-source implementations, hackathon repositories, prototypes, and implementation contacts relevant to the two proposed Standards Track work items.

### Coordination with open-source work

AINETOPS should use implementation experience to validate interoperability requirements and avoid standardizing abstractions that are not needed at an implementation boundary.

The working group would coordinate with relevant open-source projects and implementation communities through common participants, hackathons, interoperability testing, and implementation reports. The IETF specifications would remain implementation-neutral.

## Problem Statement

Consider an operator using agents and management tools from several vendors. The operator needs to know:

- which devices, resources, data, and actions an agent is allowed to use;
- which task, objective, policy, and authorization context led to an action;
- what the agent is doing now;
- which network operations have completed, remain in progress, failed, or have an unknown outcome;
- how to approve, restrict, suspend, resume, redirect, or terminate a running task; and
- how to relate resulting network changes to the original operational objective.

Today, these controls and records are largely implementation-specific.

Existing network-management protocols expose the network, but they do not by themselves define a common supervisory interface for the autonomous, multi-step behavior of the system using them. This complicates multi-vendor deployment and makes consistent operational accountability difficult.

AINETOPS addresses this interoperability gap at the boundary between a supervising management system and network-management agents.

## Why the IETF, and Why a New Working Group?

The problem appears when agent-based systems use IETF management protocols, data models, and security mechanisms to observe or change networks. An interoperable solution must work across vendors while preserving the authority of existing access-control, security, and operational change-management systems.

AINETOPS is intended to define a focused work program that keeps the management models, operational framework, and deployment practices for agent supervision consistent across independently developed agents, tools, and controllers.

Related work will remain in its existing venues:

| Concern | Primary venue | AINETOPS relationship |
| --- | --- | --- |
| Existing network-management protocols and models | NETCONF, NETMOD, and relevant model-owning WGs | Reuse mechanisms and coordinate extensions |
| Operator requirements and management integration | NMOP | Coordinate and use operational experience |
| Cross-cutting operational guidance | OPSAWG | Coordinate and avoid duplication |
| Agent discovery and naming | DAWN and related work | Reuse |
| Agent-to-agent communication | AGENTPROTO and related work | Reuse |
| Identity, authentication, authorization, and delegation | Relevant Security-area WGs | Reuse |
| Benchmarking terminology and methodology | BMWG | Coordinate and dispatch benchmarking work |
| AI-native architectures and research | NMRG and other IRTF groups | Coordinate; do not duplicate research |
| Supervision of agents acting on networks | Proposed AINETOPS | Define interoperable agent-supervision specifications |

AINETOPS will not standardize AI algorithms, models, training methods, prompts, chain-of-thought or other internal reasoning, general-purpose agent discovery or communication, MCP, A2A, or autonomous policy mechanisms that bypass existing security and change-management controls.

## What Needs to Be Standardized?

The initial standards work will specify how a supervising management system can:

- determine an agent's operational state and supported supervision capabilities;
- associate an agent task with the network operations and resources it affects;
- carry the task identity, objective, constraints, and authorization context needed across the supervision boundary;
- request an intervention and distinguish acceptance of the request from its actual operational effect;
- distinguish task state from the state of downstream network operations;
- identify operations that remain in progress after a task is suspended or terminated;
- report confirmed network changes, failures, and outcomes that remain unknown; and
- correlate resulting actions and network changes with the original task.

The specifications will define interoperable data and behavior at the management boundary while leaving internal agent implementation choices unspecified.

### Open technical question for the BoF

Do existing mechanisms allow a supervising system to determine consistently across implementations which network operations have completed, which remain in progress, and which outcomes are unknown after an agent task is suspended or terminated?

If not, what additional information or behavior requires standardization?

## Proposed Working-Group Deliverables

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

## Proposed Agenda — 120 Minutes

| Time | Topic | Presenter |
| ---: | --- | --- |
| 10 min | Note Well, agenda, BoF purpose, and desired outcomes | Chairs |
| 15 min | Problem statement: the multi-vendor operator gap | **Named operator TBD** |
| 20 min | Production or trial deployment experience | **Named operator(s) / implementer(s) TBD** |
| 10 min | Existing IETF building blocks and scope boundaries | Chairs |
| 10 min | IETF 126 Hackathon implementation report | **Named implementer TBD** |
| 10 min | Proposed charter and Standards Track deliverables | Proponents |
| 15 min | Candidate models, protocol bindings, and implementation interest | Authors / implementers |
| 20 min | Charter discussion and resolution of open issues | Chairs |
| 10 min | Sense of the room and next steps | Chairs and AD |

The agenda deliberately puts operator experience before proposed solutions and establishes the boundaries with adjacent IETF work before discussing deliverables.

## Questions for the Room

1. Is there a clear operational need for interoperable supervision of network-management agents across vendors, including reporting their actions and intervening in running tasks?

2. Is the proposed boundary — between supervising management systems and network-management agents — clear and sufficiently focused?

3. Is there support for developing each of the following Standards Track work items?
   - Agent operational state and lifecycle.
   - Agent task supervision and intervention.

4. For agent operational state and lifecycle, is YANG an appropriate leading candidate? For task supervision and intervention, which approach best meets the requirements: YANG-based management, reuse of an existing task protocol, or an HTTP/JSON interface?

5. Should this work proceed in a dedicated AINETOPS working group, or should some or all of it be handled in existing working groups such as NMOP, OPSAWG, NETCONF, or NETMOD?

6. Who is willing to contribute text or review the specifications, and for which work item?

7. Who is willing to implement the specifications and participate in interoperability testing?

8. Which operators can contribute deployment scenarios, requirements, and implementation feedback?

The chairs should distinguish objections to the problem, scope, technical approach, and organizational venue. Support for the two Standards Track work items should be assessed separately, and concrete contributor and implementation commitments should be recorded.

## Links

- **Mailing list:** https://mailman3.ietf.org/mailman3/lists/ainetops.ietf.org/
- **Mailing-list archive:** https://mailarchive.ietf.org/arch/browse/ainetops/
- **AI in OPS coordination page:** https://wiki.ietf.org/en/group/ops/aiops
- **Draft charter:** https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-Proposed-Charter.md
- **Related document inventory:** https://github.com/IETF-OPS-AD/AINETOPS
- **AINETOPS use cases:** https://datatracker.ietf.org/doc/draft-king-rokui-ainetops-usecases/
- **IETF 127 important dates:** https://datatracker.ietf.org/meeting/127/important-dates/

### Potential Input Documents

The following documents may provide input to the work. Listing a document here does not imply adoption of its complete scope or design by a future working group:

- AINETOPS use-case work.
- ICON problem-statement and requirements work.
- Agent lifecycle management work.
- NMA A2U / agent-management YANG work.
- Relevant agent observability and IETF Hackathon implementation material.

**TBD before final revision:** replace the descriptive entries above with the confirmed Datatracker URLs for the documents that proponents want to cite in the submitted request.

## Out of Scope

AINETOPS will not:

- standardize AI or machine-learning algorithms, models, training methods, prompts, or internal reasoning techniques;
- require disclosure or standardization of chain-of-thought or other internal model reasoning;
- define a general-purpose AI-agent architecture;
- define a general-purpose agent-to-agent communication protocol;
- define general agent discovery, naming, identity, authentication, authorization, delegation, or credential mechanisms;
- standardize MCP or A2A;
- define a new transport protocol for agents;
- replace existing network access-control, policy, or change-management systems; or
- standardize autonomous policy mechanisms that bypass existing security controls.

## Submission Checklist

Before filing the initial request:

- [ ] Confirm the responsible AD and that the AD supports entering the request.
- [ ] Add confirmed BoF proponents and email addresses.
- [ ] Agree on BoF chair candidates with the responsible AD.
- [ ] Confirm at least two named operator or implementer presenters with real deployment, trial, prototype, or Hackathon experience.
- [ ] Confirm the expected attendance.
- [ ] Convert the scheduling-conflict list into chair, technology-overlap, and key-participant conflicts.
- [ ] Confirm which candidate Internet-Drafts should be listed as inputs.
- [ ] Add concrete open-source repositories/implementations where available.
- [ ] Cross-check the proposed charter against the final BoF request.
- [ ] Submit the initial BoF request by **18 September 2026**.
- [ ] Incorporate community/AD feedback and submit revisions by **2 October 2026**.
- [ ] Target AD approval by **9 October 2026**.

## Notes for the Datatracker Editor

This request should remain **WG-forming**.

The initial submission does not need to settle every technical choice. In particular, the choice of YANG versus another representation/binding for each deliverable is intentionally left as a technical decision to be validated against interoperability requirements and implementation experience.

The initial request should nevertheless demonstrate:

1. a concrete interoperability problem;
2. a narrow boundary that can be chartered;
3. credible Standards Track deliverables;
4. operator and implementation interest; and
5. clear coordination boundaries with adjacent IETF work.
