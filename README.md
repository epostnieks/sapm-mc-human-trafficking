# SAPM Monte Carlo — Human Trafficking / Demand Indestructibility

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Human Trafficking (Demand Indestructibility).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **22.62** |
| β_W mean | 22.86 |
| β_W std | 3.33 |
| **90% CI** | **[17.8, 28.7]** |
| 99% CI | [16.2, 31.7] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$5,338.1B/yr** |
| Π (revenue) | $236.0B/yr |

**β_W = 22.62** means the human trafficking industry destroys **$22.62 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-human-trafficking.git
cd sapm-mc-human-trafficking
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 22.62` and `ΔW median : $5,338.1B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_victim_welfare | $3,146.9B | [$2,357.7B, $4,195.5B] | Lognormal |
| C2_labor_market | $779.6B | [$552.4B, $1,102.8B] | Lognormal |
| C3_governance | $499.8B | [$312.6B, $799.5B] | Lognormal |
| C4_supply_chain | $420.3B | [$293.7B, $599.4B] | Lognormal |
| C5_intergenerational | $379.4B | [$262.9B, $548.5B] | Lognormal |
| C6_enforcement | $62.0B | [$42.0B, $82.0B] | Normal |
| **Total ΔW** | **$5,338.1B** | **[$4,207.1B, $6,781.2B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 5.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Human Trafficking (Demand Indestructibility)*.
> GitHub: epostnieks/sapm-mc-human-trafficking.
> https://github.com/epostnieks/sapm-mc-human-trafficking
