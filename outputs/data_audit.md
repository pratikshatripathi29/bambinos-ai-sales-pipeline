# Stage 1: Data Audit & Pipeline Leak Report

**Scope:** `1_crm_leads.csv` (12 leads), cross-checked against `2_demo_class_evaluations.csv`, `3_sales_call_logs.csv`, `4_live_orders_and_invoices.csv`, `reference_courses_pricing_and_compliance_policy.csv` and the 6 call transcripts.
**Snapshot time:** the latest timestamp in the data is `2026-11-03 20:45` (LEAD-805 payment failure). "Overdue" below is measured against that.
**Method rule:** every finding cites a field, row or transcript timestamp. Anything the data cannot confirm is labelled **UNVERIFIED**, not assumed.

---

## 1. Headline

Of 12 leads, **every one has at least one leak.** Only LEAD-801's rep note is accurate, and even that CRM row misses the payment-link signal. The leaks fall into these types:

| Leak type | Leads | Count |
|---|---|---|
| Rep disposition contradicts transcript / evaluation | 802, 803, 806 | 3 |
| Stale CRM stage (already paid, still chasing) | 804 | 1 |
| Failed payment, no recovery action scheduled in time | 805, 809 | 2 |
| High-intent demo, never called, no follow-up scheduled | 807, 812 | 2 |
| Useless or invalid notes and dates | 808 ("ok"), 810 ("cb", follow-up date before last call) | 2 |
| Duplicate lead routed to a second counsellor | 811 (duplicate of 801) | 1 |
| Compliance incident (guarantees, unauthorized discount, threat) | 803 | 1 |
| Called leads with no call log, so **un-auditable** | 808, 809, 810 | 3 |

(Some leads appear in more than one row; the 3 un-auditable leads overlap with others.)

---

## 2. Lead-by-lead leak register

Priority: **P0** = money or compliance risk right now. **P1** = high-value, fixable this week. **P2** = hygiene.

