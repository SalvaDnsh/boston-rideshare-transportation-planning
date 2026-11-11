# Reproducibility notes

## Inputs and notebook selection

The course and the Kaggle release share the same record count. The public release contains additional columns. Phase 1 explicitly selects the 39 course columns. Phase 2 reads only the fields used in the analysis.

The Phase 2 portfolio notebook uses the submitted version whose trip-distribution outputs match the report and whose revenue cell contains a completed solver run. The portfolio notebooks use a relative data path, omit saved cell outputs, and contain the original analysis steps. Phase 2 adds CSV exports. Phase 1 uses the current hourly pandas alias and identifies the Taguchi cell that fits XGBoost.

## Checking results

The Phase 2 tables were regenerated from the Kaggle CSV. The origin–destination matrix and weekday totals cover all 693,071 records. The reported stopping iterations and errors match the submitted results. Daily summaries use the CSV's raw distance units and retain fractional allocation volumes. Another CBC release may select different allocations when two or more options tie.

Phase 1 scores in the English report come from the submitted notebook. Several sampling and split steps do not set a seed. Full-data clustering and ensemble tuning can take considerable time, and output may vary across runs. scikit-learn is pinned to a release compatible with Yellowbrick 1.5.

## Outputs

| File | Definition |
| --- | --- |
| [Observed OD matrix](../results/observed-od-matrix.csv) | Record counts for each ordered origin–destination pair |
| [Weekday OD summary](../results/weekday-od-summary.csv) | Pooled record counts, nonzero pairs, mean positive cell count, and zone-balance check by weekday |
| [Convergence table](../results/trip-distribution-convergence.csv) | Iteration counts and aggregate marginal errors where that error was used |
| [Daily revenue](../results/daily-revenue.csv) | Allocated volume, distance used, gross modeled revenue, and CBC status for each weekday date |
| [Revenue allocation](../results/revenue-allocation.csv) | Positive allocations by date, zone pair, and six-hour slot |
