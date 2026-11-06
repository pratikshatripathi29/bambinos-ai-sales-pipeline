# Stage 6: Revenue Impact, Adoption & 30-60-90 Rollout (Deliverable D)

All figures come from `funnel_math_model.xlsx` (live formulas; every assumption is one editable cell on the `Inputs` tab). Numbers in the case brief are marked **given**; everything else is an **assumption** to be replaced with measured data as soon as the pilot produces it.

---

## 1. The answer in five lines

1. At **1,000 demos/week and 15% conversion** (150 enrollments/week, 3.75 per counsellor), a **+2 point** lift adds **20 enrollments/week**; **+3 points** adds **30/week**.
2. Using a deliberately **conservative price** (every enrollment at the average India fee, 90% realization), that is about **Rs 1.02 crore/year at +2pp** and **Rs 1.53 crore/year at +3pp** at full run-rate.
3. After a realistic ramp (shadow, pilot, scale), **year-1 realized benefit is about Rs 85 lakh at +2pp** against about **Rs 33 lakh** of year-1 cost: roughly a **2.6x return**. Even at **+1pp** it returns about **1.3x**.
4. Managers do **not** get hours back versus today; they spend about the same time but cover **100% of calls instead of 2%**. Doing that by hand would need about **567 extra hours/week (about 14 managers)**. Each counsellor also saves about **3.3 hours/week** of admin.
5. A small pilot **cannot statistically prove** a 2-point lift quickly (it needs about 5,300 demos per arm, or about 10 weeks at 20 vs 20 counsellors), so the pilot is judged first on leading indicators.

---

## 2. Funnel math

| | Baseline | +2 points | +3 points |
|---|---|---|---|
| Conversion | 15% | 17% | 18% |
| Enrollments / week | 150 | 170 | 180 |
| **Extra enrollments / week** | | **20** | **30** |
| Extra enrollments / month | | 86.7 | 130 |
| Extra enrollments / year | | 1,040 | 1,560 |
| Extra per counsellor / week | | 0.5 | 0.75 |

Per counsellor: 25 demos a week, about 3.75 enrollments. **+2 points is about one extra enrollment every two weeks per counsellor.** That is the size of the ask, and it is small.

## 3. Revenue impact

Average catalog fee (6 classes, simple average): **Rs 10,917**. Net of an assumed 10% for discounts, installment timing and refunds: **Rs 9,825 per enrollment** (conservative case).

| | +2 points | +3 points |
|---|---|---|
| Extra revenue / month, India fee | Rs 8.5 lakh | Rs 12.8 lakh |
| **Extra revenue / year at full run-rate, India fee (conservative)** | **Rs 1.02 crore** | **Rs 1.53 crore** |
| Extra revenue / year, blended geo mix (70% India, 15% GCC, 15% US/UK, illustrative FX) | Rs 1.39 crore | Rs 2.08 crore |
| **Year-1 realized after ramp (83% of run-rate), India fee** | **Rs 85 lakh** | **Rs 1.28 crore** |

The blended case is higher because GCC and US/UK fees are about twice the India fee. I lead with the conservative case so the number survives a challenge.

## 4. Where the lift comes from (what must be true)

A target means little without a mechanism. This bottom-up model maps the lift to four levers, each tied to a leak found in the data. All inputs are assumptions and are the first things the pilot should measure.

| Lever | Assumption | Extra enrollments / week | Points |
|---|---|---|---|
| **A. Speed-to-lead** (call high-intent demos within 2 hours; 807 and 812 sat uncalled) | 6% of demos are not called within 24h; conversion rises from 5% to 12% | 4.2 | 0.42 |
| **B. Payment-failure recovery** (805 and 809 failed, 804 was chased after paying) | 1.5% of demos hit a failed payment; 40% are abandoned today; recovery saves 60% of those | 3.6 | 0.36 |
| **C. Objection-aware follow-up** (801 spouse, 802 competitor, 805 exams) | 40% of demos end as "thinking"; follow-up lifts them by 1.5 points | 6.0 | 0.60 |
| **D. Coaching the weakest quartile** (802, 803, 806 patterns) | Bottom-quartile reps handle 25% of demos, trail the median by 5 points, and coaching closes half the gap | 6.25 | 0.63 |
| **Total (base case)** | | **20.05** | **+2.0** |
| Pessimistic (half the effect) | | 10.0 | +1.0 |
| Stretch (1.5x the effect) | | 30.1 | +3.0 |

