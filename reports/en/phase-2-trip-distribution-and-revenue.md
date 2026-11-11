# Phase 2 — Trip distribution and revenue optimization

[Notebook](../../notebooks/phase-2-trip-distribution-and-revenue.ipynb) · [Persian course report](../original/phase-2-course-report-fa.pdf) · [Results](../../results)

## Observed origin–destination matrices

The analysis counts raw rideshare records by ordered origin and destination across 12 Boston zones. It also builds one matrix for each weekday by pooling the dates observed for that weekday. The overall matrix was asymmetric. Neither the overall matrix nor any weekday matrix had identical incoming and outgoing counts in every zone.

Tuesday and Monday had the highest pooled mean counts per nonzero origin–destination pair, while Wednesday had the lowest. These means depend on how many dates for each weekday occur in the sample. See the [observed matrix](../../results/observed-od-matrix.csv) and [weekday summary](../../results/weekday-od-summary.csv).

## Future trip distribution

The assignment provided future departures and arrivals by zone. The notebook rescales the arrival targets to the departure total and estimates a future origin–destination matrix under five specifications. Furness, Detroit, and Fratar use the observed matrix as their starting point. The gravity models use mean observed fare by zone pair as the impedance proxy. Missing-fare pairs and the diagonal receive zero weight.

| Method | Iterations to stopping criterion | Aggregate marginal error |
| --- | ---: | ---: |
| Furness | 1 | 0.3360% |
| Detroit | 1 | Uses a growth-factor range |
| Fratar | 1 | 0.3360% |
| Exponential gravity | 3 | 0.3586% |
| Power gravity | 2 | 0.3360% |

The aggregate error is the sum of absolute differences between modeled and target departure and arrival totals, divided by total target departures. The reported Detroit implementation checks whether row and column growth factors lie between 0.99 and 1.01. The table compares how soon each method reached its own stopping rule. Independent future observations would be needed to compare forecast accuracy.

## Daily revenue model

The market-entry exercise allocates continuous service volumes to observed origin–destination pairs in four six-hour slots per date. The code solves one linear program per observed weekday date and excludes Saturdays and Sundays. The upper bound for each decision is the observed record count for its date, zone pair, and slot.

For each date, the model maximizes the sum of allocation volume multiplied by its estimated fare per trip. The fare coefficient is the mean company-level fare per unit of distance multiplied by the mean distance of the zone pair. The only shared capacity constraint is the sum of allocated volumes multiplied by their mean distances, capped at 20 per day. The original notebook applies the cap directly to the dataset's distance column. The exports therefore label distance in native CSV units. The objective measures gross modeled revenue and the continuous decisions can produce fractional service volumes.

CBC returned an optimal solution for all 12 modeled weekday dates. [Daily solver summaries](../../results/daily-revenue.csv) and the [selected allocations](../../results/revenue-allocation.csv) are available as CSVs. The model has no operating-cost, vehicle-routing, or repositioning terms.
