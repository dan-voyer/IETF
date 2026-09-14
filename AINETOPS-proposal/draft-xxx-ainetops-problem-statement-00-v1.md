---
title: The problem statement of AI Native Network Operations
abbrev: AINETOps Problem Statement
docname: draft-XXX-ainetops-problem-statement-00
obsoletes:
updates:
date:
category: std
submissionType: IETF

ipr: trust200902
area: ops
workgroup: ainetops
keyword: Internet-Draft

author:
 -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 
 -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 
 -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 
  -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 
 -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 
 -
  ins: 
  name: 
  organization: 
  email: 
  city: 
  country: 


normative:
  RFC7011:
  RFC5424:
  RFC5277:


informative:
  I-D.zhao-nmop-network-management-agent:
 
...

--- abstract
The introduction of AI agents into network operations is fundamentally reshaping the operation and maintenance (O&M) paradigm, 
shifting from human-led, passive network management toward intent-driven, self-planning, and intelligent reasoning.  While this
shift promises significant gains in efficiency and autonomy, it introduces a set of problems that are not yet covered by the 
existing IETF network management framework.

This document identifies and summarizes the deployment and operation problems that arise when AI native network operations 
(AINETOps) are introduced into operator networks. It systematically enumerates the standardization gaps across Network 
Management Agent (NMA) lifecycle management, the Human-Agent Interface (HAI), the agent-to-agent task and evidence models, and 
task risk classification.  It does not propose solutions; its purpose is to provide a problem inventory that can anchor future 
IETF work on solutions and deployment best practices.

--- middle

# Introduction {#sec-intro}
Artificial intelligence (AI) and in particular the "agent" is being introduced into the operation and maintenance of operator 
networks. This document uses the term AI native network operations (AINETOps) to describe the resulting paradigm: a mode of 
network O&M in which AI agents are participants in the operations loop, acting on operator intent rather than merely assisting
human operators.

AI agents offer the potential to transform O&M from "human-led, OSS/NMS-passive" management to "intent-driven, self-planning, 
predictable, and intelligently reasoning" operations. Workflows move from "static scripts" to "self-planning", and security
moves from "account/person-based" to "task, operation, and authorization-based"control. Operators realize large-scale 
deployments of such agents in live networks.

However, as agentic AI systems are increasingly introduced into ISP network management systems to execute end-to-end O&M 
operations, traditional network management platforms are proving insufficient for the full operational lifecycle, e.g.,

• Unable to manage a rapidly growing fleet of heterogeneous Agents from multiple vendors, with divergent versions and 
capabilities. There lacks mechanisms for state monitoring, discovery and coordination across massive Agents.

• Network operators traditionally focus on whether system functions are operational. They now need to assess whether Agent 
reasoning and actions are correct, secure, and fit for purpose. Agent autonomous decision-making introduces non-deterministic
behaviors; it is challenging to quickly troubleshoot root causes spanning Agent, foundation model, tooling and data layers.

• Current interfaces are built for deterministic API invocation, not dynamic semantic collaboration between Agents. There are no
standardized mechanisms for Agent discovery, capability description, task decomposition, context propagation, result return, and
exception handling across multi-vendor implementations.

• Multi-vendor Agents cannot reliably interpret shared business intent, which creates ambiguity when executing cross-domain O&M 
workflows.

• Business workflows have evolved from static predefined procedures to dynamically adaptive execution. There is a gap in 
enforcing guardrails to ensure Agent autonomous decisions stay within operational and business boundaries.

• Human oversight becomes harder for multi-Agent chained tasks. Context is often lost after a task passes through multiple 
Agents and workflow stages, making it difficult for operators to retrieve complete information for auditing and validation.

As there is no common way to manage the agent itself, to let a human safely interact with it, or  to let multiple agents from
different vendors collaborate on a single end-to-end task. Existing interfaces (CLI, Web GUI, Syslog, IPFIX, NETCONF 
notifications) provide raw channels but not agent-specific semantics. This document therefore enumerates a set of deployment 
and operation problems that require further IETF work.  

## Requirements Language

{::boilerplate bcp14-tagged}

## Definition and Terminology

• AI：Artificial intelligence