**Reading it:** +2 points needs each lever to deliver a moderate, believable effect. +3 points needs everything to work at once, so I present it as stretch. Levers may overlap, so treat the total as upper-leaning. The 12-lead sample is a curated set of traps, not a random sample, so it is **not** used to estimate rates.

## 5. Manager and counsellor hours

Assumptions: 1,000 counselling calls/week, 25-minute calls, 10 minutes of scoring per audited call.

| | Hours / week | Notes |
|---|---|---|
| Manager time today (2% audit = 20 calls) | 11.7 | |
| Manager time if 100% were audited **by hand** | 583 | About 14.6 full-time managers |
| Manager time **with AI** (100% scored; humans review 5% flagged exceptions + a 5% random quality sample, 10 min each) | 16.7 | |
| **Saved versus reaching 100% coverage by hand** | **about 567** | About 14 managers' time |
| Change in actual manager hours versus today | +5 | Slightly more, for 50x the coverage |
| Counsellor admin saved (AI writes the CRM note and drafts the follow-up, 8 min/call) | 133 total | **3.3 per counsellor per week** |

**Honest framing:** the value is **coverage and quality**, not fewer manager hours. Calls that were invisible (98%) become visible, and the compliance incident in call 803 would be caught within 15 minutes instead of at month-end.

## 6. Cost and return

| Item | Estimate |
|---|---|
| AI cost per call (transcription + three prompts) | about Rs 22 |
| AI cost per week (1,000 calls) | about Rs 22,100 |
| WhatsApp messages (about 2,500/week) | about Rs 2,500 / week |
| Platform and tooling | Rs 12 lakh / year |
| **Running cost** | **about Rs 25 lakh / year** |
| One-off build and rollout | Rs 8 lakh |
| **Year-1 total cost** | **about Rs 33 lakh** |
| Year-1 benefit at +2pp (after ramp) | Rs 85 lakh, **net Rs 52 lakh, 2.6x** |
| Year-1 benefit at +1pp (pessimistic) | Rs 43 lakh, net Rs 10 lakh, 1.3x |
| **Break-even lift** | **about 0.6 points** |

Vendor prices and token counts are illustrative; confirm before presenting. The conclusion is insensitive to them: even doubling the running cost leaves the +2pp case clearly positive.

**Not counted (upside):** refunds and complaints avoided by catching compliance breaches early, installment-recovery cash, better lifetime value from correctly matched batches (806), and reduced counsellor churn.

## 7. Can a pilot prove it?

Detecting a 2-point lift (15% to 17%) with 95% confidence and 80% power needs about **5,265 demos per arm**. At 20 pilot vs 20 control counsellors (500 demos/week each), that is about **10.5 weeks**. A 1-point lift needs about 20,500 per arm. So:

- **Judge the pilot first on leading indicators** that move fast: speed-to-lead, payment-recovery rate, CRM note quality, draft-acceptance rate, rep satisfaction, critical-flag accuracy.
- **Treat conversion as directional** during the pilot, then confirm with a staggered rollout and a longer comparison.
- Be explicit about this when presenting. Over-claiming a 4-week result would lose credibility with a data-minded Head of Sales.

---

## 8. Managing rep pushback: make the tool theirs

**The risk:** reps who feel policed will game the score (call 806 already shows this), argue every flag, or quietly stop using it. **The principle:** reps adopt a tool that makes them money and saves them time, and resist one that only judges them.

**Lead with what reps get, not what managers see.**

| What the rep gets | Why they care |
|---|---|
| **No more CRM typing**: the AI drafts the note, intent and next action | Saves about 8 minutes per call; Rohan's stale CRM stage (804) would simply not happen |
| **Follow-ups drafted for them**, referencing what the child actually did | Better replies, less effort |
| **Payment recovery runs itself** (805, 809) and **credit stays with the rep** | More closed deals, no extra work |
| **Reminders for the leads that matter** (a callback they promised, a high-intent demo) | Protects their commission |
| **Private coaching first**: two strengths, two fixes, with a better line to try | Feels like a coach, not a report card |
| **A dispute button** for any flag, reviewed by a human | Fairness |

