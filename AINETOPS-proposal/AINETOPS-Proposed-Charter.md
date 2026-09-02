# AI-enabled Network Operations (AINETOPS) Working Group Charter

**Area:** Operations and Management
**Mailing list:** [ainetops@ietf.org](mailto:ainetops@ietf.org)
**Mailing-list archive:** https://mailarchive.ietf.org/arch/browse/ainetops/

> **Status: proposal for discussion.** No AINETOPS working group currently exists. This text does not represent Area Director, IESG, or IETF consensus and is expected to change through the BoF and chartering process.

## Objective

AI-based systems are moving beyond assisting network operators. They are increasingly able to plan and execute multi-step operational tasks, including making changes through existing network-management systems and protocols.

Existing IETF protocols provide access to network configuration and operational state, but they were not designed to supervise an autonomous agent carrying out a task. In a multi-vendor environment, an operator may not have a consistent way to determine what an agent is allowed to do, follow and attribute the actions it takes, intervene while a task is running, or relate the resulting network changes to the original objective and policy decision.

The AINETOPS Working Group will address this operational gap. Its focus is the boundary between AI-based agents and the existing network-management environment, not the internal design of the AI system.

## Scope

AINETOPS will bring together operators, implementers, and protocol experts to develop a common operational framework and deployment guidance for AI-based agents that can act on production networks.

The work includes:

* Defining the operational roles and responsibilities of network-management agents, supervising systems, tools, controllers, policy systems, and human operators.
* Describing how the objective, scope, constraints, authorization context, and task identity of an operation remain available as work passes between agents, tools, and management systems.
* Describing the information needed to observe and attribute an agent’s actions and relate them to resulting network changes.
* Defining the operational capabilities needed for an operator or policy system to approve, restrict, suspend, redirect, or terminate an agent task.
* Describing the state and lifecycle information needed to admit, supervise, update, suspend, recover, and retire an agent.
* Developing operational guidance for least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment.
* Identifying requirements and gaps in existing IETF management protocols and data models when they are used by AI-based agents.

AINETOPS will reuse existing IETF management protocols, data models, security mechanisms, and trace-context mechanisms wherever possible. It will distinguish information that must cross an interoperability boundary from information that may remain implementation-specific.

The initial work is requirements- and operations-focused. If it identifies a need for a new protocol, a substantial protocol extension, or a YANG module, that work will be coordinated with and dispatched to the working group responsible for the affected protocol or modelling area. AINETOPS must be rechartered before undertaking such standards-track work itself.

## Out of Scope

AINETOPS will not:

* Standardize AI or machine-learning algorithms, models, training methods, prompts, or internal reasoning techniques.
* Require disclosure or standardization of chain-of-thought or other internal model reasoning.
* Define a general-purpose AI-agent architecture or agent-to-agent communication protocol.
* Define general agent discovery, naming, identity, authentication, authorization, delegation, or credential mechanisms.
* Standardize MCP, A2A, or another externally maintained agent framework.
* Redefine network, service, topology, telemetry, anomaly, incident, or configuration models owned by other working groups.
* Develop benchmarking terminology or methodology.
* Authorize agents to bypass existing security, policy, access-control, or change-management mechanisms.

AINETOPS may describe requirements placed on work in these areas, but specifications that belong to another working group or standards organization will be developed there.

## Deliverables

The initial work of AINETOPS will consist of three documents:

### 1. AINETOPS Operational Framework

An Informational document defining the operational problem, terminology, roles, trust and management boundaries, and the relationship between AI-based agents and existing network-management systems.

### 2. Operational Practices for Network-Management Agents

A Best Current Practice document covering admission, least privilege, task supervision, observability, intervention, failure containment, recovery, auditability, human oversight, lifecycle management, and incremental deployment.

### 3. Requirements and Gap Analysis

An Informational document identifying requirements placed on existing IETF management protocols and data models when they are used by AI-based agents. It will document which requirements are met by existing mechanisms and dispatch unmet protocol or data-model requirements to the responsible working groups.

Existing individual Internet-Drafts may be considered as input. Listing or discussing an individual draft does not imply working-group adoption.

## Relationships with Other Groups

AINETOPS will coordinate with:

* **NMOP** on operator requirements, operational models, experiments, and network-management integration.
* **OPSAWG** on operational guidance and work spanning multiple Operations and Management Area technologies.
* **NETMOD, NETCONF, and relevant model-owning working groups** on YANG models and existing management protocols.
* **ANIMA** on autonomic-networking concepts and the lifecycle guidance for Autonomic Service Agents in RFC 9222.
* **DAWN** on agent discovery and naming.
* **AGENTPROTO** on general agent-to-agent communication.
* **WIMSE, OAuth, and relevant Security Area groups** on workload identity, authentication, authorization, and delegation.
* **AUDIT, if formed, SCITT, and related work** on generic audit semantics, traceability, and transparency mechanisms.
* **BMWG** on benchmarking terminology and methodology.
* **NMRG and other IRTF groups** on research concerning AI-native architectures, semantic models, ontologies, and inference.

AINETOPS will reuse the output of these groups rather than duplicate it. Work that fits an existing working-group charter will be sent there rather than adopted by AINETOPS.

## Milestones

The dates below are relative to charter approval and will be replaced with calendar dates during chartering.

| Time from chartering | Milestone                                                                                         |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| 6 months             | Adopt the AINETOPS Operational Framework document.                                                |
| 9 months             | Adopt the Operational Practices document.                                                         |
| 12 months            | Adopt the Requirements and Gap Analysis document.                                                 |
| 18 months            | Submit the AINETOPS Operational Framework to the IESG for publication as Informational.           |
| 24 months            | Submit the Requirements and Gap Analysis to the IESG for publication as Informational.            |
| 30 months            | Submit the Operational Practices document to the IESG for publication as BCP; recharter or close. |

The working group will request rechartering if the requirements and gap analysis demonstrates community support for work that falls outside this initial scope.
