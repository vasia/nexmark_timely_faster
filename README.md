# Window evaluation techniques with alternative state backends

1. Record buffer
2. Window buckets
3. Panes

## Running a Query
Each query can be run for a specified duration (in seconds) and with a given event generation rate

Queries have three varieties. To run using "vanilla" Timely simply supply the query number e.g. `q3`. To run using Managed State supply the desired state backend as a suffix e.g. `q3_faster` or `q3_mem`.
```bash
$ cargo run --release -- --duration 1000 --rate 1000000 --queries q3_faster
```

## Running on multiple workers/processes
Timely Dataflow accepts configuration via arguments supplied at runtime. These can be passed by adding an extra `--` between the line above and Timely's arguments.

For example to run with four workers:
```bash
$ cargo run --release -- --duration 1000 --rate 1000000 --queries q3_faster -- -w 4
```

## Explaining the output
(This is Moritz's explanation)

This will produce output similar to the following:

        Finished release [optimized + debuginfo] target(s) in 0.03s
         Running `target/release/nexmark --rate 1000000 --duration 30 --queries q3_faster -- -w4`
    statm_RSS	11207	1191936
    statm_RSS	500093138	143286272
    statm_RSS	1000177255	143323136
    statm_RSS	1500263478	143335424
    statm_RSS	2000348862	143282176
    statm_RSS	2500427146	143306752
    statm_RSS	3000510903	143294464
    statm_RSS	3500589805	143343616
    statm_RSS	4000674417	143368192
    statm_RSS	4500758623	143294464
    statm_RSS	5000845824	143458304
    statm_RSS	5500932658	143421440
    statm_RSS	6001016329	143392768
    statm_RSS	6500100357	143343616
    statm_RSS	7000184078	143400960
    statm_RSS	7500267736	143466496
    statm_RSS	8000352564	143433728
    statm_RSS	8500437906	143450112
    statm_RSS	9000521337	143454208
    statm_RSS	9500604198	143351808
    statm_RSS	10000687008	143433728
    statm_RSS	10500769241	143429632
    statm_RSS	11000856297	143405056
    statm_RSS	11500943404	143400960
    statm_RSS	12001026310	143478784
    statm_RSS	12500103922	143413248
    statm_RSS	13000189306	143388672
    statm_RSS	13500267298	143368192
    statm_RSS	14000350281	143462400
    statm_RSS	14500435223	143462400
    statm_RSS	15000518534	143392768
    statm_RSS	15500602761	143429632
    statm_RSS	16000685690	143441920
    statm_RSS	16500769981	143450112
    statm_RSS	17000856149	143441920
    statm_RSS	17500941156	143417344
    statm_RSS	18001024801	143446016
    statm_RSS	18500108779	143458304
    statm_RSS	19000195481	143495168
    statm_RSS	19500280029	143446016
    statm_RSS	20000364139	143519744
    statm_RSS	20500449183	143474688
    statm_RSS	21000534631	143384576
    statm_RSS	21500619807	143429632
    statm_RSS	22000705706	143437824
    statm_RSS	22500783532	143503360
    statm_RSS	23000872966	143425536
    statm_RSS	23500953048	143405056
    statm_RSS	24001037920	143466496
    statm_RSS	24500123394	143462400
    statm_RSS	25000208318	143564800
    statm_RSS	25500293209	143499264
    statm_RSS	26000379004	143486976
    statm_RSS	26500462933	143511552
    statm_RSS	27000548406	143482880
    statm_RSS	27500631475	143454208
    statm_RSS	28000716668	143470592
    statm_RSS	28500802035	143454208
    statm_RSS	29000891828	143413248
    statm_RSS	29500977316	143523840
    statm_RSS	30001057364	143482880
    latency_ccdf	122880	1	21
    latency_ccdf	126976	0.9999997980769251	74
    latency_ccdf	131072	0.9999990865384704	219
    latency_ccdf	139264	0.9999969807692598	35299
    latency_ccdf	147456	0.999657567310985	296241
    latency_ccdf	155648	0.996809096184528	636340
    latency_ccdf	163840	0.9906904423972073	793091
    latency_ccdf	172032	0.9830645674705331	830141
    latency_ccdf	180224	0.9750824425472842	838164
    latency_ccdf	188416	0.9670231733940079	842592
    latency_ccdf	196608	0.9589213273180641	846156
    latency_ccdf	204800	0.9507852120116806	848651
    latency_ccdf	212992	0.9426251063209125	850364
    latency_ccdf	221184	0.9344485294764564	850920
    latency_ccdf	229376	0.9262666064782057	851531
    latency_ccdf	237568	0.9180788084800114	851461
    latency_ccdf	245760	0.9098916835587338	851930
    latency_ccdf	253952	0.9017000490221149	851918
    latency_ccdf	262144	0.8935085298701103	851825
    latency_ccdf	278528	0.8853179049488663	1703577
    latency_ccdf	294912	0.8689373570294485	1703895
    latency_ccdf	311296	0.8525537514177524	1703857
    latency_ccdf	327680	0.8361705111906682	1703741
    latency_ccdf	344064	0.8197883863481886	1703852
    latency_ccdf	360448	0.803405194198027	1703642
    latency_ccdf	376832	0.7870240212786151	1703881
    latency_ccdf	393216	0.7706405502823024	1703869
    latency_ccdf	409600	0.7542571946706039	1703739
    latency_ccdf	425984	0.7378750890588934	1704149
    latency_ccdf	442368	0.7214890411395285	1703737
    latency_ccdf	458752	0.705106954758587	1703815
    latency_ccdf	475136	0.6887241183776527	1703952
    latency_ccdf	491520	0.6723399646890388	1703639
    latency_ccdf	507904	0.6559588206157806	1704081
    latency_ccdf	524288	0.6395734265425632	1704028
    latency_ccdf	557056	0.6231885420847255	3407857
    latency_ccdf	589824	0.5904206866305703	3407803
    latency_ccdf	622592	0.5576533504071793	3407744
    latency_ccdf	655360	0.5248865814914752	3408032
    latency_ccdf	688128	0.4921170433450284	3407816
    latency_ccdf	720896	0.4593495821216386	3407890
    latency_ccdf	753664	0.42658140935979416	3407847
    latency_ccdf	786432	0.39381365005948415	3407831
    latency_ccdf	819200	0.3610460446053265	3407956
    latency_ccdf	851968	0.3282772372281035	3407980
    latency_ccdf	884736	0.29550819908165193	3407769
    latency_ccdf	917504	0.2627411897813347	3407624
    latency_ccdf	950272	0.22997557471177332	3408205
    latency_ccdf	983040	0.1972043731038041	3407834
    latency_ccdf	1015808	0.16443673880349288	3407742
    latency_ccdf	1048576	0.1316699891185578	3407766
    latency_ccdf	1114112	0.09890300866439415	6815950
    latency_ccdf	1179648	0.033365028525336266	3445192
    latency_ccdf	1245184	0.00023818269001747413	22930
    latency_ccdf	1310720	0.00001770192290671228	758
    latency_ccdf	1376256	0.000010413461438332101	524
    latency_ccdf	1441792	0.000005374999948317308	314
    latency_ccdf	1507328	0.000002355769208117604	242
    latency_ccdf	1572864	0.000000028846153568786986	2
    latency_ccdf	1638400	0.000000009615384522928995	0
    summary_timeline	0	442368	720896	983040	1245184	1245184	1310720	1376256
    summary_timeline	250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	750000000	425984	688128	950272	1179648	1245184	1310720	1310720
    summary_timeline	1000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	1250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	1500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	1750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	2000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	2250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	2500000000	442368	720896	950272	1179648	1245184	1310720	1507328
    summary_timeline	2750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	3000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	3250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	3500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	3750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	4000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	4250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	4500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	4750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	5000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	5250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	5500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	5750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	6000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	6250000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	6500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	6750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	7000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	7250000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	7500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	7750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	8000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	8250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	8500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	8750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	9000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	9250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	9500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	9750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	10000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	10250000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	10500000000	425984	688128	950272	1179648	1245184	1376256	1638400
    summary_timeline	10750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	11000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	11250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	11500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	11750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	12000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	12250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	12500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	12750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	13000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	13250000000	425984	688128	950272	1179648	1245184	1245184	1376256
    summary_timeline	13500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	13750000000	425984	688128	950272	1179648	1245184	1310720	1376256
    summary_timeline	14000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	14250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	14500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	14750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	15000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	15250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	15500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	15750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	16000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	16250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	16500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	16750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	17000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	17250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	17500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	17750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	18000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	18250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	18500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	18750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	19000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	19250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	19500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	19750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	20000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	20250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	20500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	20750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	21000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	21250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	21500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	21750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	22000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	22250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	22500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	22750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	23000000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	23250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	23500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	23750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	24000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	24250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	24500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	24750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	25000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	25250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	25500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	25750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	26000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	26250000000	425984	688128	950272	1179648	1245184	1245184	1245184
    summary_timeline	26500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	26750000000	425984	720896	950272	1179648	1245184	1310720	1376256
    summary_timeline	27000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	27250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	27500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	27750000000	425984	688128	950272	1179648	1245184	1245184	1376256
    summary_timeline	28000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	28250000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	28500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	28750000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	29000000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	29250000000	425984	688128	950272	1179648	1245184	1376256	1638400
    summary_timeline	29500000000	425984	688128	950272	1179648	1245184	1245184	1310720
    summary_timeline	29750000000	425984	688128	950272	1179648	1245184	6291456	6553600


The output is a list of tab-separated values on `stdout`.
* `statm_RSS	13000189306	143388672`: RSS memory consumption of `143388672` bytes at time `13000189306`ns since start of application.
* `latency_ccdf	229376	0.9262666064782057	851531`: latency CCDF value, `851531` measurements, smaller than `0.9262666064782057`% of all measurements, latency `229376`ns.
* `summary_timeline	1250000000	425984	688128	950272	1179648	1245184	1245184	1310720`: Some percentiles at time `1250000000`ns: 25%, 50%, 75%, 99%, 99.9%, max in nanoseconds.
