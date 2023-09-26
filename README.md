# TF-Selective-AAVWAP (V2)
## Author: Armaan Kapoor
## Written in PineScript for TradingView charts

![vwap-ak](https://github.com/ak2k2/Custom-AAVWAP-Pinescript/assets/103453421/bdb0eaf8-19be-4dcd-b1d6-4b5a12122c68)


TF-Selective-AAVWAP (V2) generates three distinct VWAP time series, anchored at swing-low, swing-high, and swing-high-volume candle indices within a given lookback period. 
# TF-Selective-AAVWAP (V2) Calculation

The **TF-Selective-AAVWAP (V2)** method provides an enhanced VWAP approach, generating three distinct VWAP time series based on different anchoring points within a given lookback period: swing-low, swing-high, and swing-high-volume candle indices.


1. **Swing-low (`SL`)**: For a given index \( i \), the swing-low is defined as the index \( k \) where \( P(k) \) represents the minimum price within the lookback period:
\[ SL(i) = \text{argmin}_{k \leq i} P(k) \]
Here, `argmin` returns the index at which \( P(k) \) is minimized.

2. **Swing-high (`SH`)**: For a given index \( i \), the swing-high is defined as the index \( l \) where \( P(l) \) represents the maximum price within the lookback period:
\[ SH(i) = \text{argmax}_{l \leq i} P(l) \]
Here, `argmax` returns the index at which \( P(l) \) is maximized.

3. **Swing-high-volume (`SHV`)**: For a given index \( i \), this represents the index \( m \) where \( V(m) \) is the maximum volume within the lookback period:
\[ SHV(i) = \text{argmax}_{m \leq i} V(m) \]

## VWAP Formulas

For each of the above-defined indices, the VWAP is calculated starting from the specific swing index:

- **VWAP anchored at Swing-low**:
\[ VWAP_{SL}(i) = \frac{\sum_{j=SL(i)}^{i} P(j) \times V(j)}{\sum_{j=SL(i)}^{i} V(j)} \]

etc.

## TradingView Release (V2) - [TF-Selective-AAVWAP](https://www.tradingview.com/script/iDFvwKve-TF-Selective-AAVWAP/)

Release Notes: 
1. Data matches chart timeframe using 'timeframe.period'. 
2. Consistent use of bar merge and lookahead. Labels fixed. Datetime of LL and LH are reported on the correct timeframe. 
3. Automated H, L and HV anchors. Displays the date of occurrence of swing H/L on daily timeframe.


# OLD Release (V1)
## TradingView Hyperlink - [Custom_AVWAP_Harpal's-Anchors](https://www.tradingview.com/script/WQlZvYUJ-Custom-AVWAP-Harpal-s-Anchors/)

Automated VWAP Indicator written in PineScript for TradingView charts. Anchored at key swing H/L levels extracted from price and volume time-series.

1. Ensure that '//@version=5' is specified ontop of the indicator("...") call.

2. Open TradingView's Pine Editor and create a new blank Indicator Script. Paste the Script into the Pine Editor and select the "Add To chart" option to display AAVWAP plots.


