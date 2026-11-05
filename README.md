# Difference-in-Differences: Parallel Trends, Staggered Adoption and the Forbidden Comparison

## Objective
I wanted to see when difference-in-differences gives the right answer and when it quietly gives the wrong one.

## Methodology
- Downloaded Card and Krueger's (1994) New Jersey and Pennsylvania fast-food data from David Card's archive and computed the two-by-two DiD by hand from the four group means.
- Ran a DiD on a simulated panel where the true effect was zero but the treated and control groups were on different trends, then plotted the group means and ran a pre-trend test.
- Ran two-way fixed effects on a staggered-adoption panel with two cohorts and no never-treated units, and split it into its two two-by-two comparisons and their weights.
- Compared TWFE with an estimator that only uses not-yet-treated units as controls.
- Compared iid standard errors with standard errors clustered by state and period and by state, on a panel where every unit in a state shares a shock that carries over between periods.
- Used a module, did_utils.py, that never uses an already-treated unit as a control, and tested it against the earlier results.
- Asked an AI to write a Goodman-Bacon decomposition, checked it against my own numbers, found what my first prompt left it to guess, and revised the prompt once.

## Key Findings
- My Card and Krueger DiD came out to 2.75 full-time-equivalent employees, against their published +2.76.
- A significant DiD estimate can come entirely from groups being on different trends. The pre-trend test caught it here, but passing that test would not have proven parallel trends.
- TWFE returned -0.99 on a staggered panel where the true mean effect was 6.71. 0.667 of its weight sat on the comparison that uses already-treated units as controls.
- iid standard errors were 8.6 times too small when state shocks persisted from period to period.
- The AI's first decomposition did not match my numbers. After I revised the prompt, its weighted sum on the panel with missing outcomes was 2.6735, the same as the TWFE coefficient.