• AINETOps:  AI Native Network Operations， the O&M paradigm in which AI agents are first-class participants in the operations
loop.

• NMA (Network Management Agent):  An agent that performs network management operations such as fault diagnosis, root-cause 
analysis, configuration, or optimization.  See [I-D.zhao-nmop-network-management-agent].

• HAI (Human-Agent Interface):  The interface through which an operations (O&M) person interacts with an NMA, including 
instruction, approval, handoff, and emergency control.

• A2A (Agent-to-Agent):  The interface between two NMAs.

• A2C (Agent-to-Controller):  The interface between an NMA and a network controller or NMS.

• A2N (Agent-to-Network):  The interface between an NMA and network devices.

• A2U (Agent-to-User/Human):  The interface between an NMA and a human operator (closely related to HAI).

• LLM：Large Language Model

• MCP：Model Context Protocol

• NMS：Network Management System

• OSS：Operations Support System


# Problem Statement {#sec-ps}

This section enumerates the deployment and operation problems identified by the AINETOps.   The problems are organized along 
the natural lifecycle of an agent in production: how it is "managed", how it is "observed", how it "evolves", how a "human" 
interacts with it, and how "agents interact with each other" to complete a task.

## NMA Lifecycle Management

A Network Management Agent is a long-lived production component.  Like any production software, it has a lifecycle: it is 
admitted into production, it runs under monitoring, it is changed and rolled back, and it eventually exits production.  
A unified operational lifecycle can be described as:

Production Admission -> Runtime Monitoring -> Change / Rollback -> Production Exit

Based on the whole lifecycle of a NMA, it may introduces operational problems for network management Agents running in live production environments, e.g.,

• Inconsistent Onboarding Standards and Admission Criteria

When a network operations agent is introduced into the production environment, there is no unified standard for defining, 
describing, and validating its capabilities. Different agent vendors and development teams use heterogeneous schemas to 
express what an agent can do — supported network domains, permissible action scopes, underlying model types, tool dependencies,
and operational constraints — making it impossible for NMS platforms to perform automated capability matching or policy-driven 
admission decisions. Furthermore, identity attestation, capability verification, and onboarding workflow approval lack 
standardized mechanisms: operators cannot reliably answer "who is this agent?", "what exactly can it do?", and "under what
conditions is it permitted to operate?" before granting production access.

• Fragmented Runtime State Visibility and Non-Reusable Execution Records

Once an agent enters active operation, the data that characterize its runtime state, such as health status, key performance
indicators, task progress, resource consumption, and error conditions, are exposed through vendor-specific formats with no
common schema. Operators cannot aggregate state information across agents from different sources into a unified monitoring view.
Execution records including task inputs, reasoning traces, action logs, and outcomes, are similarly non-standardized and lack
structural semantics that would enable cross-agent search, replay, audit, or reuse. When an anomaly occurs, the absence of 
uniform anomaly detection thresholds and alerting mechanisms delays operator awareness, extending mean-time-to-detect and
increasing blast radius.

• Unregulated Change Management and Inadequate Impact Assessment

Agents evolve continuously as models are updated, tools are added or removed, prompts are refined, and configuration parameters
are adjusted. However, there is no standardized mechanism for versioning these artifacts, describing the semantic differences
between versions, or assessing the potential impact of a change before it is deployed to production. Pre-deployment validation
against sandbox/digital twin environments is inconsistent across platforms; some agents support simulation-based verification 
while others do not, and even when simulation is available, the fidelity of simulated network environments varies widely. 
Consequently, changes are frequently pushed into production without sufficient safety validation or impact analysis, introducing
uncontrolled risk.

• Incomplete Decommissioning Procedures and Residual Trust Surfaces

When an agent is retired from the production environment, the decommissioning process is often ad hoc and incomplete. 
Credentials, API tokens, role bindings, and policy grants associated with the agent may not be systematically revoked, leaving
residual trust surfaces that can be exploited after the agent's intended operational lifetime. Interface bindings, cached data,
and derived artifacts (e.g., learned policies, accumulated telemetry baselines) are not consistently cleaned up according to 
defined retention or purging standards. Moreover, the decommissioning process itself lacks mandatory audit logging, meaning that
there is no tamper-evident record of what was revoked, when, and by whom — undermining both security posturing and regulatory
compliance.

