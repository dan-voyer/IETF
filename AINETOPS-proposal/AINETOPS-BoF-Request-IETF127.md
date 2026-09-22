# AINETOPS BoF Request — IETF 127

## Name

AI-enabled Network Operations (AINETOPS)

## Description

AI-based agents can carry out multi-step network-management tasks through tools, controllers, and existing management protocols. When independently developed products are involved, operators need consistent ways to determine an agent's state and authority, follow its tasks, intervene, and relate its actions to resulting network changes. These supervisory interfaces and their operational meaning are often implementation-specific.

For example, terminating an agent task may stop new actions while a controller continues applying a change already accepted. A supervising system needs to distinguish acceptance of the intervention from its actual effect and identify downstream operations that completed, remain active, failed, or have unknown outcomes. The BoF will examine whether existing mechanisms provide this information consistently across implementations and where additional specification is justified.

AINETOPS proposes two Standards Track specifications at the boundary between supervising management systems and network-management agents: agent operational state and lifecycle, and task supervision and intervention. This WG-forming BoF will assess the problem, scope, proposed deliverables, contributor interest, and whether a dedicated working group or an existing venue is appropriate.

## Required Details

- **Status:** WG-forming
- **Area:** Operations and Management
- **Responsible AD:** Mahesh Jethanandani — confirmation pending
- **BoF chairs:** TBD with the responsible AD
- **BoF proponents:** TBD
- **Expected attendance:** 80–120
- **Session length:** 2 hours
- **Chair conflicts:** TBD
- **Technology overlap:** NMOP, OPSAWG, NETCONF, NETMOD, ANIMA, BMWG, NMRG, DAWN, AGENTPROTO, AUDIT
- **Key participant conflicts:** TBD

## Information for the IAB and IESG

**Existing protocols and practices.** NETCONF, RESTCONF, YANG, NACM, and telemetry mechanisms provide network access and controls. ANIMA provides relevant autonomic-agent lifecycle concepts. Agent frameworks such as MCP and A2A provide tools, tasks, and communication mechanisms. The work will identify which supervision requirements these mechanisms already meet and limit new definitions to demonstrated interoperability gaps.

**Modifications and new specifications.** The proposed work defines management data, operations, notifications, and required behavior using existing protocols and security mechanisms. Each Standards Track specification will include at least one mandatory interoperable binding. YANG is the leading candidate for lifecycle management; task supervision will also evaluate reuse of existing task protocols and HTTP/JSON interfaces. No new transport or general-purpose agent protocol is proposed.

**Scope and coordination.** The proposed group would maintain consistency between lifecycle state, task intervention, and downstream-operation reporting. It would coordinate with NMOP and OPSAWG on operational requirements, NETMOD and NETCONF on management models and bindings, and relevant agent and Security-area groups on mechanisms to reuse. Changes to protocols or models owned elsewhere will be developed with their responsible groups. AI algorithms, training, prompts, internal reasoning, general agent discovery and communication, and general identity or authorization mechanisms are outside scope. Existing access-control and change-management authority will be preserved.

**Implementation experience and open-source coordination.** The Agent Observability for Network Management Operations project at the IETF 126 Hackathon provides relevant implementation experience. Operator and implementer presentations will examine deployments, trials, and remaining integration problems. Reports, a [draft survey questionnaire](https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/Survey_AI-Enabled_Network_Operations.md), and participation from open-source developers will inform requirements and interoperability testing. Survey findings will distinguish observed problems from anticipated needs and include cases where existing mechanisms suffice; they do not establish IETF consensus. Specific presenters and implementation references remain to be confirmed.

## Proposed Working-Group Deliverables

### 1. Operational experience and requirements

- **A. Operational reports:** Collect deployment experience and plans from operators, vendors, and open-source developers using a common template, while preserving their terminology and architectural choices.
- **B. Survey:** Refine the questionnaire using these reports and summarize comparable responses, distinguishing production, trials, and plans, with the collection method and limitations documented.
- **C. Operational Framework and Requirements (Informational):** Define roles, management boundaries, requirements, reusable mechanisms, and interoperability gaps, informed by the reports and survey.

Reports and survey results are supporting material; separate RFC publication is not required. Evidence gathering, requirements, and specifications will proceed in parallel.

### 2. Standards Track specifications

- **A. Agent Operational State and Lifecycle:** Specify supported management capabilities, administrative and operational state, and agent lifecycle management, reusing existing identity and access-control mechanisms.
- **B. Agent Task Supervision and Intervention:** Specify task scope and constraints, progress and outcomes, approval, suspension, resumption, and termination, including acknowledgements, observed effects, and references correlating tasks with actions and network changes.

The specifications will distinguish agent-task state from downstream-operation state and report continuing or uncertain outcomes. Suspending or terminating a task does not imply that accepted network operations stop or that completed changes are rolled back.

### 3. Operational guidance

An Informational document covering least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment, informed by operational and implementation experience.

## Proposed Agenda — 120 Minutes

| Time | Topic | Presenter |
| ---: | --- | --- |
| 10 min | Note Well, purpose, and problem framing | Chairs |
| 30 min | Operator experience and implementation reports | Operators / implementers, TBD |
| 15 min | Existing mechanisms, interoperability gaps, and coordination | Contributors, TBD |
| 20 min | Proposed scope and three deliverable groups | Proponents |
| 30 min | Discussion of scope, technical direction, and venue | Chairs |
| 15 min | Sense of the room and contributor commitments | Chairs / AD |

## Decisions Sought

The BoF will assess whether the operational problem and scope are clear, whether each Standards Track work item has support, and which venue should undertake the work. It will identify people willing to supply operational evidence, write or review specifications, implement, and participate in interoperability testing. Support for the two Standards Track items and contributor commitments will be recorded separately.

## Supporting Material

- [Mailing list](https://mailman3.ietf.org/mailman3/lists/ainetops.ietf.org/) and [archive](https://mailarchive.ietf.org/arch/browse/ainetops/)
- [Detailed BoF proposal, including discussion questions](https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-BoF-Proposal-IETF127.md)
- [Proposed charter](https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-Proposed-Charter.md)
- [AINETOPS problem-statement working text](https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/draft-xxx-ainetops-problem-statement-00-v1.md)
- [Related document inventory](https://github.com/IETF-OPS-AD/AINETOPS), including potential inputs on use cases, ICON requirements, agent lifecycle, and agent-management models. Listing an input does not imply adoption or endorsement of its full scope.
