# AI-Native User Flow · Juno
_Module 4. Generated using `M4 - AI User Flow Architect.html`. Paste into `04-ai-ux/user-flow.md`._

## Entry point

**Signal type:** New customer signal received

A new high-priority customer insight is added to Juno from one of its connected sources, such as a Zendesk P0/P1 ticket, a Salesforce closed-lost note, or a message posted in Slack `#voice-of-customer`.

### What they see instantly

A status banner appears:

> "Juno is analysing customer evidence..."

The Insights and Prioritisation panels become visible but partially dimmed, indicating that recommendations are being prepared.

A progress timeline appears so the Product Manager can see what Juno is doing rather than waiting on a blank screen.

---

## The flow

### 1. Retrieve supporting context

Juno performs a hybrid retrieval process across the approved knowledge base:

- RocketShip Strategy One-Pager

- Slack `#voice-of-customer`
  
- Zendesk P0/P1 tickets
  
- Salesforce closed-lost opportunity notes

Top-K retrieval target = 8 evidence segments.

### 2. Evaluate strategic alignment

Juno compares the new customer signal against:

- Strategic objectives

- Product priorities
  
- Existing customer themes
  
- Similar historical requests

The system identifies whether the issue supports an existing strategic pillar or represents a potentially emerging concern.

### 3. Generate priority recommendation

Juno combines:

- Strategic alignment

- Customer impact
  
- Frequency of occurrence
  
- Strength of supporting evidence
  
to generate a recommendation:

- P0

- P1
  
- P2
  
- P3
  
- Not Recommended

Every recommendation includes supporting citations.

### 4. Confidence assessment

Juno evaluates the quality and quantity of retrieved evidence.

- Confidence < 30 → Not Recommended

- Confidence 30-69 → Medium confidence recommendation
  
- Confidence ≥ 70 → Strong recommendation

Confidence is displayed to help the Product Manager understand how heavily to rely on the recommendation.

### 5. User-facing progress updates

Throughout processing, the Product Manager sees status messages such as:

> "Reviewing strategic priorities..."

> "Comparing customer evidence across sources..."

> "Assessing alignment and drafting recommendation..."

> "Generating prioritisation rationale..."

This provides transparency into how the recommendation was produced.

### 6. Decision paths

**Path A: Strategy available**

Juno generates a fully grounded recommendation with:

- Priority level

- Rationale
  
- Linked evidence citations
  
- Confidence score

**Path B: Strategy unavailable**

Juno enters **Evidence-Only Mode**.

Recommendations are labelled:

> "Low confidence - strategy source unavailable."

The Product Manager is prompted to load or update the Strategy One-Pager before using the recommendation for roadmap decisions.

---

## AI moments

**Placement:** Inline and Embedded

The centre Insights panel displays three AI-generated Insight Cards.

Each card includes:

- Priority badge (P0-P3 or Not Recommended)

- Customer evidence summary
  
- Supporting quote or ticket extract

- Confidence score

- Strategic alignment reference

- Source citations
  
The right-hand Prioritisation panel automatically drafts a recommendation summary using the retrieved evidence.

### Why this creates value

Juno is designed as an **Augmentation tool**, not an autonomous decision-maker.

Instead of spending time searching across Slack, Zendesk, Salesforce, and strategy documents, Product Managers receive an evidence-backed starting point that they can review, adjust, and approve.

The AI accelerates prioritisation while keeping accountability with the Product Manager.

---

## Fallbacks

### Kill switch

Every recommendation includes:

- Edit priority

- Edit rationale

- Reject recommendation

- Mark as Not Recommended

No recommendation updates the backlog without Product Manager approval.

### Training signal

Manual changes are logged as feedback.

Examples:

- Priority override
  
- Strategy alignment correction

- Evidence relevance correction

If multiple similar overrides occur, Juno flags the retrieval logic for review and highlights areas where recommendation quality may be degrading.

### Fail-safe

If no relevant strategic alignment or supporting evidence is found, Juno must not manufacture a recommendation.

Instead, the item is labelled:

> "Insufficient evidence available."

The card displays an amber warning and identifies which evidence sources were searched.

The Product Manager can:

- Add more context

- Upload additional evidence
  
- Proceed using human judgement

Juno never invents strategic alignment or customer evidence.

---

## Self-review

- [x] Trigger activates automatically when new customer evidence is received.

- [x] Progress updates provide visibility into AI processing and reduce perceived waiting time.

- [x] User experience aligns with the Augmentation value proposition defined in Module 2.

- [x] Every AI recommendation includes a manual override mechanism.

- [x] Fail-safe behaviour is clearly defined and prevents unsupported recommendations.

- [x] Hidden workflow aligns with Module 3 retrieval requirements, including Top-K retrieval, grounding rules, confidence scoring, and approved knowledge sources.
