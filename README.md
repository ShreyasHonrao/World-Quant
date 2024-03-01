# World-Quant
Strategy 1:
alpha= -ts_decay_exp_window((2*close-high-low)/(high-low)*volume,252);
b=ts_median(alpha,5);
c=(b/ts_mean(volume,42));
alp=trade_when(mcr38_adx_signal>25,c,mcr38_adx_signal<20);
x=group_neutralize(alp,pv13_r2_min2_3000_sector);

![close](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/499ad69b-acab-48d7-b7de-260c87db6662)

Strategy 2:
e=(ts_delay(implied_volatility_call_120,120)/ts_delay(implied_volatility_call_90,90));
alpha=ts_decay_exp_window(hump(implied_volatility_call_360-implied_volatility_put_360,hump=0.001),252);
trade_when(e<1.35,alpha,-rank(implied_volatility_put_120/implied_volatility_call_10))

![vol](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/8eb56e53-0b7c-4b69-af85-670f15656030)


Strategy 3:
a=-power(rank_by_side(oth466_rt_stk_split_ratio),2)+2*to_nan(power(rank_by_side(mdl130_qes_rcr),2),value=0,reverse=true);
b=group_neutralize(a,exchange);
c=b*(rank(-a)+1);
d=hump(c,hump=0.001);
signed_power(hump_decay(d*(1+.125*rank(-cap))),2)

<img width="723" alt="split_ratio" src="https://github.com/ShreyasHonrao/World-Quant/assets/108209291/d5084003-2887-4eeb-980f-0cbf9d6fd728">


Strategy 4:
a=group_neutralize(ts_scale((vwap-close)/(vwap+close),60)*ts_weighted_decay(ts_arg_min(news_mins_10_chg*(scale((volume))),60))*(vwap/close),market);
alpha  = trade_when(ts_std_dev(volume,15)<ts_std_dev(volume,120),a,-1);
quantile((returns>0.025 ? (1-returns)*alpha : alpha))

<img width="735" alt="vwap" src="https://github.com/ShreyasHonrao/World-Quant/assets/108209291/c2a528e2-f638-46d1-b9e3-9c8c1536c558">


Strategy 5:
a=(((opt4_call_vega_60d-opt4_put_vega_60d)/(opt4_call_vega_30d+opt4_put_vega_30d)));
d=trade_when(opt4_call_gamma_30d>0,a,-1);
b=ts_weighted_decay(d);
group_neutralize(b,pv13_r2_min2_3000_sector);

![vega](https://github.com/ShreyasHonrao/World-Quant/assets/108209291/92904ad9-478c-48a7-ae16-715677e159c9)



