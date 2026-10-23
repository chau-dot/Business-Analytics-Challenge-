
# What Drives Airbnb Revenue in Melbourne?

**Evidence for a new multi-property host**

Chau Nguyen | Student ID 1553882
CMCE30005 Business Analytics Challenge | Semester 2, 2026 | University of Melbourne

## Overview

This project looks at what drives annual revenue for Airbnb listings in Melbourne and how a new host should position a property. It uses 25,293 short-stay listings from the Inside Airbnb snapshot of 16 June 2026. The full written report is submitted separately through the LMS, and this README summarises it.

**Business question:** which listing, host and location factors drive Airbnb revenue in Melbourne, and how should a new host set up a property to compete on more than price?

## Data

- **Source:** [Inside Airbnb](http://insideairbnb.com/get-the-data/), Melbourne listings file (25,728 listings, 90 variables), snapshot of 16 June 2026.
- **Cleaning:** 23 variables kept, 5 empty fields dropped, 435 long-stay listings (minimum stay of 30 nights or more, or none recorded) removed, leaving 25,293 listings.
- **Model sample:** 14,353 entire homes and private rooms with positive revenue, nights booked and price.
- **Note:** revenue and nights booked are Inside Airbnb estimates for the last 365 days, not confirmed bookings. The raw CSV files are not included in this repository (see "How to reproduce").

## Method

Multiple linear regression (OLS) on log annual revenue, with Superhost status, room type, guest capacity, amenity count, host tenure, minimum stay and local government area (LGA) as predictors. Because revenue = price x nights booked, the same model is also fitted to log price and log nights booked, so each effect splits exactly into a price part and a nights-booked part. The model is trained on a random 80/20 split (seed 123).

- Test-set fit (log scale): R-squared 0.42, RMSE 0.98, MAE 0.78
- Maximum variance inflation factor: 1.42
- Results held when the highest and lowest 1% of prices were removed

## Key findings

| Factor | Effect on annual revenue | Works through |
|---|---|---|
| Superhost-standard listing | +112% | Nights booked (+120%), not price |
| Entire home (vs private room) | +166% | Price (+80%) and nights (+48%) |
| 3-night minimum stay (vs 1 night) | -37% | Nights booked |
| Yarra (vs Melbourne CBD) | +23% | Price |
| Each extra amenity | +1.3% | Mostly nights booked |

Yarra is the only LGA clearly ahead of the CBD. 23 of the 27 location comparisons are clearly below it, and the outer suburbs are lowest.

(The README in the zip also embeds two figures here: `fig5_decomposition.png` and `fig4_lga_effects.png`.)

## Recommendations

1. **Acquire entire homes** rather than private rooms.
2. **Look beyond the CBD, towards Yarra.** The CBD holds 32.6% of listings but is not the most profitable market.
3. **Set 1 to 2 night minimum stays.**
4. **Operate to Superhost standard and equip the property fully.**

## Limitations

Revenue and nights are estimates from one snapshot, so seasonality is not covered. Results are associations, not causes. There is no cost data, so profit cannot be compared. R-squared is 0.42, so the model shows which factors matter better than it predicts a single listing.

## Repository structure

```
.
├── README.md
├── scripts/
│   ├── 01_cleaning.R        # raw listings file -> analysis set (25,293 rows)
│   └── 02_model.R           # model sample, three regressions, diagnostics, results table
├── model_full_results.csv   # full regression table (created by 02_model.R)
└── figures/                 # charts used in the report
```

## How to reproduce

1. Download the Melbourne listings file from Inside Airbnb (snapshot of 16 June 2026) and save it as `listings_airbnb.csv` in your R working directory.
2. In R, install the packages: `tidyverse`, `janitor`, `geosphere`, `car`.
3. Run `scripts/01_cleaning.R`, then `scripts/02_model.R`, in the same R session.
4. Check that the model uses 14,353 rows and that `model_full_results.csv` is created.

Developed in R 4.6.0.

## AI use

I used Claude (Anthropic) as an assistant to help plan the analysis, fix R code errors, and draft and edit the report text. I ran all the analysis in R, and the numbers in the report come from my R output. Figures 1 to 5 in the report were drawn from those values, and I can explain every result.

## References

- Gunter, U. (2018). What makes an Airbnb host a Superhost? Empirical evidence from San Francisco and the Bay Area. *Tourism Management, 66*, 26-37.
- Inside Airbnb. (2026). *Get the data: Melbourne, Victoria, Australia* [Listings dataset, snapshot of 16 June 2026]. http://insideairbnb.com/get-the-data/
- Liang, S., Schuckert, M., Law, R., & Chen, C. (2017). Be a "Superhost": The importance of badge systems for peer-to-peer rental accommodations. *Tourism Management, 60*, 454-465. https://doi.org/10.1016/j.tourman.2017.01.007
- R Core Team. (2026). *R: A language and environment for statistical computing* (Version 4.6.0). R Foundation for Statistical Computing. https://www.R-project.org/
- Wang, D., & Nicolau, J. L. (2017). Price determinants of sharing economy based accommodation rental: A study of listings from 33 cities on Airbnb.com. *International Journal of Hospitality Management, 62*, 120-131. https://doi.org/10.1016/j.ijhm.2016.12.007
- Wickham, H., et al. (2019). Welcome to the tidyverse. *Journal of Open Source Software, 4*(43), 1686. https://doi.org/10.21105/joss.01686
