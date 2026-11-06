# Stage 2: Call Quality Scorecard & CRM Taxonomy (Deliverable A)

**Evidence base:** the 6 transcripts, the demo evaluations, the policy file, and the payment data. The parent-psychology observations in section 1 come from these calls (a small sample), so treat them as hypotheses to confirm during rollout, not as market research.

---

## 1. What makes a great kids' EdTech sales call

Across the six calls, the strongest ones (801, 804, 805) share one pattern: **the rep proves they watched the demo, lets the parent describe the pain, then connects the course to that exact pain before price.** The weakest ones skip straight to price or pressure.

| Parent theme | India (801, 803, 805, 806) | GCC / USA (802, 804) |
|---|---|---|
| **Who decides** | Family decision. Husband handles payment (801); "mummy bol rahi hain exams ke baad dekhenge" (805). A rep must equip the *absent* decision-maker, not just the person on the call. | Usually the person on the call decides (804 bought within 2 hours). |
| **Main worry** | School performance and exams (805), stage fear (801), fear of being sold a fake promise (803: "that sounds like a fake sales promise"). | Fit with the local alternative and local curriculum (802: AED 350 tutor, British exams); schedule fit with extracurriculars (804: gymnastics). |
| **Price behaviour** | Cash-flow sensitive, wants installments (805). Accepts price when value is clear (801: "quite reasonable"). | Premium price must be justified by *method* (802). Price was not the blocker in 804. |
| **What closes** | A WhatsApp summary the other parent can read (801); installment plan (805); trust in the teacher (803). | A batch that fits the calendar (804); a clear answer to "how will this fix my child's specific problem" (802). |
| **Culture** | Hinglish is natural; WhatsApp is the default channel (805). | Heritage content must feel like character-building, not a lecture (804, and the policy bans religious-dogma framing). |

**Design implication:** the AI must read the *objection behind* the objection. "Price issue" in 802 was really "you haven't explained why you beat my local tutor."

---

## 2. Call Quality Scorecard (7 criteria, 100 points)

Each criterion is rated **1-5**. Score = sum of (weight x rating / 5).

| # | Criterion | Weight | Rating 1 | Rating 3 | Rating 5 |
|---|---|---|---|---|---|
| 1 | **Rapport & child-specific praise** | 10 | Generic ("all kids love it") or praise that contradicts the evaluation (806: "natural Grandmaster" vs engagement 2/5) | Uses the child's name and general positives | Cites a specific demo moment that matches `demo_magic_moment_for_parent` within the first 2 minutes (801: "asteroid", "Superhero Hook") |
| 2 | **Diagnosing the learning gap** | 20 | No discovery, or reads questions without reacting to answers (806) | Asks about goals but does not link the answer to the demo gap | Parent states the pain in their own words, and the rep reflects it back linked to `learning_gaps_observed` (805: mental translation, "umm") |
| 3 | **Curriculum pitch before price** | 15 | Price quoted before any method explanation (802 at 00:30) | Price after a generic pitch | Method tied to this child's gap, *then* price, with installments offered when cash flow is raised |
| 4 | **Objection handling** | 20 | Ignores, dismisses, or answers with a discount or pressure (802, 806) | Acknowledges but gives a generic answer | Names the objection, answers with specific evidence, checks it landed, uses policy-approved options (weekend batch in 804, installment in 805, bridge session per policy for 806) |
| 5 | **Trial close & next step** | 10 | Pressure close, fake deadline, or no next step (802, 803, 806) | Asks for payment but the follow-up is vague | Specific next step the parent agreed to, with time and owner (801: 11 AM callback + WhatsApp summary for father). Urgency only if factual and checkable (seat count) |
| 6 | **Compliance & honesty** | 20 | Any critical violation (see gate below) | Minor: incomplete disclosure or an unverifiable claim | Every claim matches the policy file and the evaluation |
| 7 | **Listening & talk balance** | 5 | Rep talk >70% or talks over the parent | Rep talk 56-70%, partly responsive | Rep talk <=55% **and** responds to what the parent said |

**Talk-ratio data** (from `3_sales_call_logs.csv`): 804: 44%, 801: 46%, 805: 48% (green); 802: 68% (amber); 806: 74%, 803: 84% (red). The ratio supports criterion 7 but never earns points alone: criterion 7 needs responsiveness evidence too.

### The compliance gate

If the rep breaches **any** item in the policy file's `forbidden_compliance_red_flags` for the pitched course, or any item on the list below, the total is **capped at 40** and a manager alert fires, whatever the other ratings.

