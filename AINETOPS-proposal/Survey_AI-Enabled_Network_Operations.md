# Survey of Agentic Network-Management Experience and Needs

Prepared to inform the proposed AINETOPS BoF at IETF 127 | September 2026

## Purpose and instructions

This survey asks about practical experience with AI agents in network operations, the controls already available, and any problems integrating independently developed products. Responses will help assess whether additional standardization is needed for agent operational state and lifecycle, and for task supervision and intervention. Existing mechanisms may already meet your needs; that is equally valuable feedback. The survey does not presume support for a new working group or a particular technology such as YANG.

For this survey, a **network-management agent** is software that uses AI to plan or carry out operational tasks through tools, controllers, or network interfaces. A system that only provides recommendations should be identified as advisory. Please distinguish agents from conventional scripts and other AI/ML applications.

Answer for a deployment or operational domain you know directly. Distinguish production experience, pilot results, and expectations. Select one answer unless otherwise stated. For tables, select one column per row. Questions may be skipped if you cannot answer or prefer not to disclose the information.

Do not include customer data, credentials, sensitive incident details, or identifying free text. No name or contact details are requested in the questionnaire. Results are intended for aggregate reporting; any attributed case study requires separate consent. Before launch, the organizers must publish who can access responses, their retention period, and whether the collection platform records identifiers. Do not describe the collection as anonymous unless its configuration supports that claim.

The core survey contains 19 questions. Section E is optional background. Completion time will be estimated after a pilot of the survey.

## A. Respondent and deployment context

### A1. What perspective are you answering from?

- [ ] Network operator, including an ISP, mobile, enterprise, or cloud network operator
- [ ] Vendor or system integrator
- [ ] Open-source developer or maintainer
- [ ] Research or academic organization
- [ ] Other: __________
- [ ] Prefer not to say

### A2. What is your primary role?

- [ ] Network operations
- [ ] Network engineering or architecture
- [ ] Automation or management-platform development
- [ ] AI or data science
- [ ] Standards or strategy
- [ ] Other: __________
- [ ] Prefer not to say

### A3. Which domains does your response cover? Select all that apply.

- [ ] IP or transport backbone
- [ ] Mobile access or RAN
- [ ] Mobile core
- [ ] Fixed or broadband access
- [ ] Data center, cloud, or edge
- [ ] Enterprise network
- [ ] Other: __________
- [ ] Prefer not to say

### A4. What is the current deployment status of network-management agents in the domain you are describing?

- [ ] Production at scale
- [ ] Production with limited scope
- [ ] Pilot or laboratory trial only
- [ ] Planned or under evaluation; no deployed agent
- [ ] No deployment or current plan
- [ ] Don't know

**Routing:** If no agent is deployed, or you do not know, skip Section B and continue to C1. In Section C, report expected needs separately from observed problems and skip C4–C5, which concern deployed agents. Production and pilot respondents may answer all of Section C. Everyone may answer Section D.

## B. Current agent deployment

### B1. What is the deployment status of each capability in the domain you are describing?

If a capability is both deployed and planned for expansion, select its current deployment status.

| Capability | Production | Pilot only | Planned only | Not used or planned | Don't know |
| --- | --- | --- | --- | --- | --- |
| Fault detection, correlation, or root-cause analysis | ○ | ○ | ○ | ○ | ○ |
| Configuration validation or compliance checking | ○ | ○ | ○ | ○ | ○ |
| Planning operational tasks | ○ | ○ | ○ | ○ | ○ |
| Executing network changes | ○ | ○ | ○ | ○ | ○ |
| Optimization or preventive maintenance | ○ | ○ | ○ | ○ | ○ |
| Operator assistance or report generation | ○ | ○ | ○ | ○ | ○ |
| Coordinating tasks across agents or domains | ○ | ○ | ○ | ○ | ○ |

Other capability and status: __________

### B2. What authority do your deployed agents have? Select all that apply and indicate production or pilot for each selected answer.

- [ ] Provide advice only; people execute changes
- [ ] Execute read-only diagnostic operations
- [ ] Execute changes after approval of each action
- [ ] Execute a multi-step task after approval of its plan
- [ ] Execute changes within delegated limits without per-task approval
- [ ] Other: __________
- [ ] Don't know

### B3. Where do your deployed agents come from? Select all that apply.

- [ ] Developed in-house
- [ ] One commercial vendor
- [ ] Multiple commercial vendors
- [ ] Open-source projects
- [ ] Other: __________
- [ ] Don't know