| P | Lead | What the CRM says | What the evidence shows | Action |
|---|---|---|---|---|
| P0 | **803** Vihaan | Stage `Follow_Up_Hot`; disposition "Interested"; note "good call sent payment link will pay today"; follow-up scheduled `2026-11-03 18:00` | Parent ended the call at 03:54: "Do not call me again!" after a fake guarantee, a 42% discount and a blacklist threat. Order 99403 is `Unpaid_Flagged_Discount_Anomaly`. The scheduled 18:00 follow-up would re-contact a parent who demanded no contact. | **Freeze lead. Set do-not-contact. Cancel the 18:00 follow-up. Void link 99403.** Escalate to Sales Head. Audit all of Amitabh's other calls. |
| P0 | **804** Meera | Stage `Payment_Link_Sent`; follow-up scheduled `2026-11-03 20:00` | Order 99404 **Paid** at `2026-11-03 11:40:12` (USD 265). Rep never updated the stage. A chase at 20:00 would go to a customer who already paid. | Move to `Enrolled_Paid`. Cancel the chase. Send an onboarding message, not a sales message. |
| P0 | **805** Kabir | Stage `Follow_Up_Warm`; disposition "Thinking"; next follow-up `2026-11-05 12:00` | Parent agreed to pay Rs 5,400 that night (03:28). Order 99405 **failed** at 20:45 (`Bank_OTP_Timeout_On_UPI_Mandate`). Next follow-up is about 39 hours after the failure. "Thinking" is wrong: this is a committed buyer with a payment problem. | Recovery message the next morning with a fresh **one-time** payment link (the failed attempt was a mandate flow). Reclassify as Hot. |
| P0 | **809** Devansh | Stage `Payment_Link_Sent`; disposition "Card error" | Order 99409 failed with `3DS_Authentication_Declined_By_Issuer`. That is a bank-verification decline, not a card error, so the fix differs (approve in banking app, another card, or wallet). The parent attempted payment about 15 minutes after the call, which is strong intent. **No call log or transcript exists for this call.** | Send fresh link plus plain-language help. Add the call to the audit backlog. |
| P0 | **801** Aarav | Stage `Follow_Up_Warm`; "will ask husband and tell tomorrow"; callback `2026-11-03 11:00` | Strong call. Order 99401 link **opened twice** at `2026-11-02 21:15` (consistent with the father reading it after the 8:30 PM conversation). Rep promised to hold the last seat **until 11:00 on 11-03**. CRM `last_call_at` is still `11-02 17:45`, so no evidence the callback happened. Lead 811 (below) shows the parent downloaded the brochure on 11-03 at 08:10. | Treat as Hot. Confirm the callback happened. If not, call now, and check the seat. |
| P1 | **811** (dup of 801) | `New_Duplicate_Lead`, assigned to **Pooja**; "Not called" | Same `user_id` 51001, `student_id` 78001, same mobile and email as 801. Created `11-03 08:10` from a website brochure download. | **Merge into 801. Keep Rohan as owner. Block Pooja's outreach** (a second counsellor cold-pitching a family mid-decision). Log the download as an intent signal. |
| P1 | **802** Zoya | Stage `Follow_Up_Cold`; "Price issue / price high thinking"; no follow-up date | The parent rejected the AED 100 discount herself ("doesn't answer my question"). Her real question: why does Zoya fail word problems and how is this better than a AED 350 local tutor. The demo evaluation holds the exact answer (Zing Bar-Model solved two Grade-6 British-curriculum fraction word puzzles on her own). The rep said "let me check... she did well" and never used it. | Reclassify objection: **Competitor Comparison (local tutor)**, not Price. Reassign or coach. Send a method-based message, no discount. |
| P1 | **806** Ananya | Stage `Follow_Up_Cold`; "Child not interested"; no follow-up date | Evaluation: engagement 2/5, `Absolute_Beginner_Overwhelmed_In_Group`, recommended `Micro_Batch_3_Kids_Or_1on1_Bridge`. Child was happy for the first 10 minutes. The barrier is **demo batch mismatch**, which policy says to fix with a free 1-on-1 bridge session or an age 5-6 micro-batch (max 3). Rep pushed the standard batch instead. | Reclassify to **Demo Batch Mismatch (a Child Not Interested sub-type)**. Academic team, not Karan, should contact the parent with the bridge session offer. |
| P1 | **807** Arjun | `Demo_Completed_Uncalled`; `last_call_at` NULL; `next_followup_at` NULL | Evaluation: engagement 5/5, scored 5/5 on the Olympiad challenge and **asked when the regular batch starts**. Demo ended `11-02 15:30`. No call, no follow-up scheduled. Value Rs 13,500. | Call within hours, referencing the inference challenge. |
| P1 | **812** Riya | `Demo_Completed_Uncalled`; both call fields NULL | Evaluation: engagement 5/5, asked how Karma Yoga applies to school and sports, mother clapped. Demo `11-03 06:30`. Teen Leadership track is not in the pricing catalog (see section 4). | Call at a US-friendly hour. Verify the track and price first. |
| P2 | **808** Sara | "Busy" / note "ok"; next follow-up NULL | Evaluation: engagement 4/5, asked for **two extra rounds** of the Mystery Box game. `last_call_at` is `11-02 20:10` but **no call log exists**. Class 108 has **no entry in the pricing policy**, so no price can be verified. Owner is Amitabh (see rep patterns). | Schedule a callback at an agreed time. Get the 108 price confirmed before quoting. Audit the call. |
| P2 | **810** Myra | "Call back" / note "cb" | `next_followup_at` = `2026-11-01 10:00`, which is **before** the demo (`11-02 11:30`) and before `last_call_at` (`11-02 12:30`). That date is impossible, so no valid follow-up exists. Evaluation is positive (mastered the b/d trick in 5 minutes). No call log. | Fix the date. Audit the call. Callback with the b/d moment. |

---

## 3. Pricing & discount verification (rep claims vs policy file)

| Lead | Rep quoted / order shows | Policy | Verdict |
|---|---|---|---|
| 801 | Rs 12,000 (= Rs 250 x 48) | Rs 12,000 | OK. Refund stated as "100% risk-free" without the "up to 4 classes attended" condition: **incomplete disclosure (low)** |
| 802 | AED 1,200 (6-month); AED 100 off | AED 1,200; cap AED 120 | Discount = 8.3%, **within cap**. The 12-month "96 classes, AED 2,100" package is **not in the catalog (UNVERIFIED)**. Order 99402 shows `standard_amount` **12000.0 AED**, a 10x data-entry error (net 1,100 is right) |
| 803 | Rs 9,500 list; Rs 4,000 off; link shows Rs 5,500 | List Rs 9,500; cap **Rs 950** | Discount = 42.1%, **about 4x over cap**. Violation |
| 804 | USD 265 | USD 265 | OK. Matches payment |
| 805 | Rs 12,000, 10% off (Rs 1,200), 50% down = Rs 5,400 | Cap Rs 1,200; installment = 50% down + 50% at Day 30, no extra cost | **Within policy.** The policy does not prohibit combining the max discount with installments. Order arithmetic is consistent (12,000 - 1,200 = 10,800; half = 5,400) |
| 806 | Rs 11,000; "10% off = Rs 9,900" | Rs 11,000; cap Rs 1,100 | Discount is at cap, **allowed**. The problem is false urgency ("pay before 6 PM") and ignoring the micro-batch rule |
| 807 | no order | Rs 13,500 | n/a |
| 809 | GBP 210 | **No GBP price in policy** (INR, AED, USD only) | **UNVERIFIED** |

