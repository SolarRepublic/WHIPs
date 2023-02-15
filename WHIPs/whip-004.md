# WHIP-004: Registry of Common Entity Declarations

```
Number:  WHIP-004
Title:   Registry of Common Entity Declarations
Type:    Registry
Status:  Draft
Authors: Blake Regalia (@blake-regalia)
Created: 2023-01-15
```


## Abstract

WHIP-004 provides a registry of reusable entity declarations ([WHIP-003](./whip-003.md)) for commonly used contracts, giving apps quick and easy access to provide declarations on their site.


## Motivation

WHIP-003 implementors may end up spending time writing declarations by hand and finding entity icons for already well-known contracts such as fungible tokens. A registry not only saves implementors time by cutting down on duplicated efforts, but it also provides a reference for how other contracts are declared.


## Registry

This registry consists of two parts:
  - [Icons](#icons) - plug-and-play `<link>` elements that serve icons from GitHub CDN
  - [Definitions](#definitions) - TOML blocks that can be copy-pasted into your head's TOML script content

Apps should only copy those declarations for entities they intend to support so that clients do not load the prefetch icons unnecessarily.


### Icons

> Never embed SVGs directly into the HTML of your app since they can become XSS vectors, always use `<link>` or `<img>` tags. Setting a rigid [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) will also help protect against XSS attacks.

Icons for the entity declarations are located under the adjacent [./whip-004](./whip-004) subdirectory, allowing them to also be hosted from GitHub's `raw.githubusercontent.com` CDN.

Remember that these elements belong in the `<head>` of your HTML document.

Combined:
```html

<!-- sSCRT - Secret Secret -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/sscrt.svg" data-caip-19="cosmos:secret-4/snip20:secret1k0jntykt7e4g3y88ltc60czgjuqdy4c9e8fzek">


<!-- sAAVE - Aave -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/aave.svg" data-caip-19="cosmos:secret-4/snip20:secret1yxwnyk8htvvq25x2z87yj0r5tqpev452fk6h5h">


<!-- sBLD - Agoric -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/bld.svg" data-caip-19="cosmos:secret-4/snip20:secret1rw2l7z22s3ed6dl5v70ktvnckhurldy23a3a58">


<!-- sAKT - Akash -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/akt.svg" data-caip-19="cosmos:secret-4/snip20:secret168j5f78magfce5r2j4etaytyuy7ftjkh4cndqw">


<!-- ALTER - Alter -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/alter.svg" data-caip-19="cosmos:secret-4/snip20:secret12rcvz0umvk875kd6a803txhtlu7y0pnd73kcej">


<!-- AMBER - Amber -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/amber.svg" data-caip-19="cosmos:secret-4/snip20:secret1s09x2xvfd2lp2skgzm29w2xtena7s8fq98v852">


<!-- sBAND - Band Protocol -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/band.svg" data-caip-19="cosmos:secret-4/snip20:secret1p4zvqgxggrrk435nj94p6la2g4xd0rwssgzpsr">


<!-- sBNB(BSC) - Binance Coin -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/bnb.svg" data-caip-19="cosmos:secret-4/snip20:secret1tact8rxxrvynk4pwukydnle4l0pdmj0sq9j9d5">


<!-- sBUSD(BSC) - Binance USD (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/busd.svg" data-caip-19="cosmos:secret-4/snip20:secret1793ctg56epnzjlv7t7mug2tv3s2zylhqssyjwe">


<!-- BUTT - Button -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/butt.svg" data-caip-19="cosmos:secret-4/snip20:secret1yxcexylwyxlq58umhgsjgstgcg2a0ytfy4d9lt">


<!-- sADA(BSC) - Cardano (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/ada.svg" data-caip-19="cosmos:secret-4/snip20:secret1t6228qgqgkwhnsegk84ahljgw2cj7f9xprk9zd">


<!-- sLINK - Chainlink -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/link.svg" data-caip-19="cosmos:secret-4/snip20:secret1xcrf2vvxcz8dhtgzgsd0zmzlf9g320ea2rhdjw">


<!-- sHUAHUA - Chihuahua -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/huahua.svg" data-caip-19="cosmos:secret-4/snip20:secret1ntvxnf5hzhzv8g87wn76ch6yswdujqlgmjh32w">


<!-- sATOM - Cosmos Hub -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/atom.svg" data-caip-19="cosmos:secret-4/snip20:secret14mzwd0ps5q277l20ly2q3aetqe3ev4m4260gf4">


<!-- sCRE - Crescent -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/cre.svg" data-caip-19="cosmos:secret-4/snip20:secret1tatdlkyznf00m3a7hftw5daaq2nk38ugfphuyr">


<!-- sDAI - Dai -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/dai.svg" data-caip-19="cosmos:secret-4/snip20:secret1vnjck36ld45apf8u4fedxd5zy7f5l92y3w5qwq">


<!-- sMANA - Decentraland -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/mana.svg" data-caip-19="cosmos:secret-4/snip20:secret178t2cp33hrtlthphmt9lpd25qet349mg4kcega">


<!-- sETH - Ethereum -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/eth.svg" data-caip-19="cosmos:secret-4/snip20:secret1wuzzjsdhthpvuyeeyhfq2ftsn3mvwf9rxy6ykw">


<!-- sETH(BSC) - Ethereum (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/eth.svg" data-caip-19="cosmos:secret-4/snip20:secret1m6a72200733a7jnm76xrznh9cpmt4kf5ql0a6t">


<!-- sEVMOS - Evmos -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/evmos.svg" data-caip-19="cosmos:secret-4/snip20:secret1grg9unv2ue8cf98t50ea45prce7gcrj2n232kq">


<!-- sGRAV - Gravity Bridge -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/grav.svg" data-caip-19="cosmos:secret-4/snip20:secret1dtghxvrx35nznt8es3fwxrv4qh56tvxv22z79d">


<!-- sINJ - Injective -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/inj.svg" data-caip-19="cosmos:secret-4/snip20:secret16cwf53um7hgdvepfp3jwdzvwkt5qe2f9vfkuwv">


<!-- sIST - Inter-stable token -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/ist.png" data-caip-19="cosmos:secret-4/snip20:secret1kjqktuq2wq6mk7l0ecvk2cwcskjmv3ghpklctn">


<!-- sJUNO - Juno -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/juno.svg" data-caip-19="cosmos:secret-4/snip20:secret1smmc5k24lcn4j2j8f3w0yaeafga6wmzl0qct03">


<!-- sKUJI - Kujira -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/kuji.svg" data-caip-19="cosmos:secret-4/snip20:secret1gaew7k9tv4hlx2f4wq4ta4utggj4ywpkjysqe8">


<!-- sLUNA - Terra -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/luna.svg" data-caip-19="cosmos:secret-4/snip20:secret1w8d0ntrhrys4yzcfxnwprts7gfg5gfw86ccdpf">


<!-- sXMR - Monero -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/xmr.svg" data-caip-19="cosmos:secret-4/snip20:secret19ungtd2c7srftqdwgq0dspwvrw63dhu79qxv88">


<!-- sOCEAN - Ocean Protocol -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/ocean.svg" data-caip-19="cosmos:secret-4/snip20:secret12sjaw9wutn39cc5wqxfmkypm4n7tcerwfpvmps">


<!-- sOSMO - Osmosis -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/osmo.svg" data-caip-19="cosmos:secret-4/snip20:secret1zwwealwm0pcl9cul4nt6f38dsy6vzplw8lp3qg">


<!-- sROWAN - Sifchain -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/rowan.svg" data-caip-19="cosmos:secret-4/snip20:secret159p22zvq2wzsdtqhm2plp4wg33srxp2hf0qudc">


<!-- sSTRD - Stride -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/strd.png" data-caip-19="cosmos:secret-4/snip20:secret17gg8xcx04ldqkvkrd7r9w60rdae4ck8aslt9cf">


<!-- sDOT(BSC) - Polkadot (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/dot.svg" data-caip-19="cosmos:secret-4/snip20:secret1px5mtmjh072znpez4fjpmxqsv3hpevdpyu9l4v">


<!-- sRSR - ReserveRights -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/rsr.svg" data-caip-19="cosmos:secret-4/snip20:secret1vcm525c3gd9g5ggfqg7d20xcjnmcc8shh902un">


<!-- sSCRT(BSC) - Secret (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/scrt.svg" data-caip-19="cosmos:secret-4/snip20:secret1c7apt5mmv9ma5dpa9tmwjunhhke9de2206ufyp">


<!-- sDVPN - Sentinel -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/dvpn.png" data-caip-19="cosmos:secret-4/snip20:secret1k8cge73c3nh32d4u0dsd5dgtmk63shtlrfscj5">


<!-- SHD - Shade -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/shd.svg" data-caip-19="cosmos:secret-4/snip20:secret1qfql357amn448duf5gvp9gr48sxx9tsnhupu3d">


<!-- SIENNA - Sienna -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/sienna.svg" data-caip-19="cosmos:secret-4/snip20:secret1rgm2m5t530tdzyd99775n6vzumxa5luxcllml4">


<!-- stkd-SCRT - Staked SCRT Derivative (Shade) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/stkd-scrt.svg" data-caip-19="cosmos:secret-4/snip20:secret1k6u0cy4feepm6pehnz804zmwakuwdapm69tuc4">


<!-- seSCRT - StakeEasy staked SCRT -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/sescrt.png" data-caip-19="cosmos:secret-4/snip20:secret16zfat8th6hvzhesj8f6rz3vzd7ll69ys580p2t">


<!-- sSTARS - Stargaze -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/stars.svg" data-caip-19="cosmos:secret-4/snip20:secret1x0dqckf2khtxyrjwhlkrx9lwwmz44k24vcv2vv">


<!-- sUSDT - Tether -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/usdt.svg" data-caip-19="cosmos:secret-4/snip20:secret18wpjn83dayu4meu6wnn29khfkwdxs7kyrz9c8f">


<!-- sUSDT(BSC) - Tether (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/usdt.svg" data-caip-19="cosmos:secret-4/snip20:secret16euwqyntvsp0fp2rstmggw77w5xgz2z26cpwxj">


<!-- sRUNE - THORChain -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/rune.svg" data-caip-19="cosmos:secret-4/snip20:secret1el5uj9ns9sty682dem033pt50xsv5mklmsvy24">


<!-- sUNI - Uniswap -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/uni.svg" data-caip-19="cosmos:secret-4/snip20:secret1ds8850j99cf5h3hygy25f0zzs6r6s7vsgfs8te">


<!-- sUSDC - USD Coin -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/usdc.svg" data-caip-19="cosmos:secret-4/snip20:secret1h6z05y90gwm4sqxzhz4pkyp36cna9xtp7q0urv">


<!-- sUSDC(BSC) - USD Coin (BSC) -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/usdc.svg" data-caip-19="cosmos:secret-4/snip20:secret1kf45vm4mg5004pgajuplcmkrzvsyp2qtvlklyg">


<!-- sWBTC - Wrapped BTC -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/wbtc.svg" data-caip-19="cosmos:secret-4/snip20:secret1g7jfnxmxkjgqdts9wlmn238mrzxz5r92zwqv4a">


<!-- sYFI - yearn.finance -->
<link rel="prefetch" as="image" href="https://raw.githubusercontent.com/SolarRepublic/WHIPs/main/WHIPs/whip-004/yfi.svg" data-caip-19="cosmos:secret-4/snip20:secret15grq8y54tvc24j8hf8chunsdcr84fd3d30fvqv">

```


### Definitions

Remember that these blocks belong within a `<script type="application/toml" data-whip-003>` element in the `<head>` of your HTML document.

Combined:
```toml

# sSCRT - Secret Secret
[contracts.cosmos_secret-4_sscrt]
chain = "cosmos:secret-4"
address = "secret1k0jntykt7e4g3y88ltc60czgjuqdy4c9e8fzek"
label = "Secret Secret"
[contracts.cosmos_secret-4_sscrt.interfaces.snip20]
symbol = "sSCRT"


# sAAVE - Aave
[contracts.cosmos_secret-4_saave]
chain = "cosmos:secret-4"
address = "secret1yxwnyk8htvvq25x2z87yj0r5tqpev452fk6h5h"
label = "Aave"
[contracts.cosmos_secret-4_saave.interfaces.snip20]
symbol = "sAAVE"


# sBLD - Agoric
[contracts.cosmos_secret-4_sbld]
chain = "cosmos:secret-4"
address = "secret1rw2l7z22s3ed6dl5v70ktvnckhurldy23a3a58"
label = "Agoric"
[contracts.cosmos_secret-4_sbld.interfaces.snip20]
symbol = "sBLD"


# sAKT - Akash
[contracts.cosmos_secret-4_sakt]
chain = "cosmos:secret-4"
address = "secret168j5f78magfce5r2j4etaytyuy7ftjkh4cndqw"
label = "Akash"
[contracts.cosmos_secret-4_sakt.interfaces.snip20]
symbol = "sAKT"


# ALTER - Alter
[contracts.cosmos_secret-4_alter]
chain = "cosmos:secret-4"
address = "secret12rcvz0umvk875kd6a803txhtlu7y0pnd73kcej"
label = "Alter"
[contracts.cosmos_secret-4_alter.interfaces.snip20]
symbol = "ALTER"


# AMBER - Amber
[contracts.cosmos_secret-4_amber]
chain = "cosmos:secret-4"
address = "secret1s09x2xvfd2lp2skgzm29w2xtena7s8fq98v852"
label = "Amber"
[contracts.cosmos_secret-4_amber.interfaces.snip20]
symbol = "AMBER"


# sBAND - Band Protocol
[contracts.cosmos_secret-4_sband]
chain = "cosmos:secret-4"
address = "secret1p4zvqgxggrrk435nj94p6la2g4xd0rwssgzpsr"
label = "Band Protocol"
[contracts.cosmos_secret-4_sband.interfaces.snip20]
symbol = "sBAND"


# sBNB(BSC) - Binance Coin
[contracts.cosmos_secret-4_sbnb_bsc]
chain = "cosmos:secret-4"
address = "secret1tact8rxxrvynk4pwukydnle4l0pdmj0sq9j9d5"
label = "Binance Coin"
[contracts.cosmos_secret-4_sbnb_bsc.interfaces.snip20]
symbol = "sBNB(BSC)"


# sBUSD(BSC) - Binance USD (BSC)
[contracts.cosmos_secret-4_sbusd_bsc]
chain = "cosmos:secret-4"
address = "secret1793ctg56epnzjlv7t7mug2tv3s2zylhqssyjwe"
label = "Binance USD (BSC)"
[contracts.cosmos_secret-4_sbusd_bsc.interfaces.snip20]
symbol = "sBUSD(BSC)"


# BUTT - Button
[contracts.cosmos_secret-4_butt]
chain = "cosmos:secret-4"
address = "secret1yxcexylwyxlq58umhgsjgstgcg2a0ytfy4d9lt"
label = "Button"
[contracts.cosmos_secret-4_butt.interfaces.snip20]
symbol = "BUTT"


# sADA(BSC) - Cardano (BSC)
[contracts.cosmos_secret-4_sada_bsc]
chain = "cosmos:secret-4"
address = "secret1t6228qgqgkwhnsegk84ahljgw2cj7f9xprk9zd"
label = "Cardano (BSC)"
[contracts.cosmos_secret-4_sada_bsc.interfaces.snip20]
symbol = "sADA(BSC)"


# sLINK - Chainlink
[contracts.cosmos_secret-4_slink]
chain = "cosmos:secret-4"
address = "secret1xcrf2vvxcz8dhtgzgsd0zmzlf9g320ea2rhdjw"
label = "Chainlink"
[contracts.cosmos_secret-4_slink.interfaces.snip20]
symbol = "sLINK"


# sHUAHUA - Chihuahua
[contracts.cosmos_secret-4_shuahua]
chain = "cosmos:secret-4"
address = "secret1ntvxnf5hzhzv8g87wn76ch6yswdujqlgmjh32w"
label = "Chihuahua"
[contracts.cosmos_secret-4_shuahua.interfaces.snip20]
symbol = "sHUAHUA"


# sATOM - Cosmos Hub
[contracts.cosmos_secret-4_satom]
chain = "cosmos:secret-4"
address = "secret14mzwd0ps5q277l20ly2q3aetqe3ev4m4260gf4"
label = "Cosmos Hub"
[contracts.cosmos_secret-4_satom.interfaces.snip20]
symbol = "sATOM"


# sCRE - Crescent
[contracts.cosmos_secret-4_scre]
chain = "cosmos:secret-4"
address = "secret1tatdlkyznf00m3a7hftw5daaq2nk38ugfphuyr"
label = "Crescent"
[contracts.cosmos_secret-4_scre.interfaces.snip20]
symbol = "sCRE"


# sDAI - Dai
[contracts.cosmos_secret-4_sdai]
chain = "cosmos:secret-4"
address = "secret1vnjck36ld45apf8u4fedxd5zy7f5l92y3w5qwq"
label = "Dai"
[contracts.cosmos_secret-4_sdai.interfaces.snip20]
symbol = "sDAI"


# sMANA - Decentraland
[contracts.cosmos_secret-4_smana]
chain = "cosmos:secret-4"
address = "secret178t2cp33hrtlthphmt9lpd25qet349mg4kcega"
label = "Decentraland"
[contracts.cosmos_secret-4_smana.interfaces.snip20]
symbol = "sMANA"


# sETH - Ethereum
[contracts.cosmos_secret-4_seth]
chain = "cosmos:secret-4"
address = "secret1wuzzjsdhthpvuyeeyhfq2ftsn3mvwf9rxy6ykw"
label = "Ethereum"
[contracts.cosmos_secret-4_seth.interfaces.snip20]
symbol = "sETH"


# sETH(BSC) - Ethereum (BSC)
[contracts.cosmos_secret-4_seth_bsc]
chain = "cosmos:secret-4"
address = "secret1m6a72200733a7jnm76xrznh9cpmt4kf5ql0a6t"
label = "Ethereum (BSC)"
[contracts.cosmos_secret-4_seth_bsc.interfaces.snip20]
symbol = "sETH(BSC)"


# sEVMOS - Evmos
[contracts.cosmos_secret-4_sevmos]
chain = "cosmos:secret-4"
address = "secret1grg9unv2ue8cf98t50ea45prce7gcrj2n232kq"
label = "Evmos"
[contracts.cosmos_secret-4_sevmos.interfaces.snip20]
symbol = "sEVMOS"


# sGRAV - Gravity Bridge
[contracts.cosmos_secret-4_sgrav]
chain = "cosmos:secret-4"
address = "secret1dtghxvrx35nznt8es3fwxrv4qh56tvxv22z79d"
label = "Gravity Bridge"
[contracts.cosmos_secret-4_sgrav.interfaces.snip20]
symbol = "sGRAV"


# sINJ - Injective
[contracts.cosmos_secret-4_sinj]
chain = "cosmos:secret-4"
address = "secret16cwf53um7hgdvepfp3jwdzvwkt5qe2f9vfkuwv"
label = "Injective"
[contracts.cosmos_secret-4_sinj.interfaces.snip20]
symbol = "sINJ"


# sIST - Inter-stable token
[contracts.cosmos_secret-4_sist]
chain = "cosmos:secret-4"
address = "secret1kjqktuq2wq6mk7l0ecvk2cwcskjmv3ghpklctn"
label = "Inter-stable token"
[contracts.cosmos_secret-4_sist.interfaces.snip20]
symbol = "sIST"


# sJUNO - Juno
[contracts.cosmos_secret-4_sjuno]
chain = "cosmos:secret-4"
address = "secret1smmc5k24lcn4j2j8f3w0yaeafga6wmzl0qct03"
label = "Juno"
[contracts.cosmos_secret-4_sjuno.interfaces.snip20]
symbol = "sJUNO"


# sKUJI - Kujira
[contracts.cosmos_secret-4_skuji]
chain = "cosmos:secret-4"
address = "secret1gaew7k9tv4hlx2f4wq4ta4utggj4ywpkjysqe8"
label = "Kujira"
[contracts.cosmos_secret-4_skuji.interfaces.snip20]
symbol = "sKUJI"


# sXMR - Monero
[contracts.cosmos_secret-4_sxmr]
chain = "cosmos:secret-4"
address = "secret19ungtd2c7srftqdwgq0dspwvrw63dhu79qxv88"
label = "Monero"
[contracts.cosmos_secret-4_sxmr.interfaces.snip20]
symbol = "sXMR"


# sOCEAN - Ocean Protocol
[contracts.cosmos_secret-4_socean]
chain = "cosmos:secret-4"
address = "secret12sjaw9wutn39cc5wqxfmkypm4n7tcerwfpvmps"
label = "Ocean Protocol"
[contracts.cosmos_secret-4_socean.interfaces.snip20]
symbol = "sOCEAN"


# sOSMO - Osmosis
[contracts.cosmos_secret-4_sosmo]
chain = "cosmos:secret-4"
address = "secret1zwwealwm0pcl9cul4nt6f38dsy6vzplw8lp3qg"
label = "Osmosis"
[contracts.cosmos_secret-4_sosmo.interfaces.snip20]
symbol = "sOSMO"


# sDOT(BSC) - Polkadot (BSC)
[contracts.cosmos_secret-4_sdot_bsc]
chain = "cosmos:secret-4"
address = "secret1px5mtmjh072znpez4fjpmxqsv3hpevdpyu9l4v"
label = "Polkadot (BSC)"
[contracts.cosmos_secret-4_sdot_bsc.interfaces.snip20]
symbol = "sDOT(BSC)"


# sRSR - ReserveRights
[contracts.cosmos_secret-4_srsr]
chain = "cosmos:secret-4"
address = "secret1vcm525c3gd9g5ggfqg7d20xcjnmcc8shh902un"
label = "ReserveRights"
[contracts.cosmos_secret-4_srsr.interfaces.snip20]
symbol = "sRSR"


# sSCRT(BSC) - Secret (BSC)
[contracts.cosmos_secret-4_sscrt_bsc]
chain = "cosmos:secret-4"
address = "secret1c7apt5mmv9ma5dpa9tmwjunhhke9de2206ufyp"
label = "Secret (BSC)"
[contracts.cosmos_secret-4_sscrt_bsc.interfaces.snip20]
symbol = "sSCRT(BSC)"


# sDVPN - Sentinel
[contracts.cosmos_secret-4_sdvpn]
chain = "cosmos:secret-4"
address = "secret1k8cge73c3nh32d4u0dsd5dgtmk63shtlrfscj5"
label = "Sentinel"
[contracts.cosmos_secret-4_sdvpn.interfaces.snip20]
symbol = "sDVPN"


# SHD - Shade
[contracts.cosmos_secret-4_shd]
chain = "cosmos:secret-4"
address = "secret1qfql357amn448duf5gvp9gr48sxx9tsnhupu3d"
label = "Shade"
[contracts.cosmos_secret-4_shd.interfaces.snip20]
symbol = "SHD"


# SIENNA - Sienna
[contracts.cosmos_secret-4_sienna]
chain = "cosmos:secret-4"
address = "secret1rgm2m5t530tdzyd99775n6vzumxa5luxcllml4"
label = "Sienna"
[contracts.cosmos_secret-4_sienna.interfaces.snip20]
symbol = "SIENNA"


# sROWAN - Sifchain
[contracts.cosmos_secret-4_srowan]
chain = "cosmos:secret-4"
address = "secret159p22zvq2wzsdtqhm2plp4wg33srxp2hf0qudc"
label = "Sifchain"
[contracts.cosmos_secret-4_srowan.interfaces.snip20]
symbol = "sROWAN"


# stkd-SCRT - Staked SCRT Derivative (Shade)
[contracts.cosmos_secret-4_stkd-scrt]
chain = "cosmos:secret-4"
address = "secret1k6u0cy4feepm6pehnz804zmwakuwdapm69tuc4"
label = "Staked SCRT Derivative (Shade)"
[contracts.cosmos_secret-4_stkd-scrt.interfaces.snip20]
symbol = "stkd-SCRT"


# seSCRT - StakeEasy staked SCRT
[contracts.cosmos_secret-4_sescrt]
chain = "cosmos:secret-4"
address = "secret16zfat8th6hvzhesj8f6rz3vzd7ll69ys580p2t"
label = "StakeEasy staked SCRT"
[contracts.cosmos_secret-4_sescrt.interfaces.snip20]
symbol = "seSCRT"


# sSTARS - Stargaze
[contracts.cosmos_secret-4_sstars]
chain = "cosmos:secret-4"
address = "secret1x0dqckf2khtxyrjwhlkrx9lwwmz44k24vcv2vv"
label = "Stargaze"
[contracts.cosmos_secret-4_sstars.interfaces.snip20]
symbol = "sSTARS"


# sSTRD - Stride
[contracts.cosmos_secret-4_sstrd]
chain = "cosmos:secret-4"
address = "secret17gg8xcx04ldqkvkrd7r9w60rdae4ck8aslt9cf"
label = "Stride"
[contracts.cosmos_secret-4_sstrd.interfaces.snip20]
symbol = "sSTRD"


# sLUNA - Terra
[contracts.cosmos_secret-4_sluna]
chain = "cosmos:secret-4"
address = "secret1w8d0ntrhrys4yzcfxnwprts7gfg5gfw86ccdpf"
label = "Terra"
[contracts.cosmos_secret-4_sluna.interfaces.snip20]
symbol = "sLUNA"


# sUSDT - Tether
[contracts.cosmos_secret-4_susdt]
chain = "cosmos:secret-4"
address = "secret18wpjn83dayu4meu6wnn29khfkwdxs7kyrz9c8f"
label = "Tether"
[contracts.cosmos_secret-4_susdt.interfaces.snip20]
symbol = "sUSDT"


# sUSDT(BSC) - Tether (BSC)
[contracts.cosmos_secret-4_susdt_bsc]
chain = "cosmos:secret-4"
address = "secret16euwqyntvsp0fp2rstmggw77w5xgz2z26cpwxj"
label = "Tether (BSC)"
[contracts.cosmos_secret-4_susdt_bsc.interfaces.snip20]
symbol = "sUSDT(BSC)"


# sRUNE - THORChain
[contracts.cosmos_secret-4_srune]
chain = "cosmos:secret-4"
address = "secret1el5uj9ns9sty682dem033pt50xsv5mklmsvy24"
label = "THORChain"
[contracts.cosmos_secret-4_srune.interfaces.snip20]
symbol = "sRUNE"


# sUNI - Uniswap
[contracts.cosmos_secret-4_suni]
chain = "cosmos:secret-4"
address = "secret1ds8850j99cf5h3hygy25f0zzs6r6s7vsgfs8te"
label = "Uniswap"
[contracts.cosmos_secret-4_suni.interfaces.snip20]
symbol = "sUNI"


# sUSDC - USD Coin
[contracts.cosmos_secret-4_susdc]
chain = "cosmos:secret-4"
address = "secret1h6z05y90gwm4sqxzhz4pkyp36cna9xtp7q0urv"
label = "USD Coin"
[contracts.cosmos_secret-4_susdc.interfaces.snip20]
symbol = "sUSDC"


# sUSDC(BSC) - USD Coin (BSC)
[contracts.cosmos_secret-4_susdc_bsc]
chain = "cosmos:secret-4"
address = "secret1kf45vm4mg5004pgajuplcmkrzvsyp2qtvlklyg"
label = "USD Coin (BSC)"
[contracts.cosmos_secret-4_susdc_bsc.interfaces.snip20]
symbol = "sUSDC(BSC)"


# sWBTC - Wrapped BTC
[contracts.cosmos_secret-4_swbtc]
chain = "cosmos:secret-4"
address = "secret1g7jfnxmxkjgqdts9wlmn238mrzxz5r92zwqv4a"
label = "Wrapped BTC"
[contracts.cosmos_secret-4_swbtc.interfaces.snip20]
symbol = "sWBTC"


# sYFI - yearn.finance
[contracts.cosmos_secret-4_syfi]
chain = "cosmos:secret-4"
address = "secret15grq8y54tvc24j8hf8chunsdcr84fd3d30fvqv"
label = "yearn.finance"
[contracts.cosmos_secret-4_syfi.interfaces.snip20]
symbol = "sYFI"

```

## References
- [WHIP-003](./whip-003.md)
- [`<link rel="prefetch" as="image" ...>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/prefetch)
- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md)
- [CAIP-19](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md)
- [TOML Spec](https://toml.io/en/)
- [JSON Spec](https://www.json.org/json-en.html)
- [SLIP-0044](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)
