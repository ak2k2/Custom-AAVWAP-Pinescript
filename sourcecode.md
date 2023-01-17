```pinescript
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ak2k2

//@version=5
indicator("Custom_AAVWAP", overlay=true,max_labels_count = 500,max_lines_count = 500, max_bars_back = 2000)
lb = input.int(100,"Lookback (# of Periods)",1, 1000,1)

len = lb
src = hlc3

hi = ta.highest(src,len)
hiOffset = - ta.highestbars(src,len)

lo = ta.lowest(src,len)
loOffset = - ta.lowestbars(src,len)

src_vol = volume
hv = ta.highest(src_vol, len)
hvOffset = -ta.highestbars(src_vol, len)

f_avwap(src, date, plotcolor) =>
    float[]    array_sumSrc = array.new_float( date,na)
    float[]    array_sumVol = array.new_float( date,na)
    // float[]    array_final = array.new_float( date,na)
    if date>0 and array.size(array_sumSrc)>0
        for i=date-1 to 0
            sumSrc = src[i] * volume[i]
            sumVol = volume[i]
            array.set(array_sumSrc,i,sumSrc + sumSrc[1+i])
            array.set(array_sumVol,i,sumVol + sumVol[1+i])
            finalVal=array.sum(array_sumSrc) / array.sum(array_sumVol)
            if barstate.islast
                line.new(bar_index[i+1],finalVal,bar_index[i],finalVal,color=plotcolor)        

ath_dt = bar_index-bar_index[hiOffset]
atl_dt = bar_index-bar_index[loOffset]
athv_dt = bar_index-bar_index[hvOffset]

fh=f_avwap(src, ath_dt, color.red)
fl = f_avwap(src,atl_dt, color.green)
fhv = f_avwap(src,athv_dt, color.aqua)


```
