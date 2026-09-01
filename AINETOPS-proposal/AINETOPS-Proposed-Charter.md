# AI-enabled Network Operations (AINETOPS) Working Group Charter

**Area:** Operations and Management  
**Mailing list:** ainetops@ietf.org  
**Mailing-list archive:** https://mailarchive.ietf.org/arch/browse/ainetops/

## Objective

AI-based systems are beginning to move beyond assisting network operators and are increasingly able to plan and execute operational tasks.

Existing IETF protocols provide access to network configuration and operational state, but they were not designed to manage the behavior of an autonomous agent carrying out a multi-step task. When agents, tools, controllers, and management systems from different vendors are involved, operators may not have a consistent way to determine what an agent is allowed to do, follow the actions it takes, intervene when something goes wrong, or relate the resulting network changes back to the original objective.

The AINETOPS Working Group will address the operational challenges created when AI-based agents participate directly in network operations. Its focus is the boundary between these agents and the existing network-management environment, not the internal design of the AI system.

## Scope

AINETOPS will provide a forum for operators, implementers, and protocol experts to share deployment experience and develop operational guidance for the use of AI-based agents in production networks.

The work includes:

- Describing the operational roles and responsibilities of network-management agents, supervising systems, tools, controllers, and human operators.
- Maintaining the objective, scope, constraints, and task context of an operation as it passes between agents, tools, and existing management systems.
- Observing and attributing the actions taken by an agent and the resulting changes to the network.
- Allowing an operator or policy system to approve, restrict, suspend, redirect, or terminate an agent task.
- Providing the operational state and lifecycle information needed to admit, monitor, suspend, update, or retire an agent.
- Developing guidance for least privilege, human oversight, failure containment, recovery, auditability, and incremental deployment.
- Identifying gaps in existing IETF management protocols and data models and referring protocol-specific work to the responsible working groups.

AINETOPS will reuse existing IETF protocols, security mechanisms, management models, and trace-context mechanisms wherever possible.

## Out of Scope

AINETOPS will not:

- Standardize AI or machine-learning algorithms, models, training methods, prompts, or reasoning techniques.
- Define a general-purpose AI-agent architecture or agent-to-agent protocol.
- Define general agent discovery, identity, authentication, authorization, or credential mechanisms.
- Standardize MCP, A2A, or another external agent framework.
- Redefine network, service, topology, telemetry, anomaly, incident, or configuration models owned by other working groups.
- Develop AI benchmarking methodologies.
- Authorize agents to bypass existing security, policy, or change-management controls.

New protocols or substantial extensions to protocols owned by another working group are outside the initial scope. Requirements for such work will be coordinated with and dispatched to the responsible group.

## Key Deliverables

The initial work of AINETOPS will be:

### 1. AINETOPS Operational Framework

An Informational document defining the operational problem, terminology, roles, boundaries, and the relationship between AI-based agents and existing network-management systems.

### 2. Operational Practices for Network-Management Agents

A Best Current Practice document covering admission, operational state, least privilege, task supervision, observability, intervention, failure containment, recovery, auditability, human oversight, and retirement.

### 3. Requirements and Gap Analysis

An Informational document identifying requirements placed on existing IETF management protocols and data models when they are used by AI-based agents. Protocol or data-model extensions will be developed in the responsible working groups unless AINETOPS is rechartered.

## Relationships with Other Working Groups

AINETOPS will coordinate with:

- **NMOP** on operator requirements, operational models, experiments, and network-management integration.
- **OPSAWG** on operational guidance and work spanning multiple OPS-area technologies.
- **NETMOD and NETCONF** on YANG models and existing management protocols.
- **BMWG** on benchmarking work.
- **Security and agent-related groups** working on identity, authorization, delegation, discovery, and agent-to-agent communication.
- **NMRG and other IRTF groups** on research questions concerning AI-native architectures, semantic models, ontologies, and inference.

The chairs will coordinate with the responsible working groups when work identifies a requirement for a protocol or data-model extension. Work that fits an existing working group will be sent there rather than adopted by AINETOPS.
