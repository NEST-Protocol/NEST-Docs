### Request Price for Contract

#### Price Contract

##### mainnet
- ETH: 0xE544cF993C7d477C7ef8E91D28aCA250D135aa03
- BSC: 0x09CE0e021195BA2c1CDE62A8B187abf810951540
- Polygon: 0x09CE0e021195BA2c1CDE62A8B187abf810951540
- KCC: 0x7DBe94A4D6530F411A1E7337c7eb84185c4396e6

##### test
- ETH_rinkeby: 0xc08e6a853241b9a08225eecf93f3b279fa7a1be7
- BSC: 0xF2f9E62f52389EF223f5Fa8b9926e95386935277

[Smart Contract](https://github.com/NEST-Protocol/NEST-Oracle-V4.0/blob/main/contracts/NestBatchPlatform2.sol)

#### Get the Latest Triggered Price

Get the latest trigger price.The NEST price is a weighted average of all prices in the same block.New quotes and close operations trigger the calculation of prices that are already in effect earlier, while volatility and historical average prices are calculated.

```
function triggeredPrice(
    uint channelId,
    uint[] calldata pairIndices,
    address payback
) external payable returns (uint[] memory prices);
```
|input|type|instruction|
|---|---|---|
|channelId|uint|Target channelId|
|pairIndices|uint[]|Array of pair indices|
|payback|address|Address to receive refund|

|output|type|instruction|
|---|---|---|
|prices|uint[]|Price array, i \* 2 is the block where the ith price is located, and i \* 2 + 1 is the ith price|

[Lastest Triggered Price Off-chain Reading](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)(Contract CANNOT Use)

![image1](https://raw.githubusercontent.com/NEST-Protocol/NEST-Docs/main/Image/NEST1.png)

> In block 14802456, 2000USDT = 0.069274BTC

#### Get the Full Information of Latest Triggered Price

Get the latest departure price and average price volatility information.

```
function triggeredPriceInfo(
    uint channelId, 
    uint[] calldata pairIndices,
    address payback
) external payable returns (uint[] memory prices);
```
|input|type|instruction|
|---|---|---|
|channelId|uint|Target channelId|
|pairIndices|uint[]|Array of pair indices|
|payback|address|Address to receive refund|

|output|type|instruction|
|---|---|---|
|prices|uint[]|Price array, i \* 4 is the block where the ith price is located, i \* 4 + 1 is the ith price, i \* 4 + 2 is the ith average price and i \* 4 + 3 is the ith volatility|

[Lastest Triggered Price and Volatility Off-chain Reading](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)(Contract CANNOT Use)

![image2](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST2.png?raw=true)

> In block 14802456, 2000USDT=0.069274BTC, average price:2000USDT=0.069118234324991232BTC, volatility:17065492130

#### Find the Price at Block Number

Find the price in effect on the target historical block, or if there is no offer on the target block, go forward and find the most recent price in effect.

```
function findPrice(
    uint channelId,
    uint[] calldata pairIndices, 
    uint height, 
    address payback
) external payable returns (uint[] memory prices);
```
|input|type|instruction|
|---|---|---|
|channelId|uint|Target channelId|
|pairIndices|uint[]|Array of pair indices|
|height|uint|Destination block number|
|payback|address|Address to receive refund|

|output|type|instruction|
|---|---|---|
|prices|uint[]|Price array, i \* 2 is the block where the ith price is located, and i \* 2 + 1 is the ith price|

[Find Price Off-chain Reading](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)(Contract CANNOT Use)

![image3](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST3.png?raw=true)

> In block 14802456, 2000USDT = 0.069274BTC

#### Get the Lastest Count of Effective Prices

Get the latest count of effective prices.

```
function lastPriceList(
    uint channelId, 
    uint[] calldata pairIndices, 
    uint count, 
    address payback
) external payable returns (uint[] memory prices);
```
|input|type|instruction|
|---|---|---|
|channelId|uint|Target channelId|
|pairIndices|uint[]|Array of pair indices|
|count|uint|The number of prices that want to return|
|payback|address|Address to receive refund|

|output|type|instruction|
|---|---|---|
|prices|uint[]|Result array, i \* count \* 2 to (i + 1) \* count \* 2 - 1 are the price results of group i quotation pairs|

[Last Price Off-chain Reading](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)(Contract CANNOT Use)

![image4](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST4.png?raw=true)

> Read the latest 3 price information (BTC)

#### Return LastPriceList and Triggered Price Info

Return both the lastPriceList and the triggeredPriceInfo interfaces.

```
function lastPriceListAndTriggeredPriceInfo(
    uint channelId, 
    uint[] calldata pairIndices,
    uint count, 
    address payback
) external payable returns (uint[] memory prices);
```
|input|type|instruction|
|---|---|---|
|channelId|uint|Target channelId|
|pairIndices|uint[]|Array of pair indices|
|count|uint|The number of prices that want to return|
|payback|address|Address to receive refund|

|output|type|instruction|
|---|---|---|
|prices|uint[]|Result of group i quotation pair. Among them, the first two count are the latest prices, and the last four are: triggered price block number, triggered price, average price and volatility|

[Last Price and Triggered Price Off-chain Reading](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)(Contract CANNOT Use)

![image5](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST5.png?raw=true)

> Read the latest 3 price information (BTC),average price,volatility


### Example: Price Call

The example environment is the ethereum rinkeby test network.

- Contract:0xc08e6a853241b9a08225eecf93f3b279fa7a1be7
- ChannelId:0
- Fee:0

|Token|Address|PairIndex|
|---|---|---|
|HBTC|0xaE73d363Cb4aC97734E07e48B01D0a1FF5D1190B|0|
|ETH|0x0000000000000000000000000000000000000000|1|
|NEST|0xE313F3f49B647fBEDDC5F2389Edb5c93CBf4EE25|2|

#### About ChannelId and PairIndex

Anyone can open a channel and make a quote on it. A channel can contain multiple price pairs (they all have the same currency unit of denomination). It is similar to a two-dimensional arrays that locates the price to be queried by channelId and pairIndex.

#### About the Price Call Fee
Each call to the price method needs to carry a call fee, which is allocated by the administrator of the quote channel.Current fee is 0.

|Network|Fee|
|---|---|
|Ethereum|0ETH|
|BSC|0BNB|
|polygon|0MATIC|
|KCC|0KCS|

#### Triggered Price and Last Price

Triggered Price may be delayed by one price compared to lastPrice. In most cases, they are the same. It depends on the offer density.
Triggered Price requires less gas consumption, lastPrice must have the latest price, but has higher gas consumption.

![image7](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST7.png?raw=true)

#### Price Token and Price Token Unit

All prices in the documentation are in 2000 USDT, which is not fixed. Each channel has its own Price token and Price token unit, please check it before calling.

[Channel Information Website](https://channel.nestprotocol.org/)

[Read Channel Information from the Contract](https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract)

![image6](https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST6.png?raw=true)

#### Web Display Prices

web shows 1 ETH = 2500 USDT, get ETH price data as 800000000000000000(decimals 18), which means 2000 USDT = 0.8 ETH. Web converted to show.

#### Examples:
##### Use Instant Price

```
    // Query latest 2 price
    function _lastPriceList(
        TokenConfig memory tokenConfig, 
        uint fee, 
        address payback
    ) internal returns (uint[] memory prices) {

        // -----GET NEST PRICE-----
        prices = INestBatchPrice2(NEST_OPEN_PRICE).lastPriceList {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), 2, payback);
        // -----GET NEST PRICE-----

        prices[1] = _toUSDTPrice(prices[1]);
        prices[3] = _toUSDTPrice(prices[3]);
    }

    // Query latest price
    function _latestPrice(
        TokenConfig memory tokenConfig, 
        uint fee, 
        address payback
    ) internal returns (uint oraclePrice) {

        // -----GET NEST PRICE-----
        uint[] memory prices = INestBatchPrice2(NEST_OPEN_PRICE).lastPriceList {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), 1, payback);
        // -----GET NEST PRICE-----

        oraclePrice = _toUSDTPrice(prices[1]);
    }

    // Find price by blockNumber
    function _findPrice(
        TokenConfig memory tokenConfig, 
        uint blockNumber, 
        uint fee, 
        address payback
    ) internal returns (uint oraclePrice) {

        // -----GET NEST PRICE-----
        uint[] memory prices = INestBatchPrice2(NEST_OPEN_PRICE).findPrice {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), blockNumber, payback);
        // -----GET NEST PRICE-----

        oraclePrice = _toUSDTPrice(prices[1]);
    }
```

##### Use the Average Price

```
    /// @dev Get price
    /// @param token mortgage asset address
    /// @param uToken underlying asset address
    /// @param payback return address of excess fee
    /// @return tokenPrice Mortgage asset price(2000U = ? token)
    /// @return pTokenPrice PToken price(2000U = ? pToken)
    function getPriceForPToken(
        address token, 
        address uToken,
        address payback
    ) public payable override returns (
        uint256 tokenPrice, 
        uint256 pTokenPrice
    ) {
        if(uToken == address(USDT_ADDRESS)) {
            uint256[] memory pricesIndex = new uint256[](1);
            pricesIndex[0] = addressToPriceIndex[token];

            // -----GET NEST PRICE-----
            uint256[] memory prices = _nestBatchPlatform.triggeredPriceInfo{value:msg.value}(CHANNELID, pricesIndex, payback);
            // -----GET NEST PRICE-----

            require(prices[2] > 0, "Log:PriceController:!avg");
            return(prices[2], BASE_USDT_AMOUNT);
        } else {
            uint256[] memory pricesIndex = new uint256[](2);
            pricesIndex[0] = addressToPriceIndex[token];
            pricesIndex[1] = addressToPriceIndex[uToken];

            // -----GET NEST PRICE-----
            uint256[] memory prices = _nestBatchPlatform.triggeredPriceInfo{value:msg.value}(CHANNELID, pricesIndex, payback);
            // -----GET NEST PRICE-----

            require(prices[2] > 0 && prices[6] > 0, "Log:PriceController:!avg");
            return(prices[2], prices[6]);
        }
    }
```

##### Preventing Drastic Price Fluctuations

Market prices sometimes fluctuate too much, and there are some precautions to take when using prices, such as: comparing the deviation of the instant price with the average price, and not continuing to trade if it is too large.

```
    /// @dev Query latest price info
    /// @param tokenAddress Target address of token
    /// @param payback As the charging fee may change, it is suggested that the caller pay more fees, 
    /// and the excess fees will be returned through this address
    /// @return blockNumber Block number of price
    /// @return priceEthAmount Oracle price - eth amount
    /// @return priceTokenAmount Oracle price - token amount
    /// @return avgPriceEthAmount Avg price - eth amount
    /// @return avgPriceTokenAmount Avg price - token amount
    /// @return sigmaSQ The square of the volatility (18 decimal places)
    function latestPriceInfo(address tokenAddress, address payback) 
    external 
    payable 
    override
    returns (
        uint blockNumber, 
        uint priceEthAmount,
        uint priceTokenAmount,
        uint avgPriceEthAmount,
        uint avgPriceTokenAmount,
        uint sigmaSQ
    ) {

        // -----GET NEST PRICE-----
        (
            blockNumber, 
            priceTokenAmount,
            ,//uint triggeredPriceBlockNumber,
            ,//uint triggeredPriceValue,
            avgPriceTokenAmount,
            sigmaSQ
        ) = INestPriceFacade(NEST_PRICE_FACADE).latestPriceAndTriggeredPriceInfo { 
            value: msg.value 
        } (tokenAddress, payback);
        // -----GET NEST PRICE-----
        
        _checkPrice(priceTokenAmount, avgPriceTokenAmount);
        priceEthAmount = 1 ether;
        avgPriceEthAmount = 1 ether;
    }
```
