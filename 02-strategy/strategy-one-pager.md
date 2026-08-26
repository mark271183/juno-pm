# AI Strategy One-Pager - Juno Automated Prioritization

## 1. Problem & Workflow

The Problem: At RocketShip, roadmap prioritization is frequently influenced by the most vocal stakeholders rather than a consistent review of customer evidence. Priorities can shift from week to week, creating uncertainty across teams and reducing confidence in the roadmap.

Prevention: Juno is designed to prevent stakeholder-driven prioritization bias by ensuring backlog decisions are supported by verifiable evidence. A feature should not be promoted simply because it attracted attention in Slack or from a senior leader. Instead, Juno evaluates the strength and breadth of supporting signals before recommending a priority change.

## 2. Target Metrics

Cycle time : Reduce the average time spent on weekly prioritization reviews from approximately 120 minutes to 35 minutes, representing a reduction of more than 70%.

decision quality: Within the first month of rollout:

Fewer than 15% of prioritization decisions are revised within seven days.
At least 90% of roadmap items include two or more supporting evidence sources.
Product and leadership stakeholders report improved confidence in roadmap decisions through monthly feedback surveys.

## 3. Autonomy Level

Selected Approach: Copilot

Juno acts as a decision-support partner by generating:

A ranked backlog
Supporting rationale
Evidence references and citations
Potential trade-off considerations

The Product Manager remains accountable for reviewing recommendations and approving changes before publication.

Deliberately Excluded: Fully Autonomous Agent

Allowing Juno to independently reorder sprint priorities, alter release commitments, or publish roadmap updates introduces significant trust and governance risks. Product decisions require human judgment, particularly when balancing strategic objectives, customer impact, and delivery constraints.

## 4. Data & Model Approach

Selected Approach: RAG (Retrieval-Augmented Generation)

Juno is grounded in RocketShip's internal knowledge ecosystem, including:

Slack escalation channels
Customer support tickets
Product discovery interviews
Notion documentation
Jira backlog and delivery data

Every recommendation must reference traceable evidence so Product Managers can understand the reasoning behind a prioritization outcome.

Deliberately Avoided: Generic Foundation Model

Using a standalone large language model without retrieval introduces the risk of fabricated customer insights or unsupported recommendations. In prioritization workflows, a lack of evidence transparency would quickly undermine stakeholder confidence and limit adoption.

## 5. Risks & Mitigations

Risk

Historical data bias may cause Juno to place excessive weight on the most prominent signals from recent months. For example, enterprise escalations could dominate prioritization recommendations while emerging SMB pain points receive insufficient consideration.

Over time, this could result in a roadmap that reflects historical noise rather than future business value.

Mitigation

Introduce an evidence diversity check as part of the evaluation framework.

Recommendations are flagged for review when:

More than 60% of supporting evidence comes from a single source category.
Strategic customer segments are underrepresented.
Evidence recency exceeds a defined threshold.

A Product Manager reviews flagged outputs during the weekly prioritization cycle.

## 6. V1 Scope

In Scope
Prioritizing existing backlog items using evidence-driven scoring.
Identifying items with weak or missing supporting evidence.
Highlighting conflicts between customer signals and current Jira priorities.
Providing transparency into why recommendations were generated.
Out of Scope
Workforce planning, hiring, or resource allocation decisions.
Customer-facing explanations regarding roadmap prioritization decisions.
Automatic modification of sprint commitments or release dates.

These decisions remain fully owned by human Product Managers and leadership teams.
