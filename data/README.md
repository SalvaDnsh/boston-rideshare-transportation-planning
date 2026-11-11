# Boston rideshare data

Download [Uber and Lyft Dataset Boston, MA](https://www.kaggle.com/datasets/brllrb/uber-and-lyft-dataset-boston-ma) by BM on Kaggle. Extract `rideshare_kaggle.csv` into this directory. Both notebooks also accept the 39-column version used in the course.

The public CSV has 693,071 records and 57 columns. Its documentation dates the sample from November 26 to December 18, 2018. Phase 1 selects the 39 columns listed in the submitted notebook and retains the 637,976 records with observed prices for fare analysis. Phase 2 reads the eight columns below. It uses all records for the origin–destination counts and observed prices for the fare summaries.

| Column | Role in Phase 2 |
| --- | --- |
| `source`, `destination` | Ordered pair of Boston zones |
| `month`, `day`, `hour` | Calendar weekday, date, and six-hour slot |
| `cab_type` | Uber or Lyft, used to calculate company-specific mean fares |
| `price` | Observed fare, used as a cost proxy and for revenue coefficients |
| `distance` | Recorded distance, used in the revenue model in the CSV's native units |

The records represent observations in the dataset. The project counts records as a proxy for demand. Completed trip volumes and population-level demand would require separate evidence.

SHA-256 of the Kaggle CSV used for the portfolio rerun

```text
829f2ae6d6fc7806cad37622061ded01032387a2760b21b1cf50560926909ab7
```
