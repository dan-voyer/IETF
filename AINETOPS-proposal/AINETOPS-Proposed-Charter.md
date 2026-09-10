# AI-enabled Network Operations (AINETOPS) Working Group Charter

**Area:** Operations and Management
**Mailing list:** [ainetops@ietf.org](mailto:ainetops@ietf.org)
**Mailing-list archive:** https://mailarchive.ietf.org/arch/browse/ainetops/

> **Status: proposal for discussion.** No AINETOPS working group currently exists. This text does not represent Area Director, IESG, or IETF consensus and is expected to change through the BoF and chartering process.

## Objective

AI-based systems are moving beyond assisting network operators. They are increasingly able to plan and execute multi-step operational tasks, including making changes through existing network-management systems and protocols.

Existing IETF protocols provide access to network configuration and operational state, but they were not designed to supervise an autonomous agent carrying out a task. In a multi-vendor environment, an operator may not have a consistent way to determine what an agent is allowed to do, follow and attribute the actions it takes, intervene while a task is running, or relate the resulting network changes to the original objective and policy decision.

The AINETOPS Working Group will address this operational gap. AINETOPS will standardize the management interface between a supervising management system and network-management agents from different vendors. The interface will provide consistent agent state, task operations, and notifications using existing IETF management protocols. Its focus is the boundary between AI-based agents and the existing network-management environment, not the internal design of the AI system.

## Scope

AINETOPS will bring together operators, implementers, and protocol experts to develop interoperable agent-management YANG models, a supporting operational framework, and deployment guidance for AI-based agents that can act on production networks.

The work includes:

* Standardizing agent operational state and lifecycle, and task supervision and intervention, through YANG data models, operations, and notifications.

* Defining the operational roles and responsibilities of network-management agents, supervising systems, tools, controllers, policy systems, and human operators.
* Describing how the objective, scope, constraints, authorization context, and task identity of an operation remain available as work passes between agents, tools, and management systems.
* Describing the information needed to observe and attribute an agent’s actions and relate them to resulting network changes.
* Defining the operational capabilities needed for an operator or policy system to approve, restrict, suspend, resume, or terminate an agent task.
* Describing the state and lifecycle information needed to admit, supervise, update, suspend, recover, and retire an agent.
* Developing operational guidance for least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment.
* Identifying requirements and gaps in existing IETF management protocols and data models when they are used by AI-based agents.

AINETOPS will reuse existing IETF management protocols, data models, security mechanisms, and trace-context mechanisms wherever possible. It will distinguish information that must cross an interoperability boundary from information that may remain implementation-specific.

The initial charter includes Standards Track YANG models for agent operational state and lifecycle, and for task supervision and intervention. AINETOPS will develop these models in coordination with NETMOD, NETCONF, NMOP, and relevant model-owning working groups, reusing existing models and mechanisms where applicable. Changes to existing management protocols or models owned by other working groups will be developed with those groups. New transport protocols, general-purpose agent protocols, and work beyond this agent-supervision scope require rechartering.

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

The initial work of AINETOPS will consist of four documents:

1. **Operational Framework and Requirements** — An Informational document defining the operational problem, roles, management boundaries, and requirements supporting the Standards Track work. It will identify existing mechanisms to reuse and the gaps addressed by the models. This work will proceed alongside model development rather than defer it to a future recharter.

2. **Agent Operational State and Lifecycle** — A Standards Track specification defining YANG data models for supported management capabilities, administrative and operational state, and lifecycle management of network-management agents. It will reuse existing identity and access-control mechanisms and will not define general agent discovery or internal AI-model management.

3. **Agent Task Supervision and Intervention** — A Standards Track specification defining YANG data models, operations, and notifications for task scope and constraints, progress and outcome reporting, approval, suspension, resumption, and termination. It will define intervention acknowledgements and outcomes, including incomplete or continuing network operations, and references that correlate tasks with resulting actions.

4. **Operational Guidance** — An Informational document covering least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment, informed by implementation and operational experience.

Suspending or terminating an agent task does not necessarily stop or reverse a network operation already accepted by a tool or controller. The specifications will distinguish the requested intervention, its acceptance or rejection, and its observed outcome, and report operations that remain in progress or whose outcome is unknown. They will not imply automatic rollback.

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
* **SCITT and related security work, including the AUDIT proponents**, on generic audit semantics, traceability, and transparency mechanisms. The declined AUDIT BoF request is related work, not an established WG or a dependency on future WG formation.
* **BMWG** on benchmarking terminology and methodology.
* **NMRG and other IRTF groups** on research concerning AI-native architectures, semantic models, ontologies, and inference.

AINETOPS will reuse applicable outputs of these groups and coordinate overlapping work with their chairs and responsible ADs. It will own the agent-supervision models specified here; extensions to existing protocols or models owned by other groups will be developed with those groups.

## Milestones

The dates below are relative to charter approval and will be replaced with calendar dates during chartering.

| Time from chartering | Milestone |
|---|---|
| 6 months | Adopt the Operational Framework and Requirements document and initial drafts for both Standards Track model specifications. |
| 12 months | Adopt the Operational Guidance document and review implementation experience for both model specifications. |
| 18 months | Submit the Operational Framework and Requirements document to the IESG for publication as Informational. |
| 24 months | Submit Agent Operational State and Lifecycle to the IESG for publication as Proposed Standard. |
| 30 months | Submit Agent Task Supervision and Intervention to the IESG for publication as Proposed Standard, and Operational Guidance as Informational. |

The working group will seek implementation and interoperability feedback throughout model development and will request rechartering before taking on work outside this scope.
