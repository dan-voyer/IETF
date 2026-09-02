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

The initial work will define the operational framework, practices, and requirements before assuming a protocol or data-model solution. If the resulting gap analysis identifies a need to extend an existing protocol or YANG model, that work will be dispatched to the group responsible for it.

### What entirely new protocols or practices are required?

No new protocol is proposed in the initial charter. The proposed outputs are an operational framework, a Best Current Practice document, and a requirements and gap analysis. The working group would need to be rechartered before taking on protocol or YANG-module development itself.

### What implementation experience exists?

The Agent Observability for Network Management Operations project at the IETF 126 Hackathon exercised an observability framework for network-management agents and informed the ICON problem-statement and requirements drafts. The BoF should also include operational experience from organizations deploying or evaluating agents that can take network actions.

## Problem statement

AI-based systems are moving beyond advising network operators. They can now plan and execute multi-step operational tasks, including making changes through existing management systems and protocols.

Consider an operator using agents and management tools from several vendors. The operator needs to know which devices, resources, data, and actions an agent is allowed to use; which task and policy authorized an action; what the agent is doing now; and how to approve, restrict, suspend, redirect, or stop the task. Afterward, the operator needs a record that relates the agent's actions and the resulting network changes to the original objective.

Today, those controls and records are implementation-specific. Existing network-management protocols expose the network, but they do not by themselves provide a common way to supervise the autonomous, multi-step behavior of the system using them. This makes safe multi-vendor deployment difficult and weakens operational accountability when something goes wrong.

AINETOPS addresses that operational gap. Its scope is the boundary between an AI-based agent and the network-management environment—not the agent's internal model, prompts, training, or reasoning method.

## Why the IETF, and why a new working group?

The problem occurs when agent-based systems use IETF management protocols, data models, and security mechanisms to observe or change networks. A useful approach must work across vendors while preserving the authority of existing access-control, security, and change-management systems.

Several IETF groups own important parts of the solution, but no single group owns the cross-protocol operational problem of supervising agents acting on networks:

| Concern | Primary venue | AINETOPS relationship |
|---|---|---|
| Network-management protocols and YANG models | NETCONF, NETMOD, and relevant model-owning WGs | Identifies requirements; dispatches extensions |
| Operator requirements and management integration | NMOP | Coordinates and uses operational experience |
| Cross-cutting operational guidance | OPSAWG | Coordinates and avoids duplicate documents |
| Agent discovery and naming | DAWN | Reuses |
| Agent-to-agent communication | AGENTPROTO | Reuses |
| Workload identity, authorization, and delegation | WIMSE, OAuth, and relevant Security-area WGs | Reuses |
| Generic agent delegation and interaction traceability | AUDIT, if formed, and related work | Reuses; profiles only where network operations require it |
| Benchmarking terminology and methodology | BMWG | Coordinates; dispatches benchmarking work |
| AI-native architectures and research | NMRG and other IRTF groups | Coordinates; does not standardize |
| Supervision of agents acting on networks | No single existing venue | Proposed AINETOPS focus |

AINETOPS will not standardize AI algorithms, models, training methods, prompts, chain-of-thought or other internal reasoning, general-purpose agent discovery or communication, MCP, A2A, or autonomous policy that bypasses existing security and change-management controls.

## Proposed working-group deliverables

1. **AINETOPS Operational Framework** — An Informational document defining the operational problem, terminology, roles, boundaries, and the relationship between AI-based agents and existing network-management systems.

2. **Operational Practices for Network-Management Agents** — A Best Current Practice document covering admission, least privilege, task supervision, observability, intervention, failure containment, recovery, auditability, human oversight, and retirement.

3. **Requirements and Gap Analysis** — An Informational document identifying requirements placed on existing IETF management protocols and data models when they are used by AI-based agents. Protocol and data-model extensions will be dispatched to the responsible working groups.

The ICON problem-statement and requirements drafts, the network-management-agent drafts discussed in NMOP, and the AINETOPS use-case inventory are potential inputs. Listing a draft as an input does not imply working-group adoption.

Draft charter: https://github.com/dan-voyer/IETF/blob/main/AINETOPS-proposal/AINETOPS-Proposed-Charter.md

## Proposed agenda (120 minutes)

| Time | Topic | Presenter |
|---:|---|---|
| 10 min | Note Well, agenda, BoF purpose, and desired outcomes | Chairs |
| 15 min | Problem statement: the multi-vendor operator gap | Operator |
| 20 min | Production or trial deployment experience | Operator(s) |
| 10 min | Existing IETF building blocks and scope boundaries | Chairs |
| 10 min | IETF 126 Hackathon implementation report | Implementers |
| 15 min | Proposed charter, deliverables, and candidate inputs | Proponents |
| 30 min | Charter discussion and resolution of open issues | Chairs |
| 10 min | Sense of the room and next steps | Chairs and AD |

The agenda puts operator experience before proposed solutions and discusses the boundaries with adjacent work before the deliverables.

## Questions for the room

1. Is the operational problem well understood, solvable, and worth solving?
2. Is there a clear need for vendor-neutral operational guidance or interoperability?
3. Is the IETF the right venue?
4. Is the proposed scope narrow enough, and are the boundaries with existing groups clear?
5. Are the proposed deliverables appropriate?
6. Should a working group be formed with this charter?
7. Who is willing to author or review the work?
8. Who is willing to implement or provide operational experience?

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
- Coordinate with the proponents of AUDIT and other adjacent agent work.
- Confirm the authors' support before naming individual drafts as proposed inputs.
- Confirm the expected attendance and session-conflict list.
