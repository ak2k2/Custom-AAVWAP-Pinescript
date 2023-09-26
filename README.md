# TF-Selective-AAVWAP (V2)
## Author: Armaan Kapoor
## Written in PineScript for TradingView charts

![vwap-ak](https://github.com/ak2k2/Custom-AAVWAP-Pinescript/assets/103453421/d248c283-0d88-44ca-b2c8-2f95a9387c27)


TF-Selective-AAVWAP (V2) generates three distinct VWAP time-series, anchored at swing low, swing high, and swing high volume indices in a given range. 


## TradingView Release (V2) - [TF-Selective-AAVWAP](https://www.tradingview.com/script/iDFvwKve-TF-Selective-AAVWAP/)

Release Notes: 
1. AVWAPS calculates on data matching chart timeframe using 'timeframe.period'. 
2. Consistent use of bar merge and lookahead. Labels fixed. Datetime of LL and LH are reported on the correct timeframe. 
3. Automated H, L and HV anchors. Displays the date of occurrence of swing H/L on daily timeframe.


# OLD Release (V1)
## TradingView Hyperlink - [Custom_AVWAP_Harpal's-Anchors](https://www.tradingview.com/script/WQlZvYUJ-Custom-AVWAP-Harpal-s-Anchors/)

Automated VWAP Indicator written in PineScript for TradingView charts. Anchored at key swing H/L levels extracted from price and volume time-series.

1. Ensure that '//@version=5' is specified ontop of the indicator("...") call.

2. Open TradingView's Pine Editor and create a new blank Indicator Script. Paste the Script into the Pine Editor and select the "Add To chart" option to display AAVWAP plots.

3. Indicator takes one Argument, "Lookback (# of Periods)", and then for a given security finds three key anchors, the highest and lowest values in the 'hlc3' column (average of high low and close on the daily timeframe). The script displays up to three color coded timeseries corresponding to a trailing Volume Weighted Average Price beginning at the anchor dates corresponding to the anchor points listed above.


