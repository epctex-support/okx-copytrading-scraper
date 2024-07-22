# Actor - OKX Copy Trading Scraper
OKX Copy Trading, is a popular copy trading platform of OKX cryptocurrency exchange, lacks a robust and freely accessible API. To bridge this gap, we present the OKX Copy Trading Scraper, designed to facilitate seamless data extraction and analysis from this popular copy trading platform.

- **Filter Traders with Advanced Search**: Advanced search in the futures tab, not only by search type but also by filtering traders by their assets, AUM, win rate and many other parameters.

- **Account Information Scraping with Performance Statistics**: In addition to traders' account information, get detailed statistics on both futures and personal performance.

- **Ongoing Orders Scraping**: Get detailed information about traders' active ongoing orders, including which coins they are trading, how many assets they are trading, how many X leverage they are using and more.

- **Ongoing Orders History Scraping**: If you want to scrape the history of traders' ongoing orders, you can also get all the trades they have made in the past, down to the date and time they opened and closed the position, again in detail and effortlessly.

## Bugs, fixes, updates, and changelog
This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex-support/okx-copytrading-scraper/issues).


## Input Parameters
The input of this scraper should be JSON containing the list of pages on OKX Copy Trading that should be visited. Required fields are:

- `startUrls`: (Optional) (Array) List of OKX Trading Influencers URLs.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. The default is `Infinite`. This applies to all `search` requests and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `searchType`: (Optional) (String) Keyword by which type you want to filter and search users in the futures section of OKX Copy Trading.

	* `overview`: Search by Overview
	* `yieldRatio`: Search by PnL%
	* `pnl`: Search by PnL
	* `winRatio`: Search by Win rate
	* `aum`: Search by AUM
	* `traderFollowerLimit`: Search by No. of copy traders
	* `followTotalPnl`: Search by Copy trader PnL

- `leaderHasVacancies`: (Optional) (Boolean) If you want to search users with vacancies, you can set `true`. Default setting is `false`.

- `allowApiTraders`: (Optional) (Boolean) If you want to search API traders, you can set `true`. Default setting is `false`.

- `timeAsLeader`: (Optional) (Number) Search by filtering by how long a leader has been a leader.

    * `7`: Leading for more than 7 days
    * `30`: Leading for more than 30 days
    * `90`: Leading for more than 90 days
    * `180`: Leading for more than 180 days

- `winRate`: (Optional) (Number) Search by filtering by a leader's win rate.

    * `0.5`: Traders with a win rate of more than 50%
    * `0.6`: Traders with a win rate of more than 60%
    * `0.7`: Traders with a win rate of more than 70%
    * `0.8`: Traders with a win rate of more than 80%
    * `0.9`: Traders with a win rate of more than 90%

- `minLeaderAssets`: (Optional) (Number) Search by filtering by a leader's minimum asset. *(The value can only be integers between 0 and 50000)*

- `maxLeaderAssets`: (Optional) (Number) Search by filtering by a leader's maximum asset. *(The value can only be integers between 0 and 50000)*

- `minLeaderAum`: (Optional) (Number) Search by filtering by a leader's minimum AUM. *(The value can only be integers between 0 and 500000)*

- `maxLeaderAum`: (Optional) (Number) Search by filtering by a leader's minimum AUM. *(The value can only be integers between 0 and 500000)*

- `includeHistoricalPositions`: (Optional) (Boolean) If you want the history of the user's open positions to be scraped as well, you can set `true`. Default setting is `false`.

