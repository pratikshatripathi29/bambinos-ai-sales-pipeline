# WhatsApp Follow-Up: LEAD-805

**Status:** `SEND_PAYMENT_RECOVERY`  |  **Language:** Hinglish

## Pre-flight checks
- **A_do_not_contact**: pass (No request)
- **B_already_paid**: pass (Order 99405 Payment_Failed)
- **C_compliance_gate**: pass (Gate not triggered)
- **D_academic_hold**: pass (None)
- **E_failed_payment**: apply (Bank_OTP_Timeout_On_UPI_Mandate: payment recovery sequence)

## Messages

### Touch 1 (day 0): Calm no-blame recovery with a fresh one-time link (next morning)
> Namaste Rajesh sir 🙂 Kal raat Rs. 5,400 ka payment bank OTP time-out ki wajah se complete nahi ho paya, aapki koi galti nahi. Yeh naya one-time link hai: [PAYMENT_LINK]. UPI ya card, jo aapko aasaan lage. Kabir ne PEEL se 60 second bina 'umm' ke bola tha, hum usi flow ko aage badhayenge.

- Words: 54  |  Send mode: **auto_send**
- Addresses: Payment failure (not an objection)
- Approver checklist: Link is a one-time link, not a mandate; Amount is Rs. 5,400 as agreed (order 99405)

### Touch 2 (day 2): Offer help only if still unpaid
> Rajesh sir, agar payment link mein ab bhi dikkat aa rahi ho, toh main 5 minute ki call par help kar sakti hoon, ya aap card ya net banking se try kar sakte hain. Jo aapko comfortable ho.

- Words: 38  |  Send mode: **counsellor_approve**
- Addresses: Payment friction
- Approver checklist: Confirm payment is still unpaid

### Touch 3 (day 5): Respect the exam timing
> Rajesh sir, Kabir ke exams 15 tarikh se shuru ho rahe hain. Agar aap exams ke baad shuru karna chahein, toh bas bata dijiyega, main aapke hisaab se timing dekh lungi. Koi jaldi nahi hai.

- Words: 35  |  Send mode: **counsellor_approve**
- Addresses: Schedule_Conflict / exam_period + mother's 'after exams' view
- Approver checklist: Only if still unpaid; Check batch availability if he chooses to wait

## Manager note
Highest-ROI message in the batch: a committed buyer lost to an OTP timeout. Day 0 can auto-send because the parent already agreed to the amount and no new offer is made.
