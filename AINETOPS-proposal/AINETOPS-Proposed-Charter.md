# AI-enabled Network Operations (AINETOPS) Working Group Charter

**Area:** Operations and Management  
**Mailing list:** ainetops@ietf.org  
**Mailing-list archive:** https://mailarchive.ietf.org/arch/browse/ainetops/

## Description of the Working Group

Operators are beginning to deploy autonomous and semi-autonomous network management agents (NMAs) from different vendors and across different network, technology, and administrative domains. Existing network-management protocols describe and control network resources, while generic agent mechanisms address functions such as identity, discovery, authorization, or agent-to-agent communication. Neither provides an interoperable operational contract by which an operator can manage NMAs themselves: describe their operational capabilities and dependencies; determine their version, health, and lifecycle state; bound and correlate a task across agents, gateways, and tools; or obtain evidence linking an operational objective to the resulting network actions. The absence of common semantics creates proprietary management silos and prevents consistent cross-vendor lifecycle management, intervention, and accountability.

The AINETOPS Working Group will define the minimum protocol-neutral semantics and IETF data models needed to operate NMAs as manageable entities in production networks. The work will use and extend existing IETF mechanisms where possible. It will not standardize AI algorithms, model internals, or a general-purpose agent architecture. The initial work focuses on externally observable and controllable behavior at the boundary between an NMA platform and network-operations systems.

For this charter, an NMA is an autonomous or semi-autonomous software component that interprets a network operational objective, selects or coordinates actions and tools, and participates in the configuration, assurance, optimization, or maintenance of networks implementing IETF protocols. This definition is behavioral and does not depend on a particular AI technique, model, framework, or product.

Current deployments expose four related interoperability gaps:

1. **NMA profile and capability ambiguity.** Operational capabilities, supported tools, dependencies, limitations, and versions are commonly described in proprietary schemas or natural language. An operator cannot reliably inventory, compare, admit, or select NMAs from different suppliers.

2. **Inconsistent lifecycle and health semantics.** Platforms use different representations for onboarding, validation, admission, active, degraded, suspended, revoked, and retired states. Health and dependency failures cannot be managed consistently across platforms.

3. **Loss of end-to-end task context.** A single operational task may traverse a supervisor, several NMAs, gateways, tools, controllers, and devices. Common identifiers and bounded context are missing, making it difficult to preserve the task objective, scope, constraints, parent-child relationships, and human decisions across those boundaries.

4. **Insufficient evidence and intervention points.** Operators need to connect an objective and policy decision to the actions attempted and their outcomes, including where a human or policy control approved, narrowed, suspended, redirected, or terminated a task. Proprietary evidence formats prevent end-to-end audit and cross-vendor troubleshooting.

These gaps affect architecture, operations, security, privacy, network management, scaling, and transition. The work must support large populations of NMAs and concurrent tasks without requiring disclosure of model internals or sensitive prompts and data. It must permit incremental deployment alongside existing management systems and vendor-specific implementations.

## Scope of Work

The Working Group will:

1. Establish precise terminology and role boundaries for NMAs, NMA platforms, gateways, tools, controllers, human operators, and managed network resources.

2. Define a common NMA operational profile and lifecycle model. The model will cover stable identity references, capability and dependency references, version information, administrative and operational state, health, admission and suspension state, and retirement or revocation.

3. Define a task-context and evidence model for correlating a network operational objective across multiple NMAs, gateways, tools, and management systems. The model will cover task and parent-task identifiers, objective and scope references, constraints, policy and human-intervention events, action and outcome references, timestamps, provenance, and integrity references. Existing correlation and trace-context mechanisms will be reused where suitable.

4. Document operational practices for deploying and managing NMAs safely, including admission, least privilege, validation before execution, failure containment, human oversight, rollback and recovery, change control, observability, audit retention, privacy, and retirement.

5. Validate the work against operator use cases and independent implementations. Standards-track work should identify at least two independent implementations or prototypes before being sent to the IESG, unless the responsible Area Director agrees that another form of implementation evidence is appropriate.

The Working Group may define YANG data models and mappings to existing IETF management and telemetry protocols. Any work that requires a new protocol or a material extension to a protocol owned by another working group requires coordination with that working group and the responsible Area Directors. Substantial expansion of the work requires rechartering.

