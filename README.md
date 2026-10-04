# Robust Statistics -- Automated Anomaly Detection

## Objective
I wanted to see how much extreme values distort common summary statistics, and how two different outlier-detection methods, Tukey Fences and Isolation Forest, agree or disagree on the same housing data.

## Methodology
- I loaded the California Housing dataset (20,640 observations) and computed six summary measures on the price variable: mean, median, trimmed mean, standard deviation, IQR, and MAD
- I implemented Tukey Fences by hand (Q1 - 1.5*IQR and Q3 + 1.5*IQR) to flag price outliers
- I applied scikit-learn's Isolation Forest to all eight features at once to catch anomalies that span multiple variables, not just price
- I compared the two methods' flags directly and looked at which rows each one caught that the other missed
- I ran a contamination experiment, replacing 5% of prices with extreme fake values, to see which statistics held up and which ones broke

## Key Findings
- The mean shifted by 67.1% after I corrupted 5% of the data, while the median only shifted by 3.6%, showing how much a small number of extreme values can distort the mean specifically
- Tukey Fences and Isolation Forest flagged mostly different rows: Tukey caught houses with extreme prices, while Isolation Forest caught unusual combinations of features, like ordinary prices paired with extreme occupancy or population numbers
- Many of the price outliers sat at the exact same value ($500,001), which points to a Census Bureau reporting cap rather than genuinely extreme individual prices
- Looking only at summary statistics for price would have missed the multi-feature anomalies entirely; plotting and multi-feature methods caught patterns a single number never could