### B4. Which interfaces do deployed agents use to invoke tools or network operations? Select all that apply.

These may occur at different points in the same path; for example, an agent may invoke a tool that calls a controller API.

- [ ] NETCONF or RESTCONF
- [ ] gNMI or gNOI
- [ ] CLI or scripts
- [ ] Controller or network-management system APIs
- [ ] MCP
- [ ] Other tool interfaces: __________
- [ ] Agents do not invoke tools or network operations
- [ ] Don't know

### B5. How are agents supervised today? Select all that apply.

- [ ] A common interface across independently developed agents
- [ ] Product-specific interfaces integrated through adapters
- [ ] Separate management interfaces for each product
- [ ] Manual procedures without a common supervisory interface
- [ ] Other: __________
- [ ] Don't know

## C. Operational problems and existing solutions

### C1. What is the status of each supervision need in your environment?

Report the current status. Choose “Met through existing mechanisms” when no custom supervision integration is needed, and “Met through custom integration” when adapters or workarounds adequately meet the need. Choose “Unresolved observed gap” when a need remains unmet in production or a pilot, including after a partial workaround. Choose “Expected need” only when you have no deployment evidence.

| Need | Met through existing mechanisms | Met through custom integration | Unresolved observed gap | Expected need, not tested | Not needed or applicable | Don't know |
| --- | --- | --- | --- | --- | --- | --- |
| Read agent capabilities and operational state consistently across products | ○ | ○ | ○ | ○ | ○ | ○ |
| Admit, suspend, update, and retire agents through consistent management interfaces | ○ | ○ | ○ | ○ | ○ | ○ |
| Track a task and associate it with affected resources and downstream operations | ○ | ○ | ○ | ○ | ○ | ○ |
| Approve, suspend, resume, or terminate a task with a clear acknowledgement and outcome | ○ | ○ | ○ | ○ | ○ | ○ |
| Determine which downstream operations completed, remain active, failed, or have unknown outcomes | ○ | ○ | ○ | ○ | ○ | ○ |
| Correlate actions and observed network changes with the original task | ○ | ○ | ○ | ○ | ○ | ○ |

### C2. Have differences between products' agent lifecycle or task-supervision interfaces required custom integration?

- [ ] Yes, in production
- [ ] Yes, in a pilot only
- [ ] Integration is planned but has not been attempted
- [ ] No; existing interfaces meet our needs
- [ ] No; we have not needed to integrate independent products
- [ ] Don't know

### C3. Describe one successful use of existing mechanisms or one observed gap. Optional; skip if you have no direct experience to report.

- Production or pilot: __________
- Operation you were attempting: __________
- Interface between components involved: __________
- Existing protocol, model, product feature, or framework used: __________
- What worked, or what was missing or interpreted differently: __________
- Any custom integration or workaround, its operational impact, and remaining limitations: __________

Please avoid sensitive incident details. For a gap, distinguish a missing product implementation from a missing specification, if known. Successful examples help identify mechanisms the work can reuse.

**Routing:** If no agent is deployed, or you do not know its deployment status, continue to Section D. C4–C5 concern production or pilot deployments.

### C4. After suspending or terminating a task, can your supervising system determine the state of downstream network operations?

- [ ] Yes, consistently across the products we use
- [ ] Yes, within individual products, but not consistently across them
- [ ] Partially; some outcomes require manual investigation
- [ ] No
- [ ] We have not tested this
- [ ] Not applicable; agents do not initiate network operations
- [ ] Don't know

Optional: Which outcomes cannot be determined, and how do you handle them? __________

### C5. Which controls are implemented today? Select all that apply; identify production or pilot where relevant.

- [ ] Identity and permission checks
- [ ] Authorization constrained by task, resources, actions, or time
- [ ] Human approval before changes
- [ ] Approval at intermediate task steps
- [ ] Simulation, sandbox, or canary validation
- [ ] Stop issuing new agent actions
- [ ] Cancel operations already accepted by downstream tools or controllers
- [ ] Compensate for or roll back completed changes where supported
- [ ] Record actions and correlate them with observed network outcomes
- [ ] None of these
- [ ] Don't know

Stopping an agent, cancelling a downstream operation, and reversing a completed change are separate capabilities. None implies the others.

## D. Standardization needs and participation

### D1. For each proposed work item, what is your assessment?