**Gateway rule mismatch:** order 99403's flag reads "Discount >15% Max Cap," but the policy cap is **10%**. The gateway would let a 10-15% discount through unflagged. Align the gateway to 10%.

---

## 4. Catalog & data-integrity gaps (these cause reps to improvise)

1. **Class 108** (Young Communicators GCC Track, LEAD-808) is missing from the pricing policy.
2. **"Unbox Chess Little Starters (Age 5-6 Only)"** (the recommended track for LEAD-806) has no catalog entry or price. Without it, the policy-mandated fix cannot be quoted.
3. **"Little Yogi Teen Leadership Track"** (LEAD-812) is not named in the catalog. Class 302 is listed as Ages 6-14, so it may be covered, but this is **UNVERIFIED**.
4. **GBP pricing** does not exist for UK leads.
5. **12-month / 96-class packages** are not in the catalog, yet a rep quoted one.
6. **Timestamps carry no timezone label.** They appear to be stored in each lead's local time (LEAD-804's `09:45` equals the PST time in its call note; LEAD-805's `20:45` equals the IST time in its note). A pipeline that schedules WhatsApp messages must normalize these.
7. **Only 6 of 9 called leads have call logs.** Leads 808, 809 and 810 show a `last_call_at` but have no transcript or log. This is the "2% audit" problem visible in the data.
8. **Payment events do not flow into the CRM.** 801 (link opened twice), 804 (paid), 805 and 809 (failed) all show a CRM stage that ignores the gateway. This is the biggest structural leak, and it is what the pipeline must fix first.
9. **Evaluation text for LEAD-804 can't confirm a quote the rep used.** The rep cited Acharya Aditi's note calling Meera's Arjuna question "the most thoughtful question of the week." The evaluation row contains the shloka/gymnastics moment but not that quote. **UNVERIFIED** (the note may exist elsewhere), and a reminder that the AI must not repeat unverifiable quotes in parent messages.

---

## 5. Rep patterns (observations, not verdicts: each rep has only 1-3 leads in this data)

| Rep | Leads | Pattern |
|---|---|---|
| Rohan (204) | 801, 804, 809 | Strong consultative calls (talk ratio 44-46%). Weakness is **CRM hygiene**: stale stage on 804, "card error" mislabel on 809. A coaching story, not a compliance story. |
| Pooja (215) | 805 (and misrouted 811) | Strong Hinglish call; handled competitor, exams and installments well. |
| Sneha (209) | 802, 807, 812 | Price dumped at 00:30 on 802; **two high-intent demos uncalled** (807, 812). Possible capacity or prioritization issue. |
| Amitabh (212) | 803, 808 | Severe compliance incident on 803; 808 has a note of "ok" and no call log. **Recommend a manager review of all his recent calls.** |
| Karan (218) | 806, 810 | Rubric-gaming and a batch-mismatch miss on 806; invalid follow-up date and note "cb" on 810. |

---

## 6. Money at stake

Native currency, no conversion. Values are list or agreed net prices.

| Bucket | Leads | Value |
|---|---|---|
| **Recoverable pipeline** | 801, 802, 805, 806, 807, 808, 809, 810, 812 | **INR 56,800** (801: 12,000; 805: 10,800 net of discount; 806: 11,000; 807: 13,500; 810: 9,500) + **AED 2,300** (802: 1,100 net; 808: 1,200 *proxy using class 104's GCC price, UNVERIFIED*) + **USD 265** (812) + **GBP 210** (809) |
| Approx. INR equivalent | | **about Rs 1.55 lakh**, at illustrative round-number FX of USD 85 / AED 23 / GBP 110 (not live rates) |
| Lost / compliance incident | 803 | Rs 9,500 list. Brand and legal exposure is the larger risk (a written-looking guarantee and an off-policy refund promise were made verbally) |
| Already paid, CRM wrong | 804 | USD 265 (revenue is safe; the risk is a chase message that damages trust) |
| Duplicate, no extra revenue | 811 | n/a |

**Note on 806:** the true price of the recommended micro-batch is unknown, so Rs 11,000 is a placeholder.

---

## 7. What this means for the system design

The data tells us what the pipeline must do, in order of impact:

1. **Check payment status before any message** (804 would have been chased after paying; 805 and 809 need recovery, not nudges).
2. **Honour do-not-contact before anything else** (803).
3. **Reclassify dispositions from transcript + evaluation evidence**, not rep notes (802, 806).
4. **Surface uncalled high-intent demos within hours** (807, 812).
5. **Merge duplicates** and keep one owner (801/811).
6. **Flag catalog gaps** to Ops rather than letting reps improvise prices.
7. **Validate dates and require call logs** for every call (808, 809, 810).

These seven rules feed directly into Stage 3 (the prompts) and Stage 5 (the workflow guardrails).
