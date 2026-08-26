# AI PRD · Juno

> **Module 3 · RAG / AI PRD**
4
> This Product Requirements Document defines Juno's core product and retrieval requirements. It was developed using the **M3 · AI PRD Builder**, with the retrieval approach informed by the **M3 · RAG Architecture Decider**.

## Problem & User

### Problem

Roadmap prioritisation at RocketShip is often influenced by the most vocal stakeholder or the most recent escalation rather than a balanced assessment of customer needs, product strategy, and supporting evidence.

Product Managers currently review information across Slack, Jira, customer support tickets, interview notes, and Notion pages before making prioritisation decisions. This process is manual, fragmented, and can take approximately two hours each week.

As a result:

- Priorities can change frequently without clear supporting evidence.
- Product Managers spend significant time locating and comparing customer signals.

- Stakeholders cannot always see why one backlog item was prioritised over another.

- Important but less visible customer needs may be overlooked.

- Confidence in roadmap decisions can decline when priorities are reversed.

### Primary User

The primary user is a **Product Manager at RocketShip** responsible for reviewing and prioritising an existing product backlog.

The Product Manager needs a faster and more consistent way to:

- Consolidate evidence from multiple internal sources.
- Compare the strength of evidence across backlog items.
- Identify items with weak or missing evidence.
- Explain prioritisation decisions to stakeholders.

- Retain final accountability for approving the ranked backlog.

---
## Solution Overview

Juno is an AI-powered prioritisation copilot that reviews RocketShip's existing backlog and recommends a ranked list of items based on retrieved internal evidence.

For each backlog item, Juno:

1. Retrieves relevant evidence from approved internal sources.

2. Groups evidence by source type and customer signal.

3. Produces a recommended priority and written rationale.

4. Provides citations linking the recommendation to its supporting sources.

5. Identifies conflicting, weak, outdated, or unbalanced evidence.

6. Presents the recommendation to the Product Manager for review.

Juno does not automatically update sprint priorities, release dates, or published roadmaps. The Product Manager must review and approve all recommendations before any changes are made.

The intended outcome is to reduce the weekly prioritisation process from approximately **120 minutes to 35 minutes**, while improving the traceability and consistency of roadmap decisions.

---

## Retrieval Requirements (RAG)

### Sources

Juno retrieves information from RocketShip's approved internal product and customer evidence sources:

- Slack escalation channels
- Customer support tickets

- Customer interview and discovery notes

- Notion product documentation

- Jira backlog items and delivery data

Each retrieved item must include:

- A unique source identifier

- Source type
  
- Title or short description

- Creation or last-updated date

- Author or system of origin, where available

- A link to the original source

- The relevant supporting extract

Juno must only retrieve information that the signed-in Product Manager is authorised to access.

### Chunking and Indexing

Content will be chunked by its natural business structure rather than divided into fixed-length sections wherever possible.

Examples include:

- One Slack message or connected discussion thread

- One customer support ticket
  
- One interview question and response section
  
- One Notion page section
  
- One Jira issue, including its description and relevant comments
  
Each chunk will be indexed with metadata including:

- Source type
  
- Source ID

- Product area

- Backlog item or feature reference
  
- Customer segment, where available
  
- Date created or updated
  
- Content owner
  
- Access permissions
  
This approach preserves the context of each customer or stakeholder signal while allowing Juno to retrieve evidence relevant to a specific backlog item.
  
### Grounding Rule

Juno must not recommend a backlog priority without supporting evidence from the approved corpus.

Every recommended priority must:

- Include at least two cited sources.
  
- Include citations from more than one source type where relevant evidence is available.

- Clearly distinguish retrieved facts from AI-generated interpretation.
  
- Provide links back to the original sources.
  
- State when there is insufficient evidence to make a reliable recommendation.

If the minimum evidence threshold is not met, Juno must label the backlog item as **Insufficient evidence** rather than generating an unsupported rationale.

### Freshness

Juno should prioritise the most recent and relevant evidence while retaining older material where it provides important historical context.

The following freshness rules apply:

- The index must refresh at least once every 24 hours.

- Newly created or updated Jira items and escalation records should be available by the next scheduled refresh.
  
- Evidence older than 90 days must display its age in the recommendation.
  
- Juno must identify when a recommendation relies mainly on older evidence.
  
- The Product Manager must be able to view the retrieval date for each cited source.

Freshness does not automatically determine importance. Older evidence may still be relevant when it represents an unresolved or recurring customer problem.

### Evidence Balance

