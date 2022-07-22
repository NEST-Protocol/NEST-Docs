## NEST Probability Virtual Machine(PVM)

### Introduction
NEST Probability Virtual Machine (PVM) is a virtual machine-like structure based on the basic function library. Developers can develop various exciting applications based on the function library, similar to Ethereum virtual machine (EVM) programming.

NEST inherited the genes of Ethereum. The essence of EVM is that each program is a combination of some basic codes, which can be called as long as a certain gas fee is paid. The income of each product on the PVM can be regarded as a linear combination of some basic income functions, and this income can be obtained as long as a certain cost (that is, the discounted value of this income) is paid. The underlying logic of PVM is the same as that of EVM, which means that all EVM development can be implemented on PVM.

Check the PVM's [whitepaper](https://finance.nestprotocol.org/The_White_Paper_of_NEST_PVM.pdf) for more details.

### Future

Use PVM's futures contracts to buy, sell and settle the futures.

#### Buy Future
```
    function buy(
        address tokenAddress,
        uint lever,
        bool orientation,
        uint nestAmount
    ) external payable override
```

|input|type|instruction|
|---|---|---|
|tokenAddress|address|Target token address, 0 means eth|
|lever|uint|Lever of future|
|orientation|bool|true: call, false: put|
|nestAmount|uint|Amount of paid NEST|

#### Sell Future

```
    function sell(uint index, uint amount) external payable override
```

|input|type|instruction|
|---|---|---|
|index|uint|Index of future|
|amount|uint|Amount to sell|

#### Settle Future

```
    function settle(uint index, address[] calldata addresses) external payable override
```
|input|type|instruction|
|---|---|---|
|index|uint|Index of future|
|addresses|address[]|Target addresses|


#### Get Information of Future
Future index contains a multiplier information and a call or put information.

```
    function getFutureInfo(
        address tokenAddress, 
        uint lever,
        bool orientation
    ) external view override returns (FutureView memory)
```

|input|type|instruction|
|---|---|---|
|tokenAddress|address|Target token address, 0 means eth|
|lever|uint|Lever of future|
|orientation|bool|true: call, false: put|

|output|type|instruction|
|---|---|---|
|index|uint|future index|
|tokenAddress|address|Target token address, 0 means eth|
|lever|uint|Lever of future|
|orientation|bool|true: call, false: put|

### Option

Use PVM's option contracts to open, exercise and sell the options.

#### Open Option

```
    function open(
        address tokenAddress,
        uint strikePrice,
        bool orientation,
        uint exerciseBlock,
        uint nestAmount
    ) external payable override
```

|input|type|instruction|
|---|---|---|
|tokenAddress|address|Target token address, 0 means eth|
|strikePrice|uint|The exercise price set by the user. During settlement, the system will compare the current price of the subject matter with the exercise price to calculate the user's profit and loss|
|orientation|bool|true: call, false: put|
|exerciseBlock|uint|After reaching this block, the user will exercise manually, and the block will be recorded in the system using the block number|
|nestAmount|uint|Amount of paid NEST|

#### Exercise Option

```
    function exercise(uint index, uint amount) external payable override
```

|input|type|instruction|
|---|---|---|
|index|uint|Index of option|
|amount|uint|Amount of option to exercise|

#### Sell Option

```
    function sell(uint index, uint amount) external payable override
```

|input|type|instruction|
|---|---|---|
|index|uint|Index of option|
|amount|uint|Amount of option to exercise|

#### Find the Owner of the Options (Desc)

```
    function find(
        uint start, 
        uint count, 
        uint maxFindCount, 
        address owner
    ) external view override returns (OptionView[] memory optionArray)
```

|input|type|instruction|
|---|---|---|
|start|uint|Find forward from the index corresponding to the given owner address (excluding the record corresponding to start)|
|count|uint|Maximum number of records returned|
|maxFindCount|uint|Find records at most|
|owner|address|Target address|

|output|type|instruction|
|---|---|---|
|index|uint|option index|
|tokenAddress|address|Target token address, 0 means eth|
|strikePrice|uint|The exercise price set by the user. During settlement, the system will compare the current price of the subject matter with the exercise price to calculate the user's profit and loss|
|orientation|bool|true: call, false: put|
|exerciseBlock|uint|After reaching this block, the user will exercise manually, and the block will be recorded in the system using the block number|
|balance|uint|option shares|
|owner|address|Target address|

### Roll

Play with NEST token to win more NEST for calling Roll contract.

#### Start a Roll

```
    function roll44(uint n, uint m) external override
```

|input|type|instruction|
|---|---|---|
|n|uint|count of NEST|
|m|uint|times, 4 decimals|

#### Claim NEST

```
    function claim44(uint index) external override
```

|input|type|instruction|
|---|---|---|
|index|uint|index of bet|

#### Find the Information of the Target Address (Desc)

```
    function find44(
        uint start, 
        uint count, 
        uint maxFindCount, 
        address owner
    ) external view override returns (DiceView44[] memory diceArray44)
```

|input|type|instruction|
|---|---|---|
|start|uint|Find forward from the index corresponding to the given contract address (excluding the record corresponding to start)|
|count|uint|Maximum number of records returned|
|maxFindCount|uint|Find records at most|
|owner|address|Target address|

|output|type|instruction|
|---|---|---|
|index|uint|bet index|
|owner|address|Target address|
|n|uint32|count of NEST|
|m|uint32|times, 4 decimals|
|openBlock|uint32|the block number of bet when opened|
|gained|uint|gained number of NEST|
