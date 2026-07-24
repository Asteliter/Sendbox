# Reference Clause Patterns (for grounding / RAG)

Short library of common clause categories in leases, vendor agreements, and employment offers — what's typical versus what commonly warrants a flag. This is meant as grounding context for an agent (via RAG or embedded in a system prompt), not as legal guidance to end users.

## 1. Auto-Renewal / Renewal
- **Typical:** Fixed term with a defined renewal window (30-60 days notice), renewal requires opt-in, or lease simply ends and converts to month-to-month.
- **Common flag pattern:** Long or unusual notice windows (90+ days), automatic renewal for a full additional term (vs. month-to-month), or silence-equals-consent framing that a reader could easily miss ("Renewal", "Automatic Extension", "Evergreen").
- **Why it matters to a non-lawyer:** Missing a single notice deadline can lock someone into another full term.

## 2. Liability / Indemnification
- **Typical:** Party responsible for damage caused by their own negligence or acts.
- **Common flag pattern:** "Regardless of cause," "regardless of fault," broad indemnification covering third-party or counterparty's own acts/omissions, uncapped liability.
- **Why it matters:** Can shift responsibility for events entirely outside the signer's control.

## 3. Early Termination
- **Typical:** Termination fee tied to actual costs (e.g., unamortized broker fee, remaining short notice period).
- **Common flag pattern:** Flat fee equal to several months of payment regardless of remaining term or actual harm; fee due immediately in full.

## 4. Dispute Resolution / Arbitration
- **Typical:** Reference to a governing law and venue for lawsuits.
- **Common flag pattern:** Mandatory binding arbitration, jury-trial waiver, class-action waiver — removes court access and appeal rights, often buried in boilerplate near the end.

## 5. Payment / Late Fees
- **Typical:** Grace period, flat or capped late fee.
- **Common flag pattern:** Compounding penalties, fees disproportionate to the missed amount, acceleration clauses (entire remaining balance due on one missed payment).

## 6. Non-Compete / Confidentiality (employment/vendor)
- **Typical:** Time- and geography-bounded restriction tied to a legitimate business interest.
- **Common flag pattern:** Indefinite duration, overly broad geographic or industry scope, restrictions surviving termination without compensation.

## 7. Termination for Cause vs. Convenience
- **Typical:** Either party may terminate for material breach with a cure period.
- **Common flag pattern:** One-sided termination rights (only one party can terminate at will), no cure period, immediate forfeiture of deposits/fees on termination.

---
**Usage note:** This library exists to help an agent recognize *deviation from common patterns*, not to certify what is "enforceable" or "fair" in any jurisdiction. Every flagged clause should still be surfaced with the standard disclaimer: informational only, not legal advice, recommend review by a licensed attorney for anything non-standard.
