`java
//@version=5
indicator('Armaan-Harpal-Custom-AAVWAP', overlay=true, max_bars_back=5000)
//@ak2k2, Credit to @AJ7919 for Open Source Contribution

tframe = '1D'
display_extra_labels = input(defval = false)
period = input(defval=100, title='Look Back Period (# of Days)')

display_as_hline = false
label_offset = 50
show_low_vwap_label = true
show_high_vwap_label = true
show_vol_vwap_label = true

// Var declaration
var int block_size = 1
var currentBarTime = 0


time_0 = request.security(syminfo.tickerid, tframe, time, barmerge.gaps_off, barmerge.lookahead_on)
time_1 = request.security(syminfo.tickerid, tframe, time[period], barmerge.gaps_off, barmerge.lookahead_on)

var TPeriod = 0
var chart_timeframe_minutes = 0
var indicator_timeframe_minutes = 0
var real_period = 0

// low vwap vars
var low_vwap_volume_price_summation = 0.0
var low_vwap_volume_summation = 0.0
var low_vwap_counter = 1
var float low_vwap = na
var float lowest_vwap = na
var low_vwap_color = color.fuchsia
var string low_vwap_text = na

// high vwap vars
var high_vwap_volume_price_summation = 0.0
var high_vwap_volume_summation = 0.0
var high_vwap_counter = 1
var float high_vwap = na
var float highest_vwap = na
var high_vwap_color = color.blue
var string high_vwap_text = na

// volume vwap vars
var vol_vwap_volume_price_summation = 0.0
var vol_vwap_volume_summation = 0.0
var vol_vwap_counter = 1
var float vol_vwap = na
var float volest_vwap = na
var vol_vwap_color = color.orange
var string vol_vwap_text = na


var float delta = na


if not na(time[period])
    delta := time_0 - time_1

    for int i = 1 to 4999 by 1
        if time - time[i] > delta
            block_size := i
            break

DAYVOL = request.security(syminfo.tickerid, timeframe.period, volume, barmerge.gaps_off, barmerge.lookahead_on)
DAYHIGH = request.security(syminfo.tickerid, timeframe.period, high, barmerge.gaps_off, barmerge.lookahead_on)
DAYLOW = request.security(syminfo.tickerid, timeframe.period, low, barmerge.gaps_off, barmerge.lookahead_on)
DAYHLC = request.security(syminfo.tickerid, timeframe.period, hlc3, barmerge.gaps_off, barmerge.lookahead_on)

if timenow - time < delta
    if low_vwap_counter == 1
        lowest_vwap := DAYLOW
        low_vwap_volume_price_summation := DAYVOL * DAYHLC
        low_vwap_volume_summation := DAYVOL
        low_vwap := low_vwap_volume_price_summation / low_vwap_volume_summation
        low_vwap_counter += 1
        low_vwap_counter
    else
        if lowest_vwap > DAYLOW
            low_vwap_color := low_vwap_color == color.fuchsia ? color.fuchsia : color.fuchsia
            low_vwap_volume_price_summation := DAYVOL * DAYHLC
            low_vwap_volume_summation := DAYVOL
            low_vwap := low_vwap_volume_price_summation / low_vwap_volume_summation
            lowest_vwap := DAYLOW
            lowest_vwap
        else
            low_vwap_volume_price_summation += DAYVOL * DAYHLC
            low_vwap_volume_summation += DAYVOL
            low_vwap := low_vwap_volume_price_summation / low_vwap_volume_summation
            low_vwap

        low_vwap_counter += 1
        low_vwap_counter


if timenow - time < delta
    if high_vwap_counter == 1
        highest_vwap := DAYHIGH
        high_vwap_volume_price_summation := DAYVOL * DAYHLC
        high_vwap_volume_summation := DAYVOL
        high_vwap := high_vwap_volume_price_summation / high_vwap_volume_summation
        high_vwap_counter += 1
        high_vwap_counter
    else
        if highest_vwap < DAYHIGH
            high_vwap_color := high_vwap_color == color.blue ? color.blue : color.blue
            high_vwap_volume_price_summation := DAYVOL * DAYHLC
            high_vwap_volume_summation := DAYVOL
            high_vwap := high_vwap_volume_price_summation / high_vwap_volume_summation
            highest_vwap := DAYHIGH
            highest_vwap
        else
            high_vwap_volume_price_summation += DAYVOL * DAYHLC
            high_vwap_volume_summation += DAYVOL
            high_vwap := high_vwap_volume_price_summation / high_vwap_volume_summation
            high_vwap

        high_vwap_counter += 1
        high_vwap_counter


if timenow - time < delta
    if vol_vwap_counter == 1
        volest_vwap := DAYVOL
        vol_vwap_volume_price_summation := DAYVOL * DAYHLC
        vol_vwap_volume_summation := DAYVOL
        vol_vwap := vol_vwap_volume_price_summation / vol_vwap_volume_summation
        vol_vwap_counter := high_vwap_counter + 1
        vol_vwap_counter
    else
        if volest_vwap < DAYVOL
            vol_vwap_color := vol_vwap_color == color.orange ? color.orange : color.orange
            vol_vwap_volume_price_summation := DAYVOL * DAYHLC
            vol_vwap_volume_summation := DAYVOL
            vol_vwap := vol_vwap_volume_price_summation / vol_vwap_volume_summation
            volest_vwap := DAYVOL
            volest_vwap
        else
            vol_vwap_volume_price_summation += DAYVOL * DAYHLC
            vol_vwap_volume_summation += DAYVOL
            vol_vwap := vol_vwap_volume_price_summation / vol_vwap_volume_summation
            vol_vwap

        vol_vwap_counter += 1
        vol_vwap_counter


TPeriod := time - time[1]
TPeriod := na(TPeriod) ? 0 : TPeriod

// if barstate.islast

pa = request.security(syminfo.tickerid, '1D', hlc3)
tim = request.security(syminfo.tickerid, '1D', time)

hi = ta.highest(pa, period)
hiOffset = -ta.highestbars(hlc3, period)
ath_dt = time[hiOffset]
ath_time = str.tostring(year(ath_dt)) + '-' + str.tostring(month(ath_dt)) + '-' + str.tostring(dayofmonth(ath_dt))

lo = ta.lowest(low, period)
loOffset = -ta.lowestbars(hlc3, period)
atl_dt = time[loOffset]
atl_time = str.tostring(year(atl_dt)) + '-' + str.tostring(month(atl_dt)) + '-' + str.tostring(dayofmonth(atl_dt))

// line.new(bar_index[hiOffset], low - (atr(100) * 100), bar_index[hiOffset], high + (atr(100) * 100), color=color.new(color.blue, 50), width=3)
// line.new(bar_index[loOffset], low + (atr(10) * 100), bar_index[loOffset], low - (atr(10) * 100), color=color.new(color.fuchsia, 50), width=3)
// line.new(bar_index[hiOffset], low - (atr(100) * 10), bar_index[hiOffset], high + (atr(100) * 10), color=color.new(color.blue, 50), width=3)

// Labels Initialization

if display_extra_labels and timeframe.period == 'D'
    if barstate.islast
        label.new(bar_index + 150, high + 50, 'Highest Daily hlc3: ' + str.tostring(hi) + ' Occured at: ' + str.tostring(ath_time), style=label.style_label_center)
        label.new(bar_index + 150, low - 50, 'Lowest Daily hlc3: ' + str.tostring(lo) + ' Occured at: ' + str.tostring(atl_time), style=label.style_label_center)



if tframe == '1D'
    low_vwap_text := 'LP'
    high_vwap_text := 'HP'
    vol_vwap_text := 'HV'
    vol_vwap_text


// var low_vwap_label = label.new(na, na, low_vwap_text, xloc.bar_index, size = size.tiny)
// var high_vwap_label = label.new(na, na, high_vwap_text, xloc.bar_index, size = size.tiny)
// var vol_vwap_label = label.new(na, na, vol_vwap_text, xloc.bar_index, size = size.tiny)

// if show_low_vwap_label
//     label.set_xloc(low_vwap_label, time + label_offset * TPeriod, xloc.bar_time)
//     label.set_y(low_vwap_label, low_vwap)
//     label.set_style(low_vwap_label, label.style_label_left)
//     label.set_color(low_vwap_label, low_vwap_color)
// else
//     label.delete(low_vwap_label)

// if show_high_vwap_label
//     label.set_xloc(high_vwap_label, time + label_offset * TPeriod, xloc.bar_time)
//     label.set_y(high_vwap_label, high_vwap)
//     label.set_style(high_vwap_label, label.style_label_left)
//     label.set_color(high_vwap_label, high_vwap_color)
// else
//     label.delete(high_vwap_label)

// if show_vol_vwap_label
//     label.set_xloc(vol_vwap_label, time + label_offset * TPeriod, xloc.bar_time)
//     label.set_y(vol_vwap_label, vol_vwap)
//     label.set_style(vol_vwap_label, label.style_label_left)
//     label.set_color(vol_vwap_label, vol_vwap_color)
// else
//     label.delete(vol_vwap_label)


plot(high_vwap, title='AVWAP Highest hlc3', color=color.new(high_vwap_color, 0), trackprice=display_as_hline, style=plot.style_line)
plot(low_vwap, title='AVWAP: Lowest hlc3', color=color.new(low_vwap_color, 0), trackprice=display_as_hline, style=plot.style_line)
plot(vol_vwap, title='AVWAP: Highest Volume', color=color.new(vol_vwap_color, 0), trackprice=display_as_hline, style=plot.style_line)
`
