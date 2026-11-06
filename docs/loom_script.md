# Loom walkthrough script (about 2 minutes 45 seconds)

**Before you record:** open the repository on GitHub in your browser and have these tabs ready, in this order:
1. `outputs/summary_table.csv`
2. `outputs/call_audits/LEAD-805.md`
3. `outputs/call_audits/LEAD-806.md`
4. `outputs/call_audits/LEAD-803.md`, then `outputs/whatsapp_sequences/LEAD-803.md`
5. `outputs/whatsapp_sequences/LEAD-804.md`
6. `docs/funnel_math_and_rollout.md` (scroll to section 1)

Speak naturally. The script below is a guide, not something to read word for word. At about 150 words per minute it runs roughly 2 minutes 45.

---

### 0:00 to 0:15: The problem (show `summary_table.csv`)
"Hi, I'm [name]. Bambinos audits about 2% of its counselling calls, CRM notes are vague, and follow-ups are generic. I built a pipeline that audits every call from evidence, cleans the CRM, and writes follow-ups, with rules about when not to message. This table shows all twelve leads."

### 0:15 to 0:55: A strong call, call 805 Kabir (show the audit, then scroll to the CRM and WhatsApp files)
"Here's a strong Hinglish call. It scores 86. Every rating has a timestamped quote, and a script checked each quote against the transcript, so nothing is invented. The rep cited the exact PEEL moment from the demo and handled a competitor, exams and cash flow. But the CRM said 'Thinking'. The AI saw that the installment payment failed at 8:45 PM, scored him Hot 9, and drafted a calm Hinglish recovery message with a fresh one-time link, which is safe to auto-send because he'd already agreed to pay."

### 0:55 to 1:30: A compliance failure, call 806 Ananya (show the audit)
"This rep read the call checklist aloud in the first thirty seconds to game the score. The anti-gaming rule gives credit only if the next turn builds on the parent's answer, so he scores 20. The six-year-old was overwhelmed by older boys. Policy says offer a bridge session or a micro-batch. He pushed the standard batch, so the compliance gate fires. The CRM said 'child not interested', but it's really a batch mismatch. The follow-up drafts are written but blocked until Academic confirms an option exists."

### 1:30 to 2:05: The stop trigger, call 803 Vihaan (show the audit, then the WhatsApp file)
"This is the one that matters most. The rep promised Rank 1, a six-month refund, a forty-two percent discount against a ten percent cap, and threatened to blacklist a seven-year-old. Seven critical flags, each with an exact quote. The parent said 'do not call me again', so the system generates no message at all. It cancels the scheduled follow-up, voids the payment link, and alerts the manager. The right output here is silence."

### 2:05 to 2:25: Don't chase a paying customer (show `LEAD-804`)
"Call 804 already paid two hours later, but the CRM was still chasing her. The payment status check catches that and sends onboarding instead of a sales message."

### 2:25 to 2:50: The business case (show the funnel math doc)
"At a thousand demos a week, a two-point lift is twenty more enrollments a week, about one crore a year on conservative pricing, and roughly a 2.6 times return in year one. Managers get full coverage instead of two percent. I also flagged that a small pilot can't prove a two-point lift quickly, so I judge it first on leading indicators. And to win over reps, the AI writes their CRM notes, scores stay private for thirty days, and coaching is kept separate from compliance."

### 2:50 to 3:00: Close
"Everything is in the repo, with a README and a 30-60-90 plan. Thanks for watching."

---

**Recording tips**
- Use the free Loom plan; record your screen with your voice only (face is optional).
- Zoom the browser to 125% so text is readable.
- Do one practice run. If you go over 3 minutes, cut the 804 section.
- Paste the Loom link into the submission form after you finish.
