# WhatsApp Follow-Up: LEAD-804

**Status:** `STOP_SALES_SEQUENCE`  |  **Language:** English

## Pre-flight checks
- **A_do_not_contact**: pass (No request)
- **B_already_paid**: stop (Order 99404 Paid 2026-11-03 11:40:12 (USD 265))

## STOP alert (info)
LEAD-804 already paid USD 265 two hours after the call. The CRM still shows Payment_Link_Sent with a chase scheduled at 20:00.

**System actions:**
- Move stage to Enrolled_Paid
- Cancel follow-up scheduled 2026-11-03 20:00
- Ops: confirm seat in Sat-Sun 9:30 AM PST batch
- Send onboarding message once first class date is filled

## Messages

### Touch 1 (day 0): Onboarding confirmation (not a sales message)
> Hi Neha, welcome to the Bambinos family! We've received your USD 265 payment for Meera's Little Yogi track. We're finalising her place in Acharya Aditi's Saturday-Sunday 9:30 AM PST batch and will share her first class details here: [FIRST_CLASS_DATE]. Loved how she linked 'Samatvam' to her balance-beam routine!

- Words: 48  |  Send mode: **counsellor_approve**
- Addresses: n/a (already enrolled)
- Approver checklist: Ops has filled [FIRST_CLASS_DATE] and confirmed the seat; Message is onboarding only, no upsell

## Manager note
Referral-source lead: a thank-you and a referral ask can come after the first class, never before.
