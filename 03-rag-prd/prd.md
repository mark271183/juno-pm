# AI PRD · Juno
2
 
3
> **Module 3 · RAG / AI PRD**
4
> This Product Requirements Document defines Juno's core product and retrieval requirements. It was developed using the **M3 · AI PRD Builder**, with the retrieval approach informed by the **M3 · RAG Architecture Decider**.
5
 
6
## Problem & User
7
 
8
### Problem
9
 
10
Roadmap prioritisation at RocketShip is often influenced by the most vocal stakeholder or the most recent escalation rather than a balanced assessment of customer needs, product strategy, and supporting evidence.
11
 
12
Product Managers currently review information across Slack, Jira, customer support tickets, interview notes, and Notion pages before making prioritisation decisions. This process is manual, fragmented, and can take approximately two hours each week.
13
 
14
As a result:
15
 
16
- Priorities can change frequently without clear supporting evidence.
17
- Product Managers spend significant time locating and comparing customer signals.
18
- Stakeholders cannot always see why one backlog item was prioritised over another.
19
- Important but less visible customer needs may be overlooked.
20
- Confidence in roadmap decisions can decline when priorities are reversed.
21
 
22
### Primary User
23
 
24
The primary user is a **Product Manager at RocketShip** responsible for reviewing and prioritising an existing product backlog.
25
 
26
The Product Manager needs a faster and more consistent way to:
27
 
28
- Consolidate evidence from multiple internal sources.
29
- Compare the strength of evidence across backlog items.
30
- Identify items with weak or missing evidence.
31
- Explain prioritisation decisions to stakeholders.
32
- Retain final accountability for approving the ranked backlog.
33
 
34
---
35
 
36
## Solution Overview
37
 
38
Juno is an AI-powered prioritisation copilot that reviews RocketShip's existing backlog and recommends a ranked list of items based on retrieved internal evidence.
39
 
40
For each backlog item, Juno:
41
 
42
1. Retrieves relevant evidence from approved internal sources.
43
2. Groups evidence by source type and customer signal.
44
3. Produces a recommended priority and written rationale.
45
4. Provides citations linking the recommendation to its supporting sources.
46
5. Identifies conflicting, weak, outdated, or unbalanced evidence.
47
6. Presents the recommendation to the Product Manager for review.
48
 
49
Juno does not automatically update sprint priorities, release dates, or published roadmaps. The Product Manager must review and approve all recommendations before any changes are made.
50
 
51
The intended outcome is to reduce the weekly prioritisation process from approximately **120 minutes to 35 minutes**, while improving the traceability and consistency of roadmap decisions.
52
 
53
---
54
 
55
## Retrieval Requirements (RAG)
56
 
57
### Sources
58
 
59
Juno retrieves information from RocketShip's approved internal product and customer evidence sources:
60
 
61
- Slack escalation channels
62
- Customer support tickets
63
- Customer interview and discovery notes
64
- Notion product documentation
65
- Jira backlog items and delivery data
66
 
67
Each retrieved item must include:
68
 
69
- A unique source identifier
70
- Source type
71
- Title or short description
72
- Creation or last-updated date
73
- Author or system of origin, where available
74
- A link to the original source
75
- The relevant supporting extract
76
 
77
Juno must only retrieve information that the signed-in Product Manager is authorised to access.
78
 
79
### Chunking and Indexing
80
 
81
Content will be chunked by its natural business structure rather than divided into fixed-length sections wherever possible.
82
 
83
Examples include:
84
 
85
- One Slack message or connected discussion thread
86
- One customer support ticket
87
- One interview question and response section
88
- One Notion page section
89
- One Jira issue, including its description and relevant comments
90
 
91
Each chunk will be indexed with metadata including:
92
 
93
- Source type
94
- Source ID
95
- Product area
96
- Backlog item or feature reference
97
- Customer segment, where available
98
- Date created or updated
99
- Content owner
100
- Access permissions
101
 
102
This approach preserves the context of each customer or stakeholder signal while allowing Juno to retrieve evidence relevant to a specific backlog item.
103
 
104
### Grounding Rule
105
 
106
Juno must not recommend a backlog priority without supporting evidence from the approved corpus.
107
 
108
Every recommended priority must:
109
 
110
- Include at least two cited sources.
111
- Include citations from more than one source type where relevant evidence is available.
112
- Clearly distinguish retrieved facts from AI-generated interpretation.
113
- Provide links back to the original sources.
114
- State when there is insufficient evidence to make a reliable recommendation.
115
 
116
If the minimum evidence threshold is not met, Juno must label the backlog item as **Insufficient evidence** rather than generating an unsupported rationale.
117
 
118
### Freshness
119
 
120
Juno should prioritise the most recent and relevant evidence while retaining older material where it provides important historical context.
121
 
122
The following freshness rules apply:
123
 
124
- The index must refresh at least once every 24 hours.
125
- Newly created or updated Jira items and escalation records should be available by the next scheduled refresh.
126
- Evidence older than 90 days must display its age in the recommendation.
127
- Juno must identify when a recommendation relies mainly on older evidence.
128
- The Product Manager must be able to view the retrieval date for each cited source.
129
 
