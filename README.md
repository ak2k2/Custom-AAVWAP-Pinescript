# TF-Selective-AAVWAP (V2)
## Author: Armaan Kapoor
## Written in PineScript for TradingView charts

![vwap-ak](https://github.com/ak2k2/Custom-AAVWAP-Pinescript/assets/103453421/bdb0eaf8-19be-4dcd-b1d6-4b5a12122c68)


TF-Selective-AAVWAP (V2) generates three distinct VWAP time series, anchored at swing-low, swing-high, and swing-high-volume candle indices within a given lookback period. 
# TF-Selective-AAVWAP (V2) Calculation

The **TF-Selective-AAVWAP (V2)** method provides an enhanced VWAP approach, generating three distinct VWAP time series based on different anchoring points within a given lookback period: swing-low, swing-high, and swing-high-volume candle indices.

![sxpng](https://github.com/ak2k2/Custom-AAVWAP-Pinescript/assets/103453421/b77d961c-4577-4812-89d3-9f639dab309e)


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