### Agent Observability

Observability has two distinct dimensions for an agent:

• End-to-end task perspective: It needs a cross-component view of a single task as it traverses multiple agents and tools.

• Agent perspective: the health and performance of an individual agent — connection status, model/agent/tool call logging, 
rate-limit statistics, token consumption, and API rate limits.

Base on these two perspective, it may introduces operational problems as below: 

• Lack of End-to-End Task Perspective Observability

In multi-agent collaborative scenarios, a single operational task may span multiple agents, tools and backend systems. 
Without a cross-component, end-to-end task observability view, operators cannot pinpoint which entity — Agent, Tool, or other 
supporting systems — contributes to latency, errors or task failures. Task chains across distributed agents and tools turn 
into opaque black boxes. This makes root-cause investigation extremely challenging when service anomalies emerge.

• Lack of Agent Perspective Observability

Individual agent runtime state remains invisible to operation teams. Operators lack direct visibility into agent connection
status, model/agent/tool invocation logs, token consumption, rate limiting statistics and risk profiles. Without dedicated 
agent observability metrics, it is hard to assess individual agent health, execution performance and runtime risks. This 
hinders real-time detection of agent-side anomalies.

• Fragmented Telemetry Across Agent Pipelines 

Current monitoring systems collect metrics in silos. Telemetry data such as agent call counts, task success rate, task 
execution latency and abnormal task events are not correlated across the whole task pipeline. Fragmented telemetry fails 
to reconstruct the full lifecycle of cross-agent task execution. Operators cannot establish a complete trace linking task 
requests, agent delegations, tool invocations and final outcomes, which undermines auditability and incident post-mortem.


### Agent Evaluation and Evolution

As agentic AI systems for network O&M are continuously evaluated and evolved for carrier production deployment, there is a 
lack of standardized mechanisms for dynamic Agent capability assessment and standardized interfaces between Agents and 
simulation systems. This makes it difficult to sustain objective judgement on Agent operational competence and risk 
status, e.g.,

• Absence of Standardized Dynamic Evaluation for Agent Capabilities

The operational capability and risk posture of a network operations agent are not static — they evolve as underlying models are
updated, tool integrations change, prompts are refined, and operational context shifts. However, there is currently no 
standardized framework for continuously evaluating agent behavior in production or near-production environments. Evaluation 
data produced by different agents, platforms, and vendors use heterogeneous schemas with inconsistent semantics: metrics that
share the same name (e.g., "success rate," "latency," "safety score") may be computed using different definitions, over 
different time windows, against different baselines, rendering cross-agent and cross-platform comparison meaningless.

Furthermore, safety and stability evaluations lack consistent evidentiary foundations. Different platforms record different
subsets of safety-relevant events — policy violations, rollback triggers, human intervention requests, anomalous output 
detections, using incompatible formats and granularity levels. Consequently, determining whether a given agent is "stable" or
"safe" enough for production deployment becomes a matter of platform-specific interpretation rather than objective, reproducible
judgment. Operators cannot form a credible production-readiness assessment that transcends any single vendor's evaluation 
methodology.

• Non-Standardized Interfaces Between Agents and Simulation/Sandbox Environments

Pre-deployment validation of agent behavior increasingly relies on simulation or sandbox environments that emulate network 
topology, device state, traffic patterns, and failure scenarios. However, the interfaces through which agents interact with 
these environments — and through which environments report results back to evaluation systems — are entirely ad hoc. 
Different simulation platforms return execution results, network state transitions, performance indicators, alerts, anomalies,
and business impact assessments using divergent field names, semantic definitions, data granularities, and serialization 
formats. An evaluation system that needs to consume results from multiple simulation platforms must implement per-platform 
parsing and semantic translation logic, and even then, identical numerical outcomes may carry different meanings depending on
which platform produced them.