130
Freshness does not automatically determine importance. Older evidence may still be relevant when it represents an unresolved or recurring customer problem.
131
 
132
### Evidence Balance
133
 
134
Juno must assess whether a recommendation is overly dependent on one evidence category.
135
 
136
A recommendation must be flagged for Product Manager review when:
137
 
138
- More than 60% of its cited evidence comes from a single source type.
139
- Evidence represents only one customer segment where multiple segments are relevant.
140
- Recent escalations conflict with established product strategy or existing Jira priorities.
141
- Supporting sources contain materially different views of the customer problem.
142
 
143
The flag must explain why the evidence may be unbalanced or conflicting. Juno must not resolve the conflict without human review.
144
 
145
---
146
 
147
## Requirements
148
 
149
| # | Requirement | Priority | Acceptance Criteria |
150
|---|---|---|---|
151
| 1 | Juno must retrieve evidence relevant to each selected backlog item from approved internal sources. | Must | For each backlog item, Juno returns relevant evidence with a source ID, source type, date, extract, and link to the original record. |
152
| 2 | Juno must produce a recommended ranking for the existing backlog. | Must | The output presents selected backlog items in priority order and provides a written rationale for each recommendation. |
153
| 3 | Every recommended priority must be supported by citations. | Must | At least 90% of prioritised items include two or more valid citations. Selecting a citation opens or identifies the original source. |
154
| 4 | Juno must not generate an unsupported prioritisation recommendation. | Must | When fewer than two relevant sources are retrieved, Juno labels the item as **Insufficient evidence** and does not present the recommendation as evidence-backed. |
155
| 5 | The Product Manager must approve recommendations before they are published or applied. | Must | Juno provides review, approve, reject, and edit options. No backlog or roadmap changes occur without an explicit approval action. |
156
| 6 | Juno must identify backlog items with weak or missing supporting evidence. | Must | Items that do not meet the evidence threshold are clearly flagged and grouped for further discovery or validation. |
157
| 7 | Juno must highlight conflicts between retrieved evidence and current Jira priorities. | Must | When customer evidence indicates a materially different priority from the current Jira ranking, Juno displays both positions and cites the relevant sources. |
158
| 8 | Juno must flag recommendations that rely too heavily on one source category. | Should | Recommendations are flagged when more than 60% of cited evidence comes from a single source type. |
159
| 9 | Juno should explain the main factors that influenced each recommendation. | Should | Each recommendation includes a concise explanation of the strongest supporting signals, evidence limitations, and relevant trade-offs. |
160
| 10 | Juno should display the age and source type of cited evidence. | Should | Each citation displays its source category and creation or last-updated date. Evidence older than 90 days is clearly identified. |
161
| 11 | Juno must respect existing access permissions. | Must | Users cannot retrieve or view content that they are not authorised to access in the source system. |
162
| 12 | Juno should allow the Product Manager to provide feedback on a recommendation. | Should | The Product Manager can approve, reject, or edit a recommendation and optionally record a reason for the decision. |
163
| 13 | Juno should record an audit trail of prioritisation decisions. | Should | The system records the proposed ranking, cited evidence, Product Manager decision, decision date, and any recorded rationale. |
164
| 14 | Juno should reduce the effort required for weekly prioritisation. | Should | During the initial launch period, the average weekly prioritisation review can be completed in 35 minutes or less. |
165
| 15 | Juno should provide a clear fallback when retrieval is unavailable. | Should | If a source cannot be searched or the index is unavailable, Juno identifies the affected source and avoids presenting incomplete results as comprehensive. |
166
 
167
---
168
 
169
## Success Measures
170
 
171
Juno's initial success will be measured during the first 30 days after launch.
172
 
173
- Reduce the average weekly prioritisation review from 120 minutes to 35 minutes or less.
174
- Ensure at least 90% of prioritised backlog items contain two or more cited sources.
175
- Keep the rate of prioritisation decisions reversed within seven days below 15%.
176
- Track how frequently Product Managers approve, edit, or reject Juno's recommendations.
177
- Monitor the number of recommendations flagged for insufficient, outdated, conflicting, or unbalanced evidence.
178
 
179
These measures will assess both workflow efficiency and the quality of Juno's evidence-backed recommendations.
180
 
181
---
182
 
183
## Out of Scope
184
 
185
The first version of Juno will not:
186
 
187
1. Make hiring, headcount, or workforce allocation decisions.
188
2. Automatically reorder sprint priorities or change active sprint commitments.
189
3. Change release dates without Product Manager approval.
190
4. Publish roadmap changes directly to stakeholders or customers.
191
5. Generate customer-facing explanations for why a feature was deprioritised.
192
6. Create new product strategy or company objectives.
193
7. Replace Product Manager judgment or accountability.
194
8. Retrieve information from unapproved external websites or public data sources.
195
9. Train a new foundation model using RocketShip's internal content.
196
10. Evaluate individual employee performance or attribute roadmap outcomes to specific employees.
197
 
198
These activities remain the responsibility of the Product Manager and relevant RocketShip leadership teams.
