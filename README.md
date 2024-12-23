
# Context

The United States, European Union, Russia, and more recently China, have dominated the arms production sector. 

Using the Stockholm International Peace Research Institute (SIPRI) database, **this project analyzes key metrics of the global arms trade between 1994 and 2019**, with historical data for context. I also investigate how the leading global arms suppliers leverage exports as a tool of foreign policy.

Additionally, **I propose a standardized metric of the dispute for market dominance** through the trade of conventional weapons. The Normalized Relevance Score (NRS) measures competition balance in context of the number of players and the relative scale of trade. It is applicable to most market competition analysis where the market share per region is available.

# The data

The Stockholm International Peace Research Institute (SIPRI) database is the most comprehensive resource for analyzing  imports and exports of conventional weapons. It is maintained by an independent institute dedicated to the study of international conflicts, armaments, arms control and disarmament policies.

**The key metric in the Arms Transfers database is the Total Indicator Value (TIV)**. It overcomes challenges imposed by currency and market value of assets by assigning a standardized value to military equipment based on its type, capability and estimated production cost. Thus, it is not a direct representation of financial value but instead a measure of military capability.

<details>

<summary>Tips for collapsed sections</summary>

### You can add a header

```r
f <- read.csv("trade.csv", skip = 11)
trade <- as_tibble(f)

f2 <- read.csv("country_region.csv")
region_map <- as_tibble(f2)

trade <- janitor::clean_names(trade)

trade <- select(trade, order_date, supplier, recipient, numbers_delivered,
                armament_category, description, status, sipri_estimate,
                tiv_deal_unit, tiv_delivery_values)

# Shorten column names
trade <- trade |>
  rename(
    order_year = order_date,
    arm_cat = armament_category,
    tiv_unit = tiv_deal_unit,
    tiv_delivery = tiv_delivery_values,
    items = numbers_delivered
  )

# Factors
trade$supplier <- factor(trade$supplier, ordered = FALSE)
trade$recipient <- factor(trade$recipient, ordered = FALSE)
trade$arm_cat <- factor(trade$arm_cat, ordered = FALSE)

```

</details>