This heterogeneity has two further consequences. First, test results are difficult to reproduce: if scenario inputs, 
simulation parameters, and result outputs are all defined by each platform independently, then an evaluation obtained from 
simulation system A cannot be independently verified on simulation system B under equivalent conditions. Second, cross-platform
evaluation trust is fundamentally undermined — operators cannot determine whether divergent evaluations reflect genuine 
behavioral differences between agents or merely artifacts of incompatible simulation interfaces and reporting conventions.


## End-to-End Multi-Vendor Agent Execute O&M Operations 

In network operations workflows, multiple agents often sourced from different vendors, operating within different
administrative domains, and built on different model architectures, which must cooperate to decompose, delegate, execute, 
and verify complex operational tasks. This cooperation requires the continuous exchange of task objectives, operational 
context, constraints, diagnostic questions, supporting evidence, and risk assessments across agent boundaries. Currently, 
no standardized semantic models exist for any of these exchange artifacts, rendering end-to-end multi-agent collaboration 
fragile, non-reproducible, and auditably opaque. The Figure 1 shows the task delegation and evidence message flow between 
different agents. 

+---------------+  +---------------+  +---------------+         +---------------+
|  Fault        |  |  Domain       |  |  Controller   |         |  Other        |
|  Diagnosis    |  |  Agent        |  |  / Tool       |  ...... |  Agent        |
|  Agent        |  |               |  |               |         |               |
+-------+-------+  +-------+-------+  +-------+-------+         +-------+-------+
        |                  |                  |                         |
        |                  |                  |                         |
        | (1) Task (goal / context / constraint)                        |
        |=================>|                  |                         |
        |                  |                  |                         |
        | (2) Question & Evidence (phenomenon / analysis)               |
        |<=================|                  |                         |
        |                  |                  |                         |
        |                  | (3) Task (operation / verification)        |
        |                  |=================>|                         |
        |                  |                  |                         |
        |                  | (4) Result & Evidence                      |
        |                  | (execution result / verification           |
        |                  |<=================|                         |
        |                  |                  |                         |
        |                  |                  | (5) Ongoing             |
        |                  |                  |     Collaboration       |
        |                  |                  |=======================> |
        |                  |                  |                         |

         Figure 1: Task Delegation and Evidence Return Message Flow


### Human-Agent Interface (HAI)

The Human-Agent Interface is where an operations person instructs, approves, and critically intervenes in the actions of an
agent.  A representative scenario is the approval of a high-risk configuration change, in which the agent proposes remediation
options and the operator must decide among them.

•  Loss of Emergency Breakoff and Rollback Control

As autonomous agents execute operational tasks, they often proceed through multi-step remediation workflows without built-in 
phased confirmation gates. Once task execution has commenced, operational context may become stale or inaccessible. When 
operators detect risks and need to intervene, they lack immediate, reliable channels to issue emergency rollback or isolation
commands via the agent interaction surface. This creates safety hazards for high-risk network configuration changes, where 
timely human override is essential.

•  Insufficient Option Detail and Absence of Attached Evidence Chains 
When an agent presents remediation alternatives to operators, candidate options typically lack structured risk classification, 
quantified impact scope, and clear simulation prerequisites. Agent-delivered conclusions do not bundle supporting evidence 
including execution logs, performance metrics, time windows or network topology snapshots. Without a complete, verifiable
evidence trail attached to each proposed option, operators cannot make well-informed real-time judgments, nor readily support 
post-incident review and regulatory compliance.

•  Semantic and Format Limitations of Legacy Human-Network Interfaces

Traditional human-network interfaces such as CLI, web GUIs, traps, syslog and notifications support basic command delivery and
alerting, but are designed for human-to-device interaction rather than bidirectional human-agent dialogue. Existing standards
like [RFC5424] define event logging and notification formats, yet they do not specify structured semantics for agent to operator 
recommendation exchange. The absence of standardized message schemas for remediation options prevents consistent communication
of action labels, risk levels, impact scope, affected services, and pre-confirmation simulation requirements between operators 
and agents.


### Agent-Agent Interface 

When an upstream agent delegates a sub-task to a downstream agent, there is no common schema for expressing what the task is, 
what it must achieve, and under what constraints it must operate. Three specific problems compound this deficiency:

•  Task objective semantics are inconsistent: Different agents represent intent, target object, and expected outcome using 
heterogeneous natural-language templates, structured fields, or ad-hoc JSON schemas with no shared vocabulary. An "intent" 
expressed by one vendor's fault-diagnosis agent cannot be reliably parsed and acted upon by another vendor's domain-resolution 
agent without per-integration translation logic.

•  Task scope boundaries are not uniformly specified: The network scope (which devices, domains, or topology regions are in 
scope), impact scope (what services or customers may be affected), temporal validity window (when the task is valid for 
execution), and constraint conditions (rate limits, maintenance windows, coexistence rules) are either omitted entirely or 
encoded in vendor-specific formats that downstream agents cannot interpret programmatically.

•  Task state transitions are not interoperable: Task lifecycle states — pending, dispatched, in-progress, completed, failed, rolled back — along with structured error codes, partial result summaries, and causal failure explanations, lack a common 
representation. Consequently, when a task passes through a chain of three or more agents, each intermediary must implement 
custom state mapping, and the original task context is progressively lost or distorted.

### Human-Agent and Agent-Agent Interface

As agents collaborate, they continuously exchange observational data, diagnostic logs, performance indicators, command outputs, 
and analytical conclusions as evidence supporting their decisions. No standard model governs the structure, provenance, or 
quality of this evidence:

•  Evidence structure is fragmented: Observations, system logs, KPIs, CLI command outputs, and analytical conclusions are each 
serialized using different schemas, field naming conventions, and granularity levels across vendors and platforms. A piece of 
evidence produced by one agent cannot be consumed by another without format-specific parsing and semantic normalization.

•  Evidence provenance and quality are opaque: Critical metadata — the source agent or system that produced the evidence, the 
timestamp of collection, the confidence level or uncertainty bounds, the freshness relative to current network state, and the 
chain of derivations (raw data → processed metric → conclusion) — are either absent or inconsistently represented. Downstream 
agents receiving evidence cannot assess its reliability or decide whether it is sufficiently fresh and trustworthy to base 
further decisions upon.

•  Evidence-to-decision traceability is broken: There is no standardized mechanism to bind a piece of evidence to the task or 
question it addresses, to the analytical conclusion it supports, or to the subsequent action it justifies. When an operator or 
auditor attempts to reconstruct why a particular agent made a particular decision, the evidentiary trail is discontinuous across 
agent boundaries, making root-cause analysis, accountability attribution, and post-incident review fundamentally impaired.

### Agent-Controller  Interface (Wubo?)



### Task Risk Classification

Operational tasks in carrier networks carry inherently different risk profiles depending on the nature, scope, and potential 
blast radius of the actions involved. However, there is no standardized framework for classifying, communicating, and enforcing 
risk-appropriate controls across multi-agent collaboration chains:

•  Risk classification is not uniform: Different operators, vendors, and platforms use incompatible risk taxonomies. Some use 
numeric scales (e.g., R0–R5), others use categorical labels (low / medium / high / critical), and still others embed risk
implicitly in role-based access rules. There is no shared vocabulary enabling an upstream agent to communicate "this sub-task
carries risk level R4" such that all downstream agents and control-plane components interpret and enforce it consistently.

•  Permission and approval boundaries are misaligned. For a given risk level, the required human approvals, authorization scopes 
and executable action sets vary across platforms without a standard mapping. An operation classified as "high-risk" by one 
domain's policy engine may require four-eyes approval and sandbox pre-validation, while the same operation in another domain may
execute autonomously with no human gate. This inconsistency creates exploitable asymmetries where high-risk actions can be 
routed through lower-control domains to bypass intended safeguards.

•  Control requirements lack consistent enforcement semantics. Risk-mitigating controls — mandatory pre-execution verification, 
automatic rollback triggers, execution boundary confinement (e.g., read-only vs. write-enabled scope), and temporal constraints
are not expressed in a machine-interpretable form that travels with the task delegation. Consequently, even when an originating
agent specifies strict controls, those controls may be silently dropped or weakened as the task traverses intermediate agents, 
leaving the final executing agent unaware of the originally intended safety envelope.

# Gap Analysis and Requirements of AINETOps{#sec-ra}

## NMA Lifecycle Management

Two concrete gaps make the lifecycle unmanageable today:

• Fragmented state and configuration:  Across lifecycle stages, agent states and configurations are inconsistent. Information 
is difficult to reuse, weakening observability, auditability, and continuity.  There is no single, standardized capability 
metadata model for an NMA.

• No versioned evolution or retirement: Models, knowledge, and tools lack a unified versioning and validation process. 
Vendor-specific exit logic creates orphaned access and compliance risks: when an agent is retired, permissions 
and credentials may not be revoked consistently, leaving residual attack surface.

R-1: A unified lifecycle model for Network Management Agents may be defined — covering standard identities, capability 
metadata, and trust establishment, together with versioned change, rollback, and offboarding, so that multi-vendor NMAs can 
be governed consistently across production admission, runtime monitoring, change/rollback, and production exit. 

### Agent Observability

Existing IETF collection frameworks provide infrastructure but not agent-specific semantics.  IPFIX [RFC7011] and 
Syslog [RFC5424] give standardized flow and event collection, but lack agent-specific semantic models.  
NETCONF notifications [RFC5277] provide a subscription mechanism but do not cover agent internal state and model-inference 
metrics.

Without a cross-component, end-to-end task view, it is impossible to tell which part — agent, tool, or another system — is
responsible for latency or failure; task chains spanning multiple agents become opaque black boxes.  Without an 
agent-perspective view, individual agent health and performance remain invisible to operations personnel.

R-2: A unified observability schema and a set of agent telemetry and metric standards may be defined — covering connection 
status, model/agent/tool call logging, token consumption, and API rate limits. So that operations personnel gain end-to-end 
task observability across heterogeneous agents and tools.

### Agent Evaluation and Evolution

Two related gaps concern the "quality" of an agent over time:

•  Evaluation baseline: Network operation agents lack unified standards for capability definitions, test tasks, datasets, 
and evaluation metrics.
•  Evolution and regression: Agent evolution lacks a unified mechanism to compare a new version against a previous one and to
identify capability gains or regressions across operational tasks.

Without a unified evaluation baseline, it is difficult to determine whether an agent meets production requirements, and it is 
difficult to objectively compare the capability differences among different agents and versions.  The Benchmarking Methodology
Working Group (BMWG) is advancing agent benchmarking, but standards for evaluating intelligent agents are still lacking.

Without impact validation and regression mechanisms, unverified capability regressions may enter production, increasing 
operational risk.  The IETF has not yet initiated any work on NMA evolution.

R-3: How can a unified assessment method — defining what to evaluate, how to test, how to measure, and how to determine whether
an agent meets requirements — be established, together with agent evolution mechanisms that define triggering conditions, 
evolution scope, change mechanisms, and verification processes to ensure continuous capability improvement and operational 
reliability.

## End-to-End Multi-Vendor Agent Execute O&M Operations 

End-to-end multi-agent collaboration in network operations fails to interoperate not because of any lack of connectivity or 
transport, but because three shared semantic models are entirely absent at the standards level: there is no Task Model to 
unambiguously express task goals, scopes, and lifecycle states, so upstream intent degrades into vendor-specific representations
that downstream agents cannot reliably parse or align; there is no Evidence Model to normalize the structure, provenance, 
quality, and traceability of observations, logs, metrics, and analytical conclusions, so evidence cannot be trusted, compared,
or bound back to the tasks and decisions it supports; and there is no Task Risk Classification to define consistent risk levels, 
approval mappings, and enforceable control requirements, so safety envelopes vary across domains and can be silently weakened 
or bypassed as tasks traverse intermediate agents. Because these three gaps compound multiplicatively rather than 
independently—distorted task context cannot be corrected without trustworthy evidence, and erroneous decisions cannot be 
contained without enforceable risk controls—each additional hop across agents and administrative domains amplifies the inconsistency, ultimately rendering multi-agent collaboration incapable of being executed reliably, safely, or auditable end to end. 

### Human-Agent Interface (HAI)

Existing Human-Agent interfaces are insufficient for agent interaction:

•  Insufficient option detail and no evidence chain:  CLI, Web GUI, and Trap provide basic command and alert channels but lack 
structured semantics for agent interaction.  Each remediation option is presented with no structured risk classification, 
impact scope, or simulation requirement.  Agents deliver conclusions without showing the supporting data trail (logs, metrics, 
time windows, topology evidence).

•  Loss of emergency break-off / rollback control:  Syslog and notifications [RFC5424] provide standardized event logging but 
do not cover bidirectional human-agent dialogue.  Agents lack phased confirmation mechanisms after launching tasks; when an 
operator needs to intervene, context has already been lost.  Operators cannot rapidly issue emergency rollback or isolation
commands through an agent interaction.

R-4: How can a structured Human-Agent Interaction message format be defined — carrying, for each remediation option, an action 
label, a risk level, an impact scope, the affected services, and whether simulation is required, together with an evidence 
chain and auditability mechanism that attaches supporting evidence (logs, metrics, topology snapshots, time windows) to agent 
analysis, options, and operator decisions. 

### Task Model (Agent-Agent Interface)

To complete an end-to-end operation, a task must often be decomposed and delegated across multiple agents, controllers, and 
domain tools.  A unified "task model" is the schema that expresses such a task — its identity, intent, time window, scope, 
suggested operations, and status.

Across agents, controllers, and domain tools, the same operation task is often expressed differently in goals, scope, 
constraints, execution bounds, status, and outputs.  This makes consistent delivery, delegation, and task continuation
difficult.  TM Forum's A2A-T / Task-T work defines task description, interaction flow, and status management between agents, 
and its Task-T / Event-T / Negotiation-T work aligns with shared telecom semantics — but a standardized task-definition 
schema for network management agents within the IETF scope does not yet exist.

R-5: A standardized task-definition schema is required for Network Management Agents, expressing task identity, intent, time 
window, scope, constraints, execution bounds, status, and outputs, so that a task can be  consistently delivered, delegated, 
and continued across heterogeneous agents and domain tools.

### Evidence Model (Agent-Agent Interface)

Closely coupled to the task model is the “evidence model”: the structured representation of what an agent observed, did, and 
concluded, so that a downstream agent or a human can reason over and audit it.

Observations, commands, intermediate results, and verification data are reported in inconsistent formats and often lack shared 
provenance, confidence, and trace context.  This weakens cross-agent reasoning, auditability, and human handoff.  There is 
currently no common evidence package that captures provenance, confidence, trace context, and verification results.

R-6: How can a unified evidence model be defined，covering the evidence package, provenance, confidence, trace context, and 
verification results to support cross-agent reasoning and human review is a problem.

### Task Risk Classification

ISP network tasks carry very different levels of risk.  A read-only diagnostic is far less risky than a configuration change 
on a router. Yet there is no unified standard mapping risk levels to the permissions, approvals, execution scope, rollback, 
and verification requirements that should apply to each level.

Without a unified risk classification, the authorization and intervention semantics described above cannot be anchored: 
"task-based security" requires a shared notion of how risky a task is. Operators currently encode this knowledge implicitly 
in tooling and process, which does not scale to multi-vendor agents acting autonomously.

R-7: How can a unified task-risk classification be defined: for example, R0-R5 risk levels and common assessment rules for 
network operation tasks, together with the control requirements (permissions, approvals, execution scope, rollback, and 
verification) that apply to each risk level is a problem.



# IANA Considerations {#sec-iana}

This document has no IANA actions.

# Security Considerations {#sec-security}

This document is a problem statement and does not itself introduce new protocols or change the security properties of existing
systems. However, the deployment of AI agents in production networks raises security and trust considerations that motivate 
several of the problems described in draft: task-based authorization, emergency break-off and rollback control, and task risk 
classification.  In particular, the shift from account-based to task-based security, and the need for evidence chains and
auditability, are direct responses to the risk of an autonomous agent taking an unauthorized or unexpected action.

Any future solution documents developed from this work must analyze their own security considerations, including agent 
authentication and authorization, the integrity and confidentiality of the Human-Agent Interface and Agent-Agent interfaces, 
and the auditability of agent actions.  

# Acknowledgements
{:numbered="false"}

Much thanks for the valuable comments or feedback from XXX. 

--- back


