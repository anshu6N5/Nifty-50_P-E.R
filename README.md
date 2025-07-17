# Nifty-50_P-E.R

This project uses R to estimate whether the **Nifty 50 index** is **overvalued, undervalued, or fairly valued** as of a specific date—**July 15, 2025**—based on its **price-to-earnings (P/E) ratio**.

## 🔍 Objective

To analyze Nifty 50's valuation by:
- Fetching live/historical price data using `quantmod` from Yahoo Finance
- Estimating the index’s P/E ratio using an assumed EPS value
- Comparing it with the historical average P/E of Nifty
- Visualizing the comparison using `ggplot2`

## 📦 Packages Used

- `quantmod` – for fetching stock market data
- `ggplot2` – for visualization
- `dplyr` – for data manipulation (optional)

- ## 🧠 Assumptions

- **EPS estimate** for Nifty 50 (as of July 15, 2025): `1114.86`
- **Historical average P/E** considered for comparison: 22

- ## 💻 How It Works

```r
# Step 1: Load Libraries
library(quantmod)
library(ggplot2)

# Step 2: Get Nifty 50 Price on 15 July 2025
getSymbols("^NSEI", src = "yahoo", from = "2025-07-15", auto.assign = TRUE)
nifty <- Cl(NSEI)
price <- as.numeric(nifty["2025-07-15"])

# Step 3: Estimate P/E Ratio
eps <- 1111.128319
pe_ratio <- price / eps

# Step 4: Compare with Historical P/E
historical_avg <- 20

# Step 5: Prepare Data Frame
pe_on_date <- as.numeric(last(pe_ratio))
pe_df <- data.frame(
  Type = c("Estimated P/E (15-Jul-2025)", "Historical Avg P/E"),
  PE = c(pe_ratio, historical_avg)
)

ggplot(pe_df, aes(x = Type, y = PE)) +
  geom_bar(stat = "identity", width = 0.6, fill = c("salmon", "navyblue")) +
  geom_text(aes(label = round(PE, 2)), vjust = -0.5, size = 3.5) +
  labs(
    title = "Nifty 50 P/E Comparison",
    subtitle = "Current P/E vs Historical P/E (as on 15/07/2025)",
    x = "Type",
    y = "P/E Ratio"
  ) +
  theme_minimal(base_size = 14)

## Author
 Anshu kumar
