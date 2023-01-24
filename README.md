# Most Recent Version
# Automated H, L and HV anchors. Displays the date of occurrence of swing H/L on daily timeframe

Release Notes: AVWAPS calculates on data matching chart timeframe using 'timeframe.period' . Consistencies with bar merge and lookahead resolved. labels fixed. datetime of LL and LH are reported on correct tf.

#Indicator Link (Tradingview)
[TF-Selective-AAVWAP](https://www.tradingview.com/script/iDFvwKve-TF-Selective-AAVWAP/)





# Custom-AAVWAP-Pinescript (V1)
Automated VWAP Indicator written in PineScript for TradingView charts. Anchored at key swing H/L levels extracted from price and volume time-series.

- Ensure that '//@version=5' is specified ontop of the indicator("...") call.

- Open TradingView's Pine Editor and create a new blank Indicator Script. Paste the Script into the Pine Editor and select the "Add To chart" option to display AAVWAP plots.

- Indicator takes one Argument, "Lookback (# of Periods)", and then for a given security finds three key anchors, the highest and lowest values in the 'hlc3' column (average of high low and close on the daily timeframe). The script displays up to three color coded timeseries corresponding to a trailing Volume Weighted Average Price beginning at the anchor dates corresponding to the anchor points listed above.

TradingView Indicator Link
- [Custom_AVWAP_Harpal's-Anchors](https://www.tradingview.com/script/WQlZvYUJ-Custom-AVWAP-Harpal-s-Anchors/)
