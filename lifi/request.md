# 📜Request Routes/Quotes

Prior to executing any swap or bridging, you need to request the best route from our smart routing API.

The LI.FI SDK provides functionality to request routes and quotes, as well as to execute them. This guide will walk you through the process of making a request using `getRoutes` and `getQuote` functions.

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#how-to-request-routes)

How to request Routes

To get started, here is a simple example of how to request routes to bridge and swap 10 USDC on Arbitrum to the maximum amount of DAI on Optimism.

Copy

```
import { getRoutes } from '@lifi/sdk';

const routesRequest: RoutesRequest = {
  fromChainId: 42161, // Arbitrum
  toChainId: 10, // Optimism
  fromTokenAddress: '0xaf88d065e77c8cC2239327C5EDb3A432268e5831', // USDC on Arbitrum
  toTokenAddress: '0xDA10009cBd5D07dd0CeCc66161FC93D7c9000da1', // DAI on Optimism
  fromAmount: '10000000', // 10 USDC
};

const result = await getRoutes(routesRequest);
const routes = result.routes;
```

When you request routes, you receive an array of route objects containing the essential information to determine which route to take for a swap or bridging transfer. At this stage, transaction data is not included and must be requested separately. Read more [Execute Routes/Quotes](https://docs.li.fi/integrate-li.fi-sdk/execute-routes-quotes).

Additionally, if you would like to receive just one best option that our smart routing API can offer, it might be better to request a quote using `getQuote`. See [Request a Quote](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#request-a-quote) section.

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#routes-request-parameters)

Routes request parameters

The `getRoutes` function expects a `RoutesRequest` object, which specifies a desired _any-to-any_ transfer and includes all the information needed to calculate the most efficient routes.

### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#parameters)

Parameters

Below are the parameters for the `RoutesRequest` interface along with their descriptions:

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromchainid-number-required)

`**fromChainId**` (number, required)

The ID of the source chain (e.g., Ethereum mainnet is 1).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromtokenaddress-string-required)

`**fromTokenAddress**` (string, required)

The contract address of the token on the source chain. Ensure this address corresponds to the specified `fromChainId`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromamount-string-required)

`**fromAmount**` (string, required)

The amount to be transferred from the source chain, specified in the smallest unit of the token (e.g., wei for ETH).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromaddress-string-optional)

`**fromAddress**` (string, optional)

The address from which the tokens are being transferred.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#tochainid-number-required)

`**toChainId**` (number, required)

The ID of the destination chain (e.g., Optimism is 10).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#totokenaddress-string-required)

`**toTokenAddress**` (string, required)

The contract address of the token on the destination chain. Ensure this address corresponds to the specified `toChainId`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#toaddress-string-optional)

`**toAddress**` (string, optional)

The address to which the tokens will be sent on the destination chain once the transaction is completed.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromamountforgas-string-optional)

`**fromAmountForGas**` (string, optional)

