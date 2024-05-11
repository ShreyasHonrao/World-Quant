# World-Quant

Strategy 1:<br/>
alpha= -ts_decay_exp_window((2*close-high-low)/(high-low)*volume,252);<br/>
b=ts_median(alpha,5);<br/>
c=(b/ts_mean(volume,42));<br/>
alp=trade_when(mcr38_adx_signal>25,c,mcr38_adx_signal<20);<br/>
x=group_neutralize(alp,pv13_r2_min2_3000_sector)<br/>


![close](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/499ad69b-acab-48d7-b7de-260c87db6662)<br/>


Strategy 2:<br/>
e=(ts_delay(implied_volatility_call_120,120)/ts_delay(implied_volatility_call_90,90));<br/>
alpha=ts_decay_exp_window(hump(implied_volatility_call_360-implied_volatility_put_360,hump=0.001),252);<br/>
trade_when(e<1.35,alpha,-rank(implied_volatility_put_120/implied_volatility_call_10))<br/>

![vol](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/8eb56e53-0b7c-4b69-af85-670f15656030)<br/>


Strategy 3:<br/>
a=-power(rank_by_side(oth466_rt_stk_split_ratio),2)+2*to_nan(power(rank_by_side(mdl130_qes_rcr),2),value=0,reverse=true);<br/>
b=group_neutralize(a,exchange);<br/>
c=b*(rank(-a)+1);<br/>
d=hump(c,hump=0.001);<br/>
signed_power(hump_decay(d*(1+.125*rank(-cap))),2)<br/>

<img width="723" alt="split_ratio" src="https://github.com/ShreyasHonrao/World-Quant/assets/108209291/d5084003-2887-4eeb-980f-0cbf9d6fd728"><br/>


Strategy 4:<br/>
a=group_neutralize(ts_scale((vwap-close)/(vwap+close),60)*ts_weighted_decay(ts_arg_min(news_mins_10_chg*(scale((volume))),60))*(vwap/close),market);<br/>
alpha  = trade_when(ts_std_dev(volume,15)<ts_std_dev(volume,120),a,-1);<br/>
quantile((returns>0.025 ? (1-returns)*alpha : alpha))<br/>

<img width="735" alt="vwap" src="https://github.com/ShreyasHonrao/World-Quant/assets/108209291/c2a528e2-f638-46d1-b9e3-9c8c1536c558"><br/>


Strategy 5:<br/>
a=(((opt4_call_vega_60d-opt4_put_vega_60d)/(opt4_call_vega_30d+opt4_put_vega_30d)));<br/>
d=trade_when(opt4_call_gamma_30d>0,a,-1);<br/>
b=ts_weighted_decay(d);<br/>
group_neutralize(b,pv13_r2_min2_3000_sector)<br/>

![vega](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/92904ad9-478c-48a7-ae16-715677e159c9)<br/>


Strategy 6:</br>
t=80;</br>
p=10;</br>
hm=1/(ts_mean(1/close,t));</br>
am=ts_mean(close,t);</br>
a=100*(1-(hm/am));</br>
b=p/100;</br>
trade_when(a>b,hump(ts_decay_exp_window((vwap/close)-1,t),hump=0.001),a<b)</br>


