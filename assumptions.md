# Monte Carlo Assumptions — Human Trafficking / Demand Indestructibility

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $236.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 22.62 | Confirmed by N=100,000 draws |
| ΔW median (result) | $5,338.1B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_victim_welfare` | lognormal | $2,400B | $3,150B | $4,200B | Direct victim welfare destruction (27.6M victims) |
| `C2_labor_market` | lognormal | $500B | $780B | $1,100B | Labor market distortion, wage depression |
| `C3_governance` | lognormal | $250B | $500B | $800B | Governance corrosion, corruption, state complicity |
| `C4_supply_chain` | lognormal | $250B | $420B | $600B | Consumer supply chain contamination |
| `C5_intergenerational` | lognormal | $250B | $380B | $550B | Intergenerational human capital destruction |
| `C6_enforcement` | normal | $45B | $62B | $85B | Enforcement resource diversion |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 5.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 5.0) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 22.42 | 20% DC adj = 17.94 | 40% DC adj = 13.45

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $5,338B = 5.0% of world GDP ($106T) ✓
- **β_W range**: 22.62 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