Part of the [LI.Fuel](https://docs.li.fi/li.fi-api/li.fuel). Allows receiving a part of the bridged tokens as gas on the destination chain. Specified in the smallest unit of the token.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#options-routeoptions-optional)

`**options**` (RouteOptions, optional)

Additional options for customizing the route. This is defined by the `RouteOptions` interface (detailed below, see [Route Options](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#route-options)).

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#route-options)

Route Options

The `RouteOptions` interface allows for further customization of the route request. Below are the parameters for the `RouteOptions` interface along with their descriptions:

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#integrator-string-optional)

`**integrator**` (string, optional)

The identifier of the integrator, usually the dApp or company name. Ideally, this should be specified when configuring the SDK, but it can also be modified during a request. See [Configure SDK](https://docs.li.fi/integrate-li.fi-sdk/configure-sdk).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fee-number-optional)

`**fee**` (number, optional)

The integrator fee percentage (e.g., 0.03 represents a 3% fee). This requires the integrator to be verified.

As an integrator, you can monetize your LI.FI SDK integration and collect fees. See [Monetization / Take Fees](https://docs.li.fi/monetization-take-fees) for more information.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#maxpriceimpact-number-optional)

`**maxPriceImpact**` (number, optional)

Hides routes with a price impact greater than or equal to this value. (e.g., 0.3 represents 30%)

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#order-string-optional)

`**order**` (string, optional)

_Default_: `CHEAPEST`

The order preference for routes:

- `**CHEAPEST**`
    
    This sorting option prioritises routes with the highest estimated return amount. Users who value capital efficiency at the expense of speed and route complexity should choose the cheapest routes.
    
- `**FASTEST**`
    
    This sorting option prioritizes routes with the shortest estimated execution time. Users who value speed and want their transactions to be completed as quickly as possible should choose the fastest routes.
    

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#slippage-number-optional)

`**slippage**` (number, optional)

_Default_: `0.005`

The slippage tolerance, expressed as a decimal proportion (e.g., 0.005 represents 0.5%).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#referrer-string-optional)

`**referrer**` (string, optional)

The wallet address of the referrer, for tracking purposes.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#allowswitchchain-boolean-optional)

`**allowSwitchChain**` (boolean, optional)

_Default_: `false`

Specifies whether to return routes that require chain switches (2-step routes).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#allowdestinationcall-boolean-optional)

`**allowDestinationCall**` (boolean, optional)

_Default_: `true`

Specifies whether destination calls are enabled.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#bridges-allowdenyprefer-optional)

`**bridges**` (AllowDenyPrefer, optional)

An `AllowDenyPrefer` object to specify preferences for bridges.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#exchanges-allowdenyprefer-optional)

`**exchanges**` (AllowDenyPrefer, optional)

An `AllowDenyPrefer` object to specify preferences for exchanges.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#timing-timing-optional)

**timing** (Timing, optional)

A `Timing` object to specify preferences for [Timing Strategies](https://docs.li.fi/li.fi-api/li.fi-api/requesting-a-quote/optimizing-quote-response-timing).

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#allow-deny-prefer)

Allow/Deny/Prefer

The `AllowDenyPrefer` interface is used to specify preferences for bridges or exchanges. Using the `allow` option, you can allow tools, and only those tools will be used to find the best routes. Tools specified in `deny` will be blocklisted.

You can find all available keys in [List: Chains, Bridges, DEX Aggregators, Solvers](https://docs.li.fi/list-chains-bridges-dex-aggregators-solvers) or get the available option from the API. See [Chains and Tools](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools).

Below are the parameters for the `AllowDenyPrefer` interface:

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#allow-string-optional)

`**allow**` (string[], optional)

A list of allowed bridges or exchanges (default: all).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#deny-string-optional)

`**deny**` (string[], optional)

A list of denied bridges or exchanges (default: none).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#prefer-string-optional)

`**prefer**` (string[], optional)

A list of preferred bridges or exchanges (e.g., `['1inch']` to prefer 1inch if available).

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#timing)

Timing

The `Timing` interface allows you to specify preferences for the timing of route execution. This can help optimize the performance of your requests based on timing strategies.

Parameters for the `Timing` interface:

- `**swapStepTimingStrategies**` **(TimingStrategy[], optional)** An array of timing strategies specifically for each swap step in the route. This allows you to define custom strategies for timing control during the execution of individual swap steps.
    
- `**routeTimingStrategies**` **(TimingStrategy[], optional)** An array of timing strategies that apply to the entire route. This enables you to set preferences for how routes are timed overall, potentially improving execution efficiency and reliability.
    

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#timing-strategy)

Timing Strategy

This can help optimize the timing of requests based on specific conditions.

Parameters:

- `**strategy**` **(string)** The strategy type, which must be set to `'minWaitTime'`. This indicates that the timing strategy being applied is based on a minimum wait time.
    
- `**minWaitTimeMs**` **(number)** The minimum wait time in milliseconds before any results are returned. This value ensures that the request waits for a specified duration to allow for more accurate results.
    
- `**startingExpectedResults**` **(number)** The initial number of expected results that should be returned after the minimum wait time has elapsed. This helps in managing user expectations regarding the outcomes of the request.
    
- `**reduceEveryMs**` **(number)** The interval in milliseconds at which the expected results are reduced as the wait time progresses. This parameter allows for dynamic adjustments to the expected results based on the elapsed time.
    

You can implement [custom timing strategies](https://docs.li.fi/li.fi-api/li.fi-api/requesting-a-quote/optimizing-quote-response-timing) to improve the user experience and optimize the performance of your application by controlling the timing of route execution.

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#request-a-quote)

Request a Quote

When you request a quote, our smart routing API provides the best available option. The quote includes all necessary information and transaction data required to initiate a swap or bridging transfer.

Here is a simple example of how to request a quote to bridge and swap 10 USDC on Arbitrum to the maximum amount of DAI on Optimism.

Copy

```
import { getQuote } from '@lifi/sdk';

const quoteRequest: QuoteRequest = {
  fromChain: 42161, // Arbitrum
  toChain: 10, // Optimism
  fromToken: '0xaf88d065e77c8cC2239327C5EDb3A432268e5831', // USDC on Arbitrum
  toToken: '0xDA10009cBd5D07dd0CeCc66161FC93D7c9000da1', // DAI on Optimism
  fromAmount: '10000000', // 10 USDC
  // The address from which the tokens are being transferred.
  fromAddress: '0x552008c0f6870c2f77e5cC1d2eb9bdff03e30Ea0', 
};

const quote = await getQuote(quoteRequest);
```

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#quote-request-parameters)

Quote request parameters

The `getQuotes` function expects a `QuoteRequest` object. `RoutesRequest` and `QuoteRequest` have some similarities and slight differences, and below, you can find a description of the `QuoteRequest` interface's parameters.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromchain-number-required)

`**fromChain**` (number, required)

The ID of the source chain (e.g., Ethereum mainnet is 1).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromtoken-string-required)

`**fromToken**` (string, required)

The contract address of the token on the source chain. Ensure this address corresponds to the specified `fromChain`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromamount-string-required-1)

`**fromAmount**` (string, required)

The amount to be transferred from the source chain, specified in the smallest unit of the token (e.g., wei for ETH).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromaddress-string-required)

`**fromAddress**` (string, required)

The address from which the tokens are being transferred.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#tochain-number-required)

`**toChain**` (number, required)

The ID of the destination chain (e.g., Optimism is 10).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#totoken-string-required)

`**toToken**` (string, required)

The contract address of the token on the destination chain. Ensure this address corresponds to the specified `toChain`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#toaddress-string-optional-1)

`**toAddress**` (string, optional)

The address to which the tokens will be sent on the destination chain once the transaction is completed.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromamountforgas-string-optional-1)

`**fromAmountForGas**` (string, optional)

Part of the [LI.Fuel](https://docs.li.fi/li.fi-api/li.fuel). Allows receiving a part of the bridged tokens as gas on the destination chain. Specified in the smallest unit of the token.

### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#other-quote-parameters)

Other Quote parameters

In addition to the parameters mentioned above, all parameters listed in the[Route Options](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#route-options) section are also available when using `getQuote`, except for `allowSwitchChain`, which is used exclusively to control chain switching in route requests.

Also, parameters to specify options for allowing, denying, or preferring certain bridges and exchanges have slightly different names:

- `allowBridges` (string[], optional)
    
- `denyBridges` (string[], optional)
    
- `preferBridges` (string[], optional)
    
- `allowExchanges` (string[], optional)
    
- `denyExchanges` (string[], optional)
    
- `preferExchanges` (string[], optional)
    

Additionally, you can specify [timing strategies](https://docs.li.fi/li.fi-api/li.fi-api/requesting-a-quote/optimizing-quote-response-timing#parameters-overview) for the swap steps using the `swapStepTimingStrategies` parameter:

- **swapStepTimingStrategies** (string[], optional) Specifies the timing strategy for swap steps. This parameter allows you to define how long the request should wait for results and manage expected outcomes. The format is:
    
    Copy
    
    ```
    minWaitTime-${minWaitTimeMs}-${startingExpectedResults}-${reduceEveryMs}
    ```
    

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#request-contract-call-quote)

Request contract call Quote

Besides requesting general quotes, the LI.FI SDK also provides functionality to request quotes for destination contract calls.

Read more [TX-Batching aka "Zaps"](https://docs.li.fi/li.fi-api/tx-batching-aka-zaps).

Here is a simple example of how to request a quote to bridge and purchase an NFT on the OpenSea marketplace costing 0.0000085 ETH on the Base chain using ETH from Optimism. The call data for this example was obtained using the OpenSea Seaport SDK.

Copy

```
import { getContractCallsQuote } from '@lifi/sdk';

const contractCallsQuoteRequest = {
  fromAddress: '0x552008c0f6870c2f77e5cC1d2eb9bdff03e30Ea0',
  fromChain: 10,
  fromToken: '0x0000000000000000000000000000000000000000',
  toAmount: '8500000000000',
  toChain: 8453,
  toToken: '0x0000000000000000000000000000000000000000',
  contractCalls: [
    {
      fromAmount: '8500000000000',
      fromTokenAddress: '0x0000000000000000000000000000000000000000',
      toContractAddress: '0x0000000000000068F116a894984e2DB1123eB395',
      toContractCallData:
        '0xe7acab24000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000006e0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000029dacdf7ccadf4ee67c923b4c22255a4b2494ed700000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000520000000000000000000000000000000000000000000000000000000000000064000000000000000000000000090884b5bd9f774ed96f941be2fb95d56a029c99c00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000160000000000000000000000000000000000000000000000000000000000000022000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000066757dd300000000000000000000000000000000000000000000000000000000669d0a580000000000000000000000000000000000000000000000000000000000000000360c6ebe0000000000000000000000000000000000000000ad0303de3e1093e50000007b02230091a7ed01230072f7006a004d60a8d4e71d599b8104250f000000000000000000000000000000000000000000000000000000000000000000030000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000200000000000000000000000029f25e8a71e52e795e5016edf7c9e02a08c519b40000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000006ff0cbadd00000000000000000000000000000000000000000000000000000006ff0cbadd0000000000000000000000000090884b5bd9f774ed96f941be2fb95d56a029c99c0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000003179fcad000000000000000000000000000000000000000000000000000000003179fcad000000000000000000000000000000a26b00c1f0df003000390027140000faa7190000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008a88c37e000000000000000000000000000000000000000000000000000000008a88c37e000000000000000000000000009323bb21a4c6122f60713e4a1e38e7b94a40ce2900000000000000000000000000000000000000000000000000000000000000e3b5b41791fe051471fa3c2da1325a8147c833ad9a6609ffc07a37e2603de3111b262911aaf25ed6d131dd531574cf54d4ea61b479f2b5aaa2dff7c210a3d4e203000000f37ec094486e9092b82287d7ae66fbf8cd6148233c70813583e3264383afbd0484b80500070135f54edd2918ddd4260c840f8a6957160766a4e4ef941517f2a0ab3077a2ac6478f0ad7fad9b821766df11ca3fdb16a8e95782faaed6e0395df2f416651ac87a5c1edec0a36ad42555083e57cff59f4ad98617a48a3664b2f19d46f4db85e95271c747d03194b5cfdcfc86bb0b08fb2bc4936d6f75be03ab498d000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000',
      toContractGasLimit: '210000',
    },
  ],
};

const contractCallQuote = await getContractCallsQuote(contractCallsQuoteRequest);
```

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#contract-call-quote-request-parameters)

Contract call Quote request parameters

The `getContractCallsQuote` function expects a `ContractCallsQuoteRequest` object, which includes all the information needed to request a quote for a destination contract call.

Contract call quote request can be treated as an extension to the quote request and in addition to the parameters mentioned below, all parameters listed in the [Other Quote parameters](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#other-quote-parameters) section (such as `integrator`, `fee`, `slippage`, etc.) are also available when using `getContractCallsQuote`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromchain-number-required-1)

`**fromChain**` (number, required)

The ID of the source chain (e.g., Ethereum mainnet is 1).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromtoken-string-required-1)

`**fromToken**` (string, required)

The contract address of the token on the source chain. Ensure this address corresponds to the specified `fromChain`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#fromaddress-string-required-1)

`**fromAddress**` (string, required)

The address from which the tokens are being transferred.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#tochain-number-required-1)

`**toChain**` (number, required)

The ID of the destination chain (e.g., Optimism is 10).

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#totoken-string-required-1)

`**toToken**` (string, required)

The token required to perform the contract interaction (can be something to stake, donate, or to be used as payment). Ensure this address corresponds to the specified `toChain`.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#toamount-string-required)

`toAmount` (string, required)

The amount of tokens required by the contract interaction. The LI.FI API will try and generate a quote that guarantees at least that amount on the destination chain.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#tofallbackaddress-string-optional)

`toFallbackAddress` (string, optional)

The address to send the bridged tokens to if the call fails. Defaults to the sending address if not specified.

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#contractcalls-contractcall-required)

`contractCalls` (ContractCall[], required)

Array of contract call objects.

- `fromAmount` (string, required): The amount of tokens to be sent to the contract. This amount is independent of any previously bridged or deposited tokens.
    
- `fromTokenAddress` (string, required): The address of the token to be sent to the contract. For example, an ETH staking transaction would require ETH.
    
- `toContractAddress` (string, required): The address of the contract to interact with on the destination chain.
    
- `toContractCallData` (string, required): The call data to be sent to the contract for the interaction on the destination chain.
    
- `toContractGasLimit` (string, required): The estimated gas required for the contract call. Incorrect values may cause the interaction to fail.
    
- `toApprovalAddress` (string, optional): The address to approve the token transfer if it is different from the contract address.
    
- `toTokenAddress` (string, optional): The address of the token that will be output by the contract, if applicable (e.g., staking ETH produces stETH).
    

#### 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#contractoutputstoken-string-optional)

`contractOutputsToken` (string, optional)

The token address that will be output by the contract, if applicable. Omit if no token should be returned.

## 

[](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes#difference-between-route-and-quote)

Difference between `Route` and `Quote`

Even though `Route` and `Quote` terms lie in the same field of providing you with the best option to make a swap or bridging transfer, there are some differences you need to be aware of.

A `Route` in LI.FI represents a detailed transfer plan that may include _multiple steps_. Each step corresponds to an individual transaction, such as swapping tokens or bridging funds between chains. These steps must be executed in a specific sequence, as each one depends on the output of the previous step. A `Route` provides a detailed pathway for complex transfers involving multiple actions.

In contrast, a `Quote` is a _single-step_ transaction. It contains all the necessary information to perform a transfer in one go, without requiring any additional steps. `Quotes` are used for simpler transactions where a single action, such as a token swap or a cross-chain transfer, is sufficient. Thus, while `Routes` can involve multiple steps to complete a transfer, a `Quote` always represents just one step.

Read more [LI.FI Terminology](https://docs.li.fi/overview/li.fi-terminology).