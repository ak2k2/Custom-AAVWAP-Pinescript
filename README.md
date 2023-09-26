# TF-Selective-AAVWAP (V2)
## Author: Armaan Kapoor
## Written in PineScript for TradingView charts

![vwap-ak](https://github.com/ak2k2/Custom-AAVWAP-Pinescript/assets/103453421/bdb0eaf8-19be-4dcd-b1d6-4b5a12122c68)


TF-Selective-AAVWAP (V2) generates three distinct VWAP time series, anchored at swing-low, swing-high, and swing-high-volume candle indices within a given lookback period. 

It considers three distinct anchoring points: swing-low, swing-high, and swing-high-volume candle indices. 1. **Swing-low** (`SL`): The index 
 such that 
 is the minimum price within a given lookback period ending at index 
. That is:
where `argmin` returns the index at which 
 is minimized. 2. **Swing-high** (`SH`): The index 
 such that 
 is the maximum price within a given lookback period ending at index 
. That is:
where `argmax` returns the index at which 
 is maximized. 3. **Swing-high-volume** (`SHV`): The index 
 such that 
 is the maximum volume within a given lookback period ending at index 
. This point represents the candle with the highest traded volume:
For each of these indices, you can compute a VWAP anchored at that specific index. The VWAP formula remains the same as before, but you start the summation from the swing index rather than from the beginning: \[ VWAP_{SL}(i) = \frac{\sum_{j=SL(i)}^{i} P(j) \times V(j)}{\sum_{$

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