**Critical violations:**
- Guaranteed outcomes or ranks (803: "Rank 1", "Harry Potter in 30 days")
- Refund promises beyond the 14-day policy (803: "100% refund anytime in 6 months")
- Discount above the 10% cap, or without a Team Lead approval code (803: 42%)
- Threats or false scarcity about the child's account (803: "blacklist")
- Claiming 1-on-1 for a group plan (803)
- Telling a parent to ignore the written policy ("off the record")
- Price dumping before explaining the method, for Maths class 205 (802)
- Pushing a standard batch after a young child was overwhelmed, for Chess class 401 (806)
- Rude or dismissive language ("kids always make excuses")

**Minor / unverified (do not trigger the gate, but are listed):** refund quoted without the "up to 4 classes attended" condition; claims the data cannot confirm (a "40% maths improvement," "top 1% teachers," "half the price of 1-on-1," an "Exam Pause" feature). These are labelled **UNVERIFIED**, never "false."

### Bands
85-100 Excellent. 70-84 Good. 50-69 Needs coaching. Below 50 Critical (manager review).

### Anti-gaming rules (LEAD-806 shows why)
1. **Mention is not execution.** Asking a discovery question earns credit only if the rep's *next turn* builds on the parent's answer. Reading three questions in a row earns 0 for criterion 2.
2. **Every rating needs a quote with a timestamp.** No quote, no points above 2.
3. **Cross-check against the evaluation.** Claims about the child must match `2_demo_class_evaluations.csv`. A mismatch is a criterion 1 failure.
4. **Parent signals override rep claims.** If the parent says "are you even listening," criterion 7 is capped at 2.
5. **Checklist phrases ("mandatory call checklist") trigger a gaming flag**, and the whole call is scored on content, not on keyword presence.
6. **The AI quotes, never infers.** If evidence is absent, the output is `"not_found"`, not a guess.

### Calibration targets (to sanity-test the prompts in Stage 4)
These are my expectations before running anything. If the prompt disagrees, I investigate the prompt *and* my expectation, but never tune until the numbers match.

| Call | Expected | Why |
|---|---|---|
| 801 Aarav | 78-90, no gate | Specific praise, parent-led discovery, agreed next step |
| 804 Meera | 80-92, no gate | Clean schedule fix; one unverifiable quote is minor |
| 805 Kabir | 75-90, no gate | Handles three objections; watch the unverified claims |
| 802 Zoya | <=40 (gated) | Price dumped at 00:30; policy 205 flag; ignored the parent's real question |
| 806 Ananya | <=40, expect ~25 (gated) | Gaming plus policy 401 flag; "force her" |
| 803 Vihaan | <=40, expect ~10-20 (gated) | Multiple critical violations |

---

## 3. CRM Taxonomy (what the AI must write to the CRM)

### 3.1 Lead intent

**Label:** Hot (8-10), Warm (5-7), Cold (1-4). **Score:** start at 3, apply signals, clamp to 1-10.

