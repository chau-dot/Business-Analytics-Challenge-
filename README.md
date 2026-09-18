# CMCE30005 Business Analytics Challenge
## AirBnb Melbourne

**Subject:** CMCE30005 Business Analytics Challenge, Semester 2 2026
**University:** University of Melbourne
**Team Members:** Chau Nguyen 1553882
**GitHub Link** https://github.com/chau-dot/Business-Analytics-Challenge-

---

## Business Problem

Our client is preparing to invest in and list multiple Airbnb properties across 
Melbourne but currently has no data driven basis for deciding which properties, 
locations, or hosting practices are likely to perform well. This project 
investigates what listing, host, and location factors drive Airbnb revenue and 
occupancy performance in Melbourne, and how a new host should position their 
property to compete on more than price. This matters because early exploration 
revealed that Superhosts earn substantially more revenue than non Superhosts 
despite charging near identical nightly prices, indicating that price alone 
cannot explain performance in this market, a costly assumption for a client 
about to commit capital to specific properties. The project uses linear 
regression, supported by descriptive and exploratory analysis, to identify 
which factors most strongly predict revenue and translate these findings into 
practical, evidence based recommendations for the client.

---

## Dataset

**Dataset name:** Airbnb Melbourne - June 2026 Snapshot
**Source:** Inside Airbnb - http://insideairbnb.com/
**Coverage:** All active Airbnb listings in Melbourne as of 16 June 2026

### Data Files

| File | Description | Size |
|------|-------------|------|
| `listings_all.csv` | Full listing details (~75 variables) | ~50 MB |
| `reviews_all.csv` | Guest review text | ~200 MB |
| `calendar_all.csv` | Daily availability and pricing | ~1 GB |

---

## Introduction

AirBnb has become a significant channel for short-term accommodation in 
Melbourne, and prospective hosts increasingly rely on data to decide where and 
how to list a property. This project investigates what drives revenue and
occupancy performance for Airbnb listings in Melbourne, using data from Inside 
AirBnb, an independent platform publishing public AirBnb listings data. The
dataset was selected because it provides both listing-level detail and
platform-estimated performance measures, allowing performance to be examined 
directly rather than inferred.

The project is framed around a client who intends to list multiple properties 
in Melbourne and requires evidence-based guidance rather than assumption. Early
exploration revealed a striking pattern: Superhosts earn substantially more 
revenue than non-Superhosts despite charging near-identical prices, suggesting 
that price is not the primary driver of performance in this market. By the final
report, this project aims to identify which factors most strongly explain isting
performance and translate these findings into practical recommendations for a 
new host. 

## Problem Definition and Objectives

The business problem addressed is: what listings, host, and location factors 
drive AirBnb revenue and occupancy performance in Melbourne, and how should a 
new host position their property to complete on more than price? This matters 
because a client preparing to invest in multiple properties needs to understand 
what genuinely determines returns before committing capital, rather than relying 
on the common assumption that higher prices or better locations alone guarantee
success.

The project's scope is limited to entire home and private-room listings, given
that shared-room and hotel-room listings each represent under one percent of the 
market and are commercially marginal. The primary objective is to build a 
regression model explaining variation in estimated annual revenue, using host, 
property, location, and guest-experience variables as predictors. A central 
hypothesis under investigation is that Superhost status is associated with 
substantially higher revenue primarily through increased occupancy rather than 
through higher pricing, and that this relationship may be confounded by other 
factors such as amenity provision and room type.

##Data Description

The primary dataset is listings_airbnb.csv from Inside Airbnb, a snapshot of 
25,728 active Melbourne listings across 90 variables, collected 16 June 2026. 
Two supporting files, containing calendar availability and guest reviews, were 
also provided but have not yet been incorporated into the analysis.

Data cleaning began by retaining only variables relevant to the business 
problem, reducing the dataset to 22 columns covering host, property, location, 
pricing, and review characteristics. Price was converted from a currency-
formatted string to a numeric field. Five host-related variables, including 
response rate and license status, were entirely missing and were excluded. 
Listings requiring a minimum stay of 30 nights or more (n = 435) were removed 
after analysis showed a median price of $84.90 and a 78.5 percent zero-revenue 
rate for this group, indicating they function as long-term rentals rather than 
short-term Airbnb stays. The cleaned dataset comprises 25,293 listings.

Exploratory analysis identified several important patterns. Estimated revenue is
heavily right-skewed, with approximately 25 percent of listings showing zero 
revenue; this was found to align almost perfectly with listings having zero 
reviews, confirming these are genuinely inactive rather than erroneous records. 
Superhosts show a markedly higher median revenue than non-Superhosts ($23,400 
versus $2,928) despite comparable pricing, with the gap explained primarily by 
occupancy (median 96 nights versus 0). A correlation matrix confirmed occupancy 
as the strongest numeric correlate of revenue (r = 0.58), well ahead of price 
(r = 0.13).

## Methodology and Analytical Approach

This project will use linear regression as the primary analytical method, with 
estimated_revenue_l365d (log-transformed to address skew) as the target variable
and estimated_occupancy_l365d examined as a supporting variable. Regression was 
selected because the objective is to identify which factors influence revenue 
and by how much, rather than to produce a prediction alone; regression 
coefficients allow specific, explainable findings to be communicated to the 
client. Random forest regression will be considered as a comparison model to 
test whether non-linear relationships, such as the U-shaped association observed 
between revenue and distance from the CBD, improve on the linear approach.

Several assumptions and validation considerations have already emerged from 
exploratory analysis. A correlation of 0.84 between accommodates and bedrooms 
indicates multicollinearity; accommodates will be retained as the primary size 
variable. Individual amenities were found to be confounded with overall amenity 
count and Superhost status, so amenities_count will be used instead of specific 
amenity indicators. Distance to the CBD shows a non-linear relationship with 
revenue and will require a categorical or quadratic treatment rather than a raw 
linear term. Model validation will use a held-out test set, with RMSE, MAE, and 
R² as evaluation criteria. All analysis is conducted in R, using the tidyverse 
ecosystem for data manipulation and visualisation, selected for its suitability 
for statistical modelling and reproducible reporting.

## Analysis Plan and Progress to Date

To date, the dataset has been cleaned and reduced to relevant variables, and an 
extensive exploratory analysis has been completed. This included univariate and 
grouped summary statistics, correlation analysis, and visualisations across host 
characteristics, room type, location, review behaviour, amenities, and booking 
terms. Key findings include the Superhost revenue gap, a non-linear relationship 
between revenue and distance to the CBD, weak explanatory power of review scores 
relative to review volume, and confounding between amenity count and Superhost 
status.

Remaining tasks include finalising feature engineering, particularly encoding 
categorical variables and deriving a distance-based location feature, followed 
by fitting and comparing the linear regression and random forest models. 
Subsequent steps include model evaluation against the held-out test set and 
translating significant predictors into concrete recommendations for the client 
regarding location, property type, and hosting standards, to be presented in the 
final report.


*Last updated: 18/09/2026*
