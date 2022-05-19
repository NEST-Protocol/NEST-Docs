# Call Price

---

## Contract address

### mainnet
- ETH: 0xE544cF993C7d477C7ef8E91D28aCA250D135aa03
- BSC: 0x09CE0e021195BA2c1CDE62A8B187abf810951540
- Polygon: 0x09CE0e021195BA2c1CDE62A8B187abf810951540
- KCC: 0x7DBe94A4D6530F411A1E7337c7eb84185c4396e6

### test
- ETH_rinkeby: 0xc08e6a853241b9a08225eecf93f3b279fa7a1be7
- BSC: 0xF2f9E62f52389EF223f5Fa8b9926e95386935277


<a href="https://github.com/NEST-Protocol/NEST-Oracle-V4.0/blob/main/contracts/NestBatchPlatform2.sol" target="_blank">Smart contract</a>

## Request Price(for contract)

#### Get the latest trigger price

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

<a href="https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract" target="_blank">Off-chain reading(Prohibit contract use)</a>

<img src="https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST1.png?raw=true" alt="" style="max-width: 60%;">

> In block 14802456, 2000USDT = 0.069274BTC

#### Get the full information of latest trigger price
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

<a href="https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract" target="_blank">Off-chain reading(Prohibit contract use)</a>

<img src="https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST2.png?raw=true" alt="" style="max-width: 60%;">

> In block 14802456, 2000USDT=0.069274BTC, average price:2000USDT=0.069118234324991232BTC, volatility:17065492130

#### Find the price at block number
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

<a href="https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract" target="_blank">Off-chain reading(Prohibit contract use)</a>

<img src="https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST3.png?raw=true" alt="" style="max-width: 60%;">

> In block 14802456, 2000USDT = 0.069274BTC

#### Get the last (num) effective price
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

<a href="https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract" target="_blank">Off-chain reading(Prohibit contract use)</a>

<img src="https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST4.png?raw=true" alt="" style="max-width: 60%;">

> Read the latest 3 price information (BTC)

#### Returns lastPriceList and triggered price info
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
|prices|uint[]|Result of group i quotation pair. Among them, the first two count are the latest prices, and the last four are: trigger price block number, trigger price, average price and volatility|

<a href="https://etherscan.io/address/0xE544cF993C7d477C7ef8E91D28aCA250D135aa03#readProxyContract" target="_blank">Off-chain reading(Prohibit contract use)</a>

<img src="https://github.com/NEST-Protocol/NEST-Docs/raw/main/Image/NEST5.png?raw=true" alt="" style="max-width: 60%;">

> Read the latest 3 price information (BTC),average price,volatility

## About channelId and pairIndex

Anyone can open a channel and make a quote on it. A channel can contain multiple price pairs (they all have the same currency unit of denomination). It is similar to a two-dimensional arrays that locates the price to be queried by channelId and pairIndex.

## About the price call fee (for now)
Each call to the price method needs to carry a call fee, which is allocated by the administrator of the quote channel.Current fee is 0.

|Network|Fee|
|---|---|
|Ethereum|0ETH|
|BSC|0BNB|
|polygon|0MATIC|
|KCC|0KCS|

## TriggeredPrice and LastPrice

triggeredPrice may be delayed by one price compared to lastPrice. In most cases, they are the same. It depends on the offer density.
triggeredPrice requires less gas consumption, lastPrice must have the latest price, but has higher gas consumption.

## Call example

The example environment is the ethereum rinkeby test network.

- Contract:0xc08e6a853241b9a08225eecf93f3b279fa7a1be7
- ChannelId:0
- Fee:0

|Token|Address|PairIndex|
|---|---|---|
|HBTC|0xaE73d363Cb4aC97734E07e48B01D0a1FF5D1190B|0|
|ETH|0x0000000000000000000000000000000000000000|1|
|NEST|0xE313F3f49B647fBEDDC5F2389Edb5c93CBf4EE25|2|

### FORT:Use Instant Price

<a href="https://github.com/FORT-Protocol/FORT-V1.1/blob/main/contracts/custom/FortPriceAdapter.sol#L36" target="_blank">FORT Smart contract</a>

```
    // Query latest 2 price
    function _lastPriceList(
        TokenConfig memory tokenConfig, 
        uint fee, 
        address payback
    ) internal returns (uint[] memory prices) {
        prices = INestBatchPrice2(NEST_OPEN_PRICE).lastPriceList {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), 2, payback);

        prices[1] = _toUSDTPrice(prices[1]);
        prices[3] = _toUSDTPrice(prices[3]);
    }

    // Query latest price
    function _latestPrice(
        TokenConfig memory tokenConfig, 
        uint fee, 
        address payback
    ) internal returns (uint oraclePrice) {
        uint[] memory prices = INestBatchPrice2(NEST_OPEN_PRICE).lastPriceList {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), 1, payback);

        oraclePrice = _toUSDTPrice(prices[1]);
    }

    // Find price by blockNumber
    function _findPrice(
        TokenConfig memory tokenConfig, 
        uint blockNumber, 
        uint fee, 
        address payback
    ) internal returns (uint oraclePrice) {
        uint[] memory prices = INestBatchPrice2(NEST_OPEN_PRICE).findPrice {
            value: fee
        } (uint(tokenConfig.channelId), _pairIndices(uint(tokenConfig.pairIndex)), blockNumber, payback);

        oraclePrice = _toUSDTPrice(prices[1]);
    }
```

### Parasset:Use the average price

<a href="https://github.com/Parasset/ParassetV2-Protocol/blob/main/contracts/PriceController2.sol#L44" target="_blank">Parasset Smart contract</a>

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
            uint256[] memory prices = _nestBatchPlatform.triggeredPriceInfo{value:msg.value}(CHANNELID, pricesIndex, payback);
            require(prices[2] > 0, "Log:PriceController:!avg");
            return(prices[2], BASE_USDT_AMOUNT);
        } else {
            uint256[] memory pricesIndex = new uint256[](2);
            pricesIndex[0] = addressToPriceIndex[token];
            pricesIndex[1] = addressToPriceIndex[uToken];
            uint256[] memory prices = _nestBatchPlatform.triggeredPriceInfo{value:msg.value}(CHANNELID, pricesIndex, payback);
            require(prices[2] > 0 && prices[6] > 0, "Log:PriceController:!avg");
            return(prices[2], prices[6]);
        }
    }
```

### Preventing drastic price fluctuations

Market prices sometimes fluctuate too much, and there are some precautions to take when using prices, such as: comparing the deviation of the instant price with the average price, and not continuing to trade if it is too large.

<a href="https://github.com/Computable-Finance/CoFiX-V2.1/blob/nest4.0/contracts/CoFiXController.sol#L31" target="_blank">CoFix Smart contract</a>

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
        
        _checkPrice(priceTokenAmount, avgPriceTokenAmount);
        priceEthAmount = 1 ether;
        avgPriceEthAmount = 1 ether;
    }
```