| Work item | Existing mechanisms suffice | Implementation or guidance improvements needed; no new specification identified | Additional interoperable specification needed | Not relevant to us | Insufficient information |
| --- | --- | --- | --- | --- | --- |
| Agent operational state and lifecycle management | ○ | ○ | ○ | ○ | ○ |
| Agent task supervision and intervention | ○ | ○ | ○ | ○ | ○ |

What evidence or existing mechanism supports your answer? __________

### D2. Which interfaces could your organization realistically implement or integrate for agent supervision? Select all that apply.

- [ ] YANG with NETCONF or RESTCONF
- [ ] HTTP/JSON API
- [ ] Protobuf/gRPC API
- [ ] A profile or extension of an existing task protocol; specify: __________
- [ ] Another interface: __________
- [ ] No preference; common behavior and interoperability are the priority
- [ ] No implementation planned
- [ ] Don't know

These approaches can overlap. Optional: distinguish what you already support from what you would need to add. __________

### D3. If additional standardization is justified, where should it be pursued?

- [ ] A dedicated AINETOPS working group
- [ ] Existing IETF working groups, coordinating where necessary
- [ ] An existing external specification or implementation community
- [ ] A combination; explain: __________
- [ ] No additional standardization is needed
- [ ] Insufficient information

Optional explanation: __________

### D4. What contributions could you or your organization make?

For each entry below, indicate **committed**, **interested but unconfirmed**, **none**, or **unknown**, and whether you are answering for yourself or your organization. Do not report an organizational commitment without authority to make it.

- Contribute an operational report: __________
- Help refine the survey questionnaire: __________

For the Standards Track work items:

| Work item | Supply cases or requirements | Write or review specifications | Implement | Join interoperability testing | Evaluate deployment |
| --- | --- | --- | --- | --- | --- |
| Agent operational state and lifecycle | | | | | |
| Agent task supervision and intervention | | | | | |

### D5. What should this effort address first, or avoid doing? Optional.

Response: __________

## E. Optional broader context

These questions provide background for related industry and IETF discussions. They do not imply that these topics belong in the proposed AINETOPS charter.

### E1. Where does your organization operate? Select all that apply.

- [ ] Europe
- [ ] North America
- [ ] Latin America and the Caribbean
- [ ] Asia-Pacific, excluding Greater China
- [ ] Greater China
- [ ] Middle East and Africa
- [ ] Prefer not to say

### E2. Approximately how many network elements are managed in the domain covered by your response?

- [ ] Fewer than 10,000
- [ ] 10,000–99,999
- [ ] 100,000–999,999
- [ ] 1 million or more
- [ ] Don't know or prefer not to say

### E3. Approximately how many agent instances operate concurrently in that domain?

Count running instances, rather than model types or cumulative task executions.

- [ ] None
- [ ] 1–9
- [ ] 10–99
- [ ] 100–999
- [ ] 1,000 or more
- [ ] Don't know

### E4. Which broader challenges matter most? Select up to three.

- [ ] Data quality or fragmentation
- [ ] Agent evaluation or benchmarking
- [ ] Simulation or digital-twin integration
- [ ] Agent-to-agent collaboration
- [ ] Security, privacy, or regulatory requirements
- [ ] Skills or organizational change
- [ ] Cost or return on investment
- [ ] Energy use
- [ ] Legacy-system integration
- [ ] Availability of tools or reference implementations
- [ ] Other: __________
- [ ] None of these
- [ ] Don't know

### E5. Which frameworks or implementation communities inform your work? Select all that apply.

- [ ] TM Forum
- [ ] ETSI or 3GPP
- [ ] IETF working groups or IRTF research groups
- [ ] OpenConfig
- [ ] OpenDaylight
- [ ] MCP
- [ ] A2A
- [ ] Other: __________
- [ ] None
- [ ] Don't know

## Follow-up and reporting

Thank you for contributing. If you would like to discuss a case study or participate further, contact the organizers separately through [the AINETOPS mailing list](mailto:ainetops@ietf.org). Mailing-list messages are public; do not send confidential responses there.

Organizers should report the sample size and recruitment method, distinguish operators, vendors, open-source developers, and researchers, and separate production evidence, pilot experience, and expectations. Report the number answering each question and retain “not applicable” and “don't know” responses. Avoid publishing small identifiable subgroups or identifiable free-text responses. Survey findings are input to the BoF discussion, not a determination of IETF consensus or proof that a new working group is required.
