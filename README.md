# Damages & Claims Log

A single web page (`index.html`) for logging van damage, parcel claims, third-party damage and fines/PCNs for the DPD franchise. It is in the same style as the Driver Pay Log, the DPD P&L Tracker and the EV Charging Log, and its downloads go straight into the pay log and the P&L.

The page is published as a claude.ai Artifact, which stores the log in its own database. If you open `index.html` straight from this repo instead, it saves to that browser only.

## First-time setup (FDs, drivers & rules tab)

1. **FDs:** FD number/name, **email** and **depot** (Raunds / Glenfield by default), as in the P&L Tracker. Every claim is linked to an FD, so you always know which FD, email and depot a charge belongs to.
2. **Drivers:** name (same as in the Driver Pay Log), depot and, optionally, their usual FD (fills in automatically when you log a claim).
3. **Rules:** the first day of a 4-week pay period (2 Nov 2026 by default, the same as the Driver Pay Log), the depot list, and whether to **hold** deductions until the driver has signed (off by default, so unsigned deductions are flagged but still taken).

## What is recorded per claim

- Date of incident and date reported
- Type: van damage / parcel lost / parcel damaged / third-party damage / fine or PCN
- Driver, FD (with email and depot), route and van reg
- DPD claim ref and parcel tracking number
- Short description and a link to photos/evidence
- Total amount charged, insurance claim (Y/N) and excess, driver's share
- Driver signed agreement to the deduction (Y/N)
- Payment: in full or payment plan (instalments, amount per pay period, first deduction pay period, anything already paid back before this log)
- Dispute: disputed (Y/N), who disputed it, date raised, status (open / won / lost), outcome date and notes

## How it works things out

- **Cost to the business** = the total charged, or the insurance excess if it's going through insurance (whichever is lower). The insurer pays the rest.
- **Absorbed by the business** = cost to the business − driver's share.
- **Deductions:** one per 4-week pay period, from the first deduction period, for the full share or the plan amount, until the balance is cleared. A deduction counts as **paid** once its pay period has ended. **Balance** = driver's share − paid so far.
- **Open dispute:** deductions pause for any pay period where the dispute is still open on its last day. Remaining instalments move to later periods. A lost dispute resumes them.
- **Won dispute:** deductions stop. If we disputed it with DPD / the third party, the charge is cancelled (nothing absorbed). If the driver disputed their share, the business covers it. Anything already taken from the driver is refunded in the pay period of the outcome date.
- **Status:** a claim closes when its balance hits £0 (and no dispute is open), or when a dispute is won.
- **Flag:** any claim with a driver's share but no signed agreement shows *Not signed* everywhere it appears.

## Views

- **Dashboard:** open / all / closed, filtered to everything, a depot, an FD, a driver, a van or a claim type. Totals for outstanding balances, money absorbed by the business, total charged, paid back, due this pay period, unsigned claims, open disputes and refunds owed. Tables by driver, by van, by FD (with email), by depot and by type, plus a *Needs attention* list.
- **Log a claim:** the form, with a live breakdown and the full deduction schedule as you type.
- **Pay period deductions:** per driver for any 4-week pay period: deductions, refunds, paused claims, net off wages and what's still owed, every claim line behind them, and a pay-period-by-pay-period table.
- **All claims:** every claim with search, filters, edit, delete, CSV download and a detail view with its deduction schedule.

## Feeding the Driver Pay Log and the P&L

On *Pay period deductions*:

- **Download for Driver Pay Log:** one line per claim deducted that pay period, dated the last day of the period. Fines/PCNs are type *Parking ticket*; van, parcel and third-party claims are *Van damage* (the note says which, with the DPD ref, instalment number and what's left). Refunds after a won dispute are *Top up*. FD, email and depot are included too.
- **Download for P&L:** the cost absorbed by the business on every claim with an incident in that pay period, by FD, email and depot, for the *Van damages* box on the P&L's daily entry.
- **Copy summary:** a short per-driver text summary for the pay period.