## Deliverables

### 1. Operational Framework and BCP for Network Management Agents

An Informational or Best Current Practice document defining terminology, roles, deployment and failure models, operator requirements, architecture boundaries, security and privacy considerations, and recommended production practices. The document will be grounded in operational experience from multiple operators and implementations.

### 2. Network Management Agent Profile and Lifecycle Data Model

A Standards Track document defining a protocol-neutral information model and a YANG data model for NMA inventory, operational profile, capability and dependency references, versioning, administrative and operational state, health, admission, suspension, revocation, and retirement. It will define notifications and management actions only where they can be expressed through existing IETF management mechanisms.

### 3. Network Management Agent Task Context and Evidence Model

A Standards Track document defining common task correlation, bounded context, status, provenance, human and policy intervention events, and evidence references across NMAs, gateways, tools, controllers, and managed resources. It will specify mappings to existing IETF correlation, management, and telemetry mechanisms where appropriate, but will not define a general-purpose agent communication protocol.

## Out of Scope

The Working Group will not:

- Standardize AI or machine-learning algorithms, foundation models, training, prompts, reasoning methods, model selection, or evaluation of model intelligence.
- Define a general-purpose AI-agent architecture or agent-to-agent application protocol.
- Define generic agent discovery, naming, identity, authentication, authorization, credentialing, or workload-identity mechanisms. The Working Group will reuse and coordinate with the responsible IETF work.
- Standardize MCP, A2A, or another non-IETF framework. The Working Group may document requirements or mappings needed to use such frameworks in network operations without taking ownership of them.
- Redefine authoritative network, service, topology, telemetry, anomaly, incident, or configuration semantics owned by existing IETF working groups. NMA-facing representations must preserve traceability to their authoritative source models.
- Develop benchmarking methodologies. Such work will be coordinated with BMWG or another agreed venue.
- Standardize general ontologies, automated ontology construction, or AI inference theory. Research questions will be coordinated with the IRTF, including NMRG.
- Define the internals of a vendor's NMA platform, mandate a particular orchestration architecture, or require disclosure of proprietary model state.
- Define autonomous network policy or authorize an NMA to bypass existing security, change-management, or human-oversight controls.

## Coordination

The Working Group will coordinate closely with:

- **NMOP**, for operator requirements, experiments, network-management integration, and authoritative operational semantics.
- **OPSAWG**, for operational documents and cross-area work outside the focused AINETOPS deliverables.
- **NETMOD and NETCONF**, for YANG modeling and use of existing management protocols.
- **BMWG**, for NMA and AI-related benchmarking methodologies.
- Relevant IETF work on agent discovery, communication, workload identity, authentication, and authorization, so AINETOPS reuses rather than duplicates generic mechanisms.
- Related network-management-agent observability and intervention work, so task evidence, intervention, and lifecycle management have clear boundaries and compatible information models.
- **NMRG and other IRTF groups**, for research topics such as semantic reconciliation, ontologies, inference, and long-term architectures.
- Other standards-development organizations when external agent frameworks or management technologies are referenced.

The chairs will maintain a public dispatch and dependency table identifying related work, its venue, and its boundary with AINETOPS. Work that is better handled elsewhere will be sent to that venue rather than adopted by AINETOPS.

## Goals and Milestones

- **March 2027:** Adopt the Operational Framework and BCP for Network Management Agents document.
- **June 2027:** Adopt the Network Management Agent Profile and Lifecycle Data Model document.
- **September 2027:** Adopt the Network Management Agent Task Context and Evidence Model document.
- **December 2027:** Complete Working Group Last Call for the Operational Framework and BCP.
- **March 2028:** Submit the Operational Framework and BCP to the IESG.
- **June 2028:** Publish an implementation-status report and complete Working Group Last Call for the NMA Profile and Lifecycle Data Model.
- **September 2028:** Submit the NMA Profile and Lifecycle Data Model to the IESG.
- **December 2028:** Publish an implementation-status report and complete Working Group Last Call for the NMA Task Context and Evidence Model.
- **March 2029:** Submit the NMA Task Context and Evidence Model to the IESG and evaluate whether to close or recharter the Working Group.