Juno must assess whether a recommendation is overly dependent on one evidence category.

A recommendation must be flagged for Product Manager review when:

- More than 60% of its cited evidence comes from a single source type.
  
- Evidence represents only one customer segment where multiple segments are relevant.

- Recent escalations conflict with established product strategy or existing Jira priorities.
  
- Supporting sources contain materially different views of the customer problem.

The flag must explain why the evidence may be unbalanced or conflicting. Juno must not resolve the conflict without human review.

---

## Requirements

| # | Requirement | Priority | Acceptance Criteria |

|---|---|---|---|

| 1 | Juno must retrieve evidence relevant to each selected backlog item from approved internal sources. | Must | For each backlog item, Juno returns relevant evidence with a source ID, source type, date, extract, and link to the original record. |

| 2 | Juno must produce a recommended ranking for the existing backlog. | Must | The output presents selected backlog items in priority order and provides a written rationale for each recommendation. |

| 3 | Every recommended priority must be supported by citations. | Must | At least 90% of prioritised items include two or more valid citations. Selecting a citation opens or identifies the original source. |

| 4 | Juno must not generate an unsupported prioritisation recommendation. | Must | When fewer than two relevant sources are retrieved, Juno labels the item as **Insufficient evidence** and does not present the recommendation as evidence-backed. |

| 5 | The Product Manager must approve recommendations before they are published or applied. | Must | Juno provides review, approve, reject, and edit options. No backlog or roadmap changes occur without an explicit approval action. |

| 6 | Juno must identify backlog items with weak or missing supporting evidence. | Must | Items that do not meet the evidence threshold are clearly flagged and grouped for further discovery or validation. |

| 7 | Juno must highlight conflicts between retrieved evidence and current Jira priorities. | Must | When customer evidence indicates a materially different priority from the current Jira ranking, Juno displays both positions and cites the relevant sources. |

| 8 | Juno must flag recommendations that rely too heavily on one source category. | Should | Recommendations are flagged when more than 60% of cited evidence comes from a single source type. |

| 9 | Juno should explain the main factors that influenced each recommendation. | Should | Each recommendation includes a concise explanation of the strongest supporting signals, evidence limitations, and relevant trade-offs. |

| 10 | Juno should display the age and source type of cited evidence. | Should | Each citation displays its source category and creation or last-updated date. Evidence older than 90 days is clearly identified. |

| 11 | Juno must respect existing access permissions. | Must | Users cannot retrieve or view content that they are not authorised to access in the source system. |

| 12 | Juno should allow the Product Manager to provide feedback on a recommendation. | Should | The Product Manager can approve, reject, or edit a recommendation and optionally record a reason for the decision. |

| 13 | Juno should record an audit trail of prioritisation decisions. | Should | The system records the proposed ranking, cited evidence, Product Manager decision, decision date, and any recorded rationale. |

| 14 | Juno should reduce the effort required for weekly prioritisation. | Should | During the initial launch period, the average weekly prioritisation review can be completed in 35 minutes or less. |

| 15 | Juno should provide a clear fallback when retrieval is unavailable. | Should | If a source cannot be searched or the index is unavailable, Juno identifies the affected source and avoids presenting incomplete results as comprehensive. |

---

## Success Measures

Juno's initial success will be measured during the first 30 days after launch.

- Reduce the average weekly prioritisation review from 120 minutes to 35 minutes or less.

- Ensure at least 90% of prioritised backlog items contain two or more cited sources.
  
- Keep the rate of prioritisation decisions reversed within seven days below 15%.
  
- Track how frequently Product Managers approve, edit, or reject Juno's recommendations.
  
- Monitor the number of recommendations flagged for insufficient, outdated, conflicting, or unbalanced evidence.

These measures will assess both workflow efficiency and the quality of Juno's evidence-backed recommendations.

---

## Out of Scope

The first version of Juno will not:

1. Make hiring, headcount, or workforce allocation decisions.
   
3. Automatically reorder sprint priorities or change active sprint commitments.
  
4. Change release dates without Product Manager approval.
  
5. Publish roadmap changes directly to stakeholders or customers.
  
6. Generate customer-facing explanations for why a feature was deprioritised.
   
7. Create new product strategy or company objectives.
   
8. Replace Product Manager judgment or accountability.
   
9. Retrieve information from unapproved external websites or public data sources.
   
10. Train a new foundation model using RocketShip's internal content.

11. Evaluate individual employee performance or attribute roadmap outcomes to specific employees.

These activities remain the responsibility of the Product Manager and relevant RocketShip leadership teams.