- `onlyUserInformation`: (Optional) (Boolean) If you want only user information to be scraped with relevant performance stats(futures or personal), you can set `true`. Default setting is `false`. *(If the value is true, data from ongoing orders and the history of ongoing orders are ignored and only the trader account information and the trader's performance statistics are scraped.)*

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as an argument and returns an object with data.

- `customMapFunction`: (Optional) (String) Function that takes each object's handle as an argument and returns the object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip
When you want to scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

### Compute Unit Consumption
The actor is optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detailed requests. If the actor doesn't block very often it'll scrape 200 listings in 1 minutes with ~0.03-0.05 compute units.

### OKX Copy Trading Scraper Input example
```json
{
    "startUrls": [
        "https://www.okx.com/copy-trading/account/305B2C62DA40873F",
    ],
    "searchType": "pnl",
    "leaderHasVacancies": true,
    "allowApiTraders": false,
    "timeAsLeader": 180,
    "winRate": 0.5,
    "minLeaderAssets": 10000,
    "maxLeaderAssets": 49999,
    "minLeaderAum": 100000,
    "maxLeaderAum": 499999,
    "includeHistoricalPositions": false,
    "onlyUserInformation": true,
    "maxItems": 100,
    "endPage": 3,
    "proxy": {
        "useApifyProxy": true
    }
}
```

## During the Run
During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.

When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with a failure state and output an explanation of what is wrong.

## OKX Copy Trading Export
During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any language (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this OKX Copy Trading actor.

## Scraped OKX Copy Trading Properties
The structure of each item in OKX Copy Trading looks like this:

### Account Information with Performance Stats in Detail
```json
{
	"url": "https://www.okx.com/copy-trading/account/BA1A719B8225DD83",
	"type": "user",
	"uniqueName": "BA1A719B8225DD83",
	"apiTrader": "0",
	"portrait": "",
	"nickName": "Linen_bitmex",
	"enNickName": "",
	"sign": "Linen-Horse-Flasher\nBitmex Leader board rank 20th +1261 BTC",
	"translatedBio": "",
	"enSign": "",
	"day": "164",
	"count": "718",
	"followeeNum": "0",
	"targetId": "4",
	"roleType": "1",
	"spotRoleType": "0",
	"publicStatus": "2",
	"isStrategyLead": true,
	"isSignalTrader": false,
	"isChinese": false,
	"isFollowed": false,
	"maxRetreat": "0",
	"profitDays": "61",
	"lossDays": "68",
	"winRatio": "0.4729",
	"pnlProfitLossRatio": "1.96:1",
	"avgPositionValue": "3048.5069",
	"tradeInfo": [
		{
			"aum": "3764.289879127359881",
			"copierFollowPnl": "",
			"copyRelId": "",
			"emptyMinderState": "0",
			"followPnl": "0",
			"followerLimit": "100",
			"followerNum": "33",
			"followerStatus": "",
			"followerTime": "",
			"instruments": [
				{
					"instId": "BTC-USDT-SWAP",
					"name": "BTC",
					"selected": "1"
				}
			],
			"leadMode": "1",
			"pnl": "",
			"roleType": "1",
			"shareRatio": "0.08",
			"signalProtect": "0",
			"symbol": "USDT",
			"totalFollowerNum": "599"
		}
	],
	"weekPnl": [
		{
			"pnl": "279374.2487426150408692",
			"ratio": "0.1941",
			"statTime": "1714320000000"
		}
	],
	"yieldPnl": [
		{
			"pnl": "0",
			"ratio": "0.0",
			"statTime": "1707580800000"
		}
	],
	"tradeData": [
		{
			"nonPeriodicPart": [
				{
					"desc": "Number of days this trader has been a lead trader for.",
					"functionId": "initialDay",
					"learnMoreUrl": "",
					"order": 1,
					"title": "Days leading trades",
					"type": "2",
					"value": "158"
				}
			],
			"periodicPart": [
				{
					"desc": "",
					"functionId": "profitDays",
					"learnMoreUrl": "",
					"order": 1,
					"title": "Days w/ profit",
					"type": "2",
					"value": "61"
				}
			]
		}
	],
	"followerList": [
		{
			"followers": [
				{
					"aum": "600108.5815629774006084",
					"coinSymbol": "USDT",
					"followDays": "113",
					"followTime": "1711634478000",
					"nickName": "jolupacc",
					"pnl": "6452.3200830850595381",
					"portrait": "",
					"targetId": "6",
					"uniqueName": "D0DE8C8F985B0B83"
				}
			],
			"pnlCoinSymbol": "USDT",
			"sevenDaysFollowerFlag": "1",
			"sevenDaysFollowerNum": "1",
			"sevenDaysFollowerRatio": "0.0017",
			"sevenDaysFollowerRatioFlag": "1",
			"statTime": "1721318399000",
			"totalFollowerNum": "599",
			"totalFollowerPnl": "-15063.2883850446245517"
		}
	],
	"preferenceCoin": [
		{
			"currency": "BTC",
			"percent": "0.507"
		}
	],
	"positionHistoryScatter": [
		{
			"itemScatterList": [
				{
					"closePnl": "-9.5936",
					"holdTimeMS": "84769024"
				}
			],
			"symbol": "USDT"
		}
	],
	"totalPnl": [
		{
			"ratio": "0.0961",
			"statTime": "1707148800000"
		}
	],
	"monthlyPnl": [
		{
			"ratio": "",
			"statTime": "1690819200000"
		}
	],
	"riskLevel": [
		{
			"highRisk": "8",
			"isDisplayLastRiskRevel": "1",
			"lastRiskLevel": "middle",
			"middleRisk": "4",
			"risks": [
				[
					"1690819200000",
					""
				]
			]
		}
	],
	"maxDrawdown": [
		{
			"dayMaxDrawdown": "-0.2962",
			"historyMaxDrawdown": "-0.7241",
			"weekMaxDrawdown": "-0.3025"
		}
	]
}
```

### Ongoing Orders in Detail
```json
{
    "availSubPos": "120",
    "ccy": "USDT",
    "closePnl": "0",
    "dealVolume": "",
    "fee": "-14.13312",
    "fundingFee": "6.1597664188335026",
    "imr": "6973.668",
    "instId": "BTC-USDT-SWAP",
    "instType": "SWAP",
    "last": "58113.7",
    "lever": "10",
    "liquidationFee": "",
    "margin": "7066.56",
    "markPx": "58113.9",
    "maxSellableAmount": "",
    "mgnMode": "cross",
    "notionalUsd": "69746.4431352",
    "openAvgPx": "58888",
    "openTime": "1720514981796",
    "pnl": "928.92",
    "pnlRatio": "0.13145292759136",
    "posSide": "short",
    "posType": "3",
    "side": "sell",
    "slOrdPx": "",
    "slTriggerPx": "",
    "slTriggerType": "last",
    "subPos": "120",
    "tpOrdPx": "",
    "tpTriggerPx": "",
    "tpTriggerType": "last",
    "tradeItemId": "1611034911019958274",
    "uTime": "1720656000048",
    "uniqueName": "94736C533515E1FC"
}
```

### History of Ongoing Orders in Detail
```json
{
    "ccy": "USDT",
    "closeAvgPx": "57553.5",
    "closePnl": "200.7",
    "contractVal": "0.01",
    "dealVolume": "",
    "fee": "-24.21261",
    "fundingFee": "9.4025595349621039",
    "id": "1603333729782661120",
    "instId": "BTC-USDT-SWAP",
    "instType": "SWAP",
    "lever": "10",
    "liquidationFee": "0",
    "margin": "3473.28",
    "mgnMode": "cross",
    "multiplier": "1",
    "openAvgPx": "57888",
    "openTime": "1720286183640",
    "pnl": "185.8899495349621039",
    "pnlRatio": "0.053520001132924",
    "posSide": "short",
    "posType": "3",
    "side": "sell",
    "subPos": "60",
    "tradeItemId": "1603333729782661120",
    "type": "2",
    "uTime": "1720642621960",
    "uniqueName": "94736C533515E1FC"
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that are available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