| Signal | Points |
|---|---|
| Parent states a payment intent with timing ("I'll pay after dinner") | +2 |
| Payment link opened or payment attempted (gateway data) | +2 |
| Parent asks logistics or method questions (batch time, fee, start date, how the teacher will address the child's gap) | +1 |
| Child engagement >= 4 in the evaluation | +1 |
| Price accepted without pushback | +1 |
| Concrete next step agreed, with a time | +1 |
| Unresolved objection at end of call (not Spouse_Decision or Competitor_Comparison; those use their own -1 rows) | -2 |
| Decision-maker absent or hesitant | -1 |
| Child engagement <= 2 | -1 |
| Competitor comparison unresolved | -1 |

**No double counting:** one objection takes one penalty only.

**Overrides:** parent says do-not-contact, then **score 1, Cold, stop all messaging.** Payment status `Paid`, then **label `Won`, stage `Enrolled_Paid`.**

**Worked examples** (Stage 4 will apply these to all six):
- **LEAD-805:** 3 +2 (will pay tonight) +2 (attempt made) +1 (asked fees/batch) +1 (engagement 4) +1 (price OK after installment) -1 (mother's hesitation) = **9, Hot**
- **LEAD-801:** 3 +2 (link opened twice) +1 (asked timing/fee) +1 (engagement 5) +1 (fee accepted) +1 (11 AM callback) -1 (husband absent) = **8, Hot**
- **LEAD-803:** do-not-contact override = **1, Cold**

### 3.2 Primary objection (one value, evidence required)

| Bucket | Use when | Sub-types |
|---|---|---|
| `Price` | Cost or cash flow is the stated blocker | `lump_sum_too_high`, `wants_installment` |
| `Spouse_Decision` | Another family member must approve | |
| `Schedule_Conflict` | Batch time clashes | `exam_period`, `extracurricular`, `timezone` |
| `Child_Not_Interested` | The child resisted | `demo_batch_mismatch` (age or level mismatch in the demo group) |
| `Competitor_Comparison` | Parent compares with another option | `online_competitor`, `local_tutor` |
| `Trust_Breakdown` | Parent distrusts the rep or company | (added: 803 does not fit the five required buckets) |
| `Other` | Free text, 80 characters max | |
| `None` | No objection raised | |

**Selection rules:** (1) the objection that blocks the next step, usually the last one raised; (2) the parent's words, not the rep's note, decide; (3) also list up to 2 `secondary_objections`; (4) mark each `resolved` / `unresolved` / `partially_resolved`.

**Applied to the data:** 801 `Spouse_Decision`, unresolved. 802 `Competitor_Comparison / local_tutor` (not Price), unresolved. 804 `Schedule_Conflict / extracurricular`, resolved. 805 `Competitor_Comparison / online_competitor`, resolved, with secondaries `Schedule_Conflict / exam_period` and `Price / wants_installment`. 806 `Child_Not_Interested / demo_batch_mismatch`, unresolved. 803 `Trust_Breakdown`.

### 3.3 Separate fields (these are *not* objections)
- **`payment_status`:** `none` / `link_sent` / `link_opened` / `failed` / `paid` (from `4_live_orders_and_invoices.csv`). A failed payment is a transaction state, not an objection, so it never goes in the objection field.
- **`do_not_contact`:** true / false, with a quote.
- **`compliance_flags`:** list of `{rule, timestamp, quote, severity}`.

### 3.4 Child's demo highlight
One sentence, taken from `demo_magic_moment_for_parent`. Must be paraphrased from that field only. If the field is empty, the value is `null`. The AI never invents a highlight.

### 3.5 Next Best Action (controlled vocabulary, one value)

| Value | Owner | When |
|---|---|---|
| `STOP_DO_NOT_CONTACT` | System + manager | Parent requested no contact |
| `ONBOARD_PAID` | Ops | Payment status `Paid` |
| `SEND_PAYMENT_RECOVERY` | Counsellor approves | Payment `failed` |
| `CALL_NOW` | Counsellor | High-intent, uncalled or callback overdue |
| `SCHEDULE_CALLBACK` | Counsellor | Parent agreed a time |
| `SEND_WHATSAPP_SEQUENCE` | Counsellor approves | Warm lead, open objection |
| `ACADEMIC_TEAM_CONTACT` | Academic team | Batch or level mismatch needs a fix |
| `MERGE_DUPLICATE` | CRM admin | Same user and student ID |
| `ESCALATE_MANAGER` | Manager | Compliance gate fired |

Each action carries a due time. `STOP`, `ESCALATE` and `ONBOARD` are system-triggered immediately. `CALL_NOW` is due within 2 hours of the demo.

### 3.6 Full CRM record (example for LEAD-805; Stage 4 produces all six)

```json
{
  "lead_id": "LEAD-805",
  "lead_intent": {"label": "Hot", "score": 9,
    "evidence": ["[03:28] \"Haan, yeh kaafi comfortable hai\"", "gateway: order 99405 attempted 20:45"]},
  "primary_objection": {"bucket": "Competitor_Comparison", "sub_type": "online_competitor",
    "status": "resolved", "evidence": "[01:14] PlanetSpark demo taken last week"},
  "secondary_objections": [
    {"bucket": "Schedule_Conflict", "sub_type": "exam_period", "status": "resolved"},
    {"bucket": "Price", "sub_type": "wants_installment", "status": "resolved"}],
  "demo_highlight": "Spoke 60 seconds on 'Should homework be banned?' with no filler words using the PEEL method.",
  "payment_status": "failed",
  "do_not_contact": false,
  "compliance_flags": [],
  "next_best_action": {"value": "SEND_PAYMENT_RECOVERY", "owner": "counsellor_approves", "due": "next 09:00 IST"},
  "overwritten_rep_note": {"original": "comparing with planetspark and school exam going on",
    "clean": "Agreed to 50% installment (Rs 5,400 down). UPI mandate failed (OTP timeout). Needs fresh one-time link."}
}
```