**Rules of the road (publish them before launch).**
1. **Two clearly separate tracks.** *Coaching* (everything on the scorecard) is private to the rep for the first 30 days. *Compliance* (guarantees, off-policy discounts, threats) is zero-tolerance and goes to a manager. Reps always know which track a flag is on.
2. **No stack-ranking and no penalty from AI scores in the first 90 days.** Boards show **improvement**, not rank. The only exception is a confirmed critical compliance breach.
3. **Co-design the rubric with a rep council** of 6 counsellors, including strong performers. Publish the scorecard so nothing is secret.
4. **Reward outcomes, not checklists.** The rubric scores listening, not keywords, and the system is built so that the way to score high is the same as the way to sell more (call 806 fails both).
5. **Celebrate great calls publicly.** A weekly "Call of the Week" with the exact lines (801 Rohan's spouse handling, 805 Pooja's competitor answer) shows the tool spotting good work, not only bad.
6. **Start with volunteers.** Champions first (reps like those on 801, 804 and 805), then everyone.
7. **Tell reps what is recorded and why**, and confirm with HR and Legal how AI scores may and may not be used.

**Managers get a new job, not a surveillance dashboard.** A 20-minute weekly coaching session per rep, built from the AI's cards. They review exceptions, not everything.

**Adoption KPIs:** weekly active reps, coaching cards opened, drafts accepted without edit, approval turnaround, dispute rate and outcomes, rep satisfaction (NPS) on the cards.

---

## 9. 30-60-90 day rollout

### Days 1-30: Fix the leaks and run in shadow mode
| Week | Actions |
|---|---|
| 1 | Approved **fact sheet** (batches, seat counts, features, credentials, prices including class 108, GBP and the age 5-6 micro-batch). Align the payment gateway cap to the policy's **10%**; require a Team Lead code above it. Get call recording to 100% coverage. |
| 2 | Payment webhook into the CRM (stage sync, cancel chases, queue recovery); demo-completed watcher; duplicate merge; suppression list. These are low-risk and high-return. |
| 3 | **Shadow mode**: audit 100% of calls, no rep visibility. Calibrate against human scoring on about 100 calls. Test Hinglish transcription accuracy. |
| 4 | Rep council reviews the rubric; WhatsApp templates submitted for approval; baseline metrics measured (true conversion by rep, time-to-first-call, payment-failure rate). |

**Exit criteria:** AI and human reviewers agree on critical flags (target 90%+); scores within 10 points on 80%+ of calls; templates approved; baselines recorded.

### Days 31-60: Pilot
- **20 volunteer counsellors vs 20 control.** Coaching cards, AI CRM fields, approval queue, auto-sent payment recovery, and manager alerts for critical flags go live for the pilot group.
- Weekly calibration meeting; every false-positive flag is reviewed and fed back into the prompts.
- Regression test (the 6 sample calls) before any prompt change.

**Exit criteria (leading indicators):** 90%+ of high-intent demos called within 2 hours; payment-recovery messages sent next morning on 100% of failures; 70%+ of drafts accepted with little or no edit; critical-flag false positives under 10%; rep satisfaction positive.

### Days 61-90: Scale and lock in
- Roll out to all 40 counsellors (staggered, so the comparison keeps its value).
- Manager dashboard and weekly coaching ritual in place.
- Align incentives (recovered payments credited to the rep).
- Quarterly prompt and policy review; add GCC and US-friendly send windows.
- **Go/no-go for more automation:** only after false-positive and complaint data support it, consider auto-sending more templates.

**Day-90 targets:** 100% call coverage; critical flags reach a manager within 15 minutes; leading indicators hit; directional conversion lift in the pilot versus control. **Statistical confirmation of the conversion lift arrives around day 105** (about 10.5 weeks after the pilot starts).

---

## 10. Risks and mitigations

| Risk | Mitigation |
|---|---|
| Reps resist or game the score | Section 8; scoring based on evidence, not keywords |
| AI misjudges a call | Quotes must match the transcript; human reviews every critical flag; dispute button |
| Transcription errors on Hinglish | Test on call 805 first; low-quality transcripts route to human review |
| A bad message reaches a parent | Humans approve persuasion; only transactional messages auto-send; kill switch |
| Privacy and consent | Recording notice, data-processing agreement, retention policy; confirm with Legal |
| WhatsApp template delays | Submit in week 4; fall back to counsellor-sent messages meanwhile |
| Lift smaller than hoped | Break-even is only about 0.6 points; the compliance and visibility value remains |
| Policy and catalog gaps persist | Fact sheet in week 1; nightly check flags missing prices |
