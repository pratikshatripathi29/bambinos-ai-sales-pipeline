# WhatsApp Follow-Up: LEAD-802

**Status:** `SEND_SEQUENCE`  |  **Language:** English

## Pre-flight checks
- **A_do_not_contact**: pass (No request)
- **B_already_paid**: pass (Order 99402 unpaid, link not clicked)
- **C_compliance_gate**: apply (Gate triggered (policy 205 price dump): manager_approve on all messages; release the false deadline; no discount)
- **D_academic_hold**: pass (None)
- **E_failed_payment**: pass (None)
- **F_standard**: apply (Conversion sequence, Competitor_Comparison (local tutor) variant)

## Messages

### Touch 1 (day 0): Release the deadline; answer the method question the rep skipped
> Hi Amina ma'am, thank you for your time today. Please ignore the 30-minute link deadline; there's no rush. You asked what method Mr. Vikram used: Zoya solved two fraction word problems from the British curriculum on her own with our visual Bar-Model, and said it was 'so easy!'

- Words: 48  |  Send mode: **manager_approve**
- Addresses: Competitor_Comparison / local_tutor: the unanswered method question
- Approver checklist: No discount mentioned; Facts match evaluation 9002; Deadline is explicitly withdrawn

### Touch 2 (day 2): Explain the method without criticising the tutor
> Hi Amina ma'am, Zoya's challenge is guessing the operation in story problems. The Bar-Model has her draw the problem first, then choose the operation. Would you like a short sample problem solved this way, to compare with what her tutor does?

- Words: 41  |  Send mode: **manager_approve**
- Addresses: Competitor_Comparison / local_tutor
- Approver checklist: Sample problem prepared by the Maths team; No criticism of the tutor

### Touch 3 (day 5): Easy close with a choice
> Hi Amina ma'am, no pressure at all. If it helps, I can arrange a short call with our academic team to explain the method, or you can continue with her tutor and revisit whenever you like. Whatever works best for Zoya.

- Words: 41  |  Send mode: **manager_approve**
- Addresses: Competitor_Comparison / local_tutor
- Approver checklist: Academic team availability confirmed

## Manager note
Consider reassigning this lead to a different counsellor. Price-led follow-up would repeat the original mistake.
