# AI Post-Demo Conversion & Call Intelligence Pipeline

Take-home case for **AI Program Manager (Sales), Bambinos.live**.

**Author:** Pratiksha Tripathi

An AI pipeline that takes a demo or counselling call and automatically (1) **audits call quality** from timestamped evidence, (2) **cleans the CRM** and scores lead intent, and (3) **drafts a personalized WhatsApp follow-up** or, when messaging would be wrong, a **STOP alert**.

No code is required to run it: it is three prompts, a Google-Sheet-style tracker, and an n8n workflow specification.

---

## Start here (3 files, 5 minutes)

| Open this | To see |
|---|---|
| [`outputs/summary_table.csv`](outputs/summary_table.csv) | All 12 leads on one page: score, intent, objection, next action |
| [`outputs/call_audits/LEAD-803.md`](outputs/call_audits/LEAD-803.md) then [`outputs/whatsapp_sequences/LEAD-803.md`](outputs/whatsapp_sequences/LEAD-803.md) | A call with 7 critical compliance flags, and the system sending **no message** |
| [`outputs/whatsapp_sequences/LEAD-805.md`](outputs/whatsapp_sequences/LEAD-805.md) | A Hinglish payment-recovery sequence for a committed buyer whose installment failed |

The full written case (Deliverables A, B, D) is the PDF report submitted with this repository.

---

## Results on the six sample calls

| Lead | Score | Gate | Intent | Primary objection | Next best action | Follow-up |
|---|---|---|---|---|---|---|
| 801 Aarav | 86 Excellent | no | Hot 8 | Spouse_Decision (open) | CALL_NOW | 3 touches, counsellor approves |
| 802 Zoya | 27 Critical | **yes** | Cold 4 | Competitor_Comparison / local tutor | ESCALATE_MANAGER | 3 touches, manager approves |
| 803 Vihaan | 20 Critical | **yes** (7 critical) | Cold 1 | Trust_Breakdown | STOP_DO_NOT_CONTACT | **STOP, no messages** |
| 804 Meera | 88 Excellent | no | Won 10 | Schedule_Conflict (resolved) | ONBOARD_PAID | Onboarding only |
| 805 Kabir | 86 Excellent | no | Hot 9 | Competitor_Comparison (resolved) | SEND_PAYMENT_RECOVERY | Hinglish recovery, day 0 auto-send |
| 806 Ananya | 20 Critical | **yes** + gaming | Cold 1 | Child_Not_Interested / demo_batch_mismatch | ESCALATE_MANAGER, then ACADEMIC_TEAM_CONTACT | 3 drafts **blocked** until Academic confirms |

The 12-lead CRM audit ([`outputs/data_audit.md`](outputs/data_audit.md), [`outputs/pipeline_leaks.csv`](outputs/pipeline_leaks.csv)) found that **every lead had at least one leak**: a customer who had paid was still scheduled for a chase (804), two failed payments had no fast recovery (805, 809), two high-intent demos were never called (807, 812), and a duplicate lead went to a second counsellor (811).

---

## How it works

```
Call ends -> transcript -> assemble context (CRM row, demo evaluation, order, policy)
          -> PROMPT 1  Call audit        (score, compliance flags, coaching)
          -> PROMPT 2  CRM extraction    (intent, objection, highlight, next action)
          -> SAFETY ROUTER (code): do-not-contact > already paid > academic hold > compliance gate
          -> PROMPT 3  WhatsApp follow-up (3 touches, or STOP alert)
          -> approval gate -> send
```

Design rule: **code enforces the critical rules; AI exercises judgement.** Do-not-contact, payment status, discount maths and send windows are checked by deterministic code. Humans approve persuasive messages; only transactional ones auto-send.

Full diagrams, the guardrail table and the n8n node specification are in [`workflow/pipeline.md`](workflow/pipeline.md).

---

## Folder map

```
prompts/        the three system prompts (role, inputs, step-by-step rules, JSON schema, never-do list)
docs/           scorecard_and_taxonomy.md       Deliverable A
                funnel_math_and_rollout.md      Deliverable D
                funnel_math_model.xlsx          live-formula revenue/hours/cost model
                loom_script.md                  2-3 minute walkthrough script
workflow/       pipeline.md                     Deliverable B (diagrams, guardrails, n8n spec)
inputs/         the 6 transcripts and 5 CSVs from the assessment repository (unmodified)
outputs/        summary_table.csv, data_audit.md, pipeline_leaks.csv
                Bambinos_AI_Sales_CRM_Tracker.xlsx   Google-Sheet-ready tracker with live formulas
                call_audits/ (6)  crm_cleaned/ (12 + all_12_leads.json)  whatsapp_sequences/ (6)
```

---

## How to reproduce a result

1. Open a new Claude chat.
2. Paste the contents of `prompts/1_call_audit_prompt.md` (the part under "SYSTEM PROMPT").
3. Paste one transcript from `inputs/call_transcripts/`, plus the matching rows from the CSVs in `inputs/data/`.
4. Compare the JSON with `outputs/call_audits/LEAD-80X.json`. Run Prompt 2 on that output, then Prompt 3 on both.

**Regression test:** the six calls have expected score bands (see `docs/scorecard_and_taxonomy.md`): 801, 804, 805 should land at 75 to 92 with no gate; 802, 803, 806 should be gated and at most 40. Re-run them before any prompt change.

---

## Honest notes and limitations

- **The outputs were produced by applying the three prompts in a Claude conversation, not by an automated API run.** A script then verified that every evidence quote appears verbatim in the transcript, that score arithmetic is correct, and that every WhatsApp message is within the 60-word limit.
- **Many claims are labelled `UNVERIFIED`** because the data contains no batch roster, curriculum document or feature list. The recommended fix is an approved fact sheet.
- **The intent score has a known blind spot:** Ananya (806) scores 1/10 although her mother stated a clear condition for enrolling. A "parent states a fixable condition" signal is proposed for version 2.
- **Leads 807 to 812** have CRM records but no WhatsApp drafts: they need a human call first, or have no transcript.
- **Revenue figures are model outputs, not forecasts.** The 12-lead sample is curated, FX rates are illustrative, LEAD-808 uses a proxy price, and LEAD-806 a placeholder.
- **Legal, privacy and WhatsApp-policy points** (recording consent, data protection, opt-in and templates) are listed in `workflow/pipeline.md` and must be confirmed by the company before launch.
- Personal data in the sample files is masked, as provided in the assessment repository.
