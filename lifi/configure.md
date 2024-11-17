# ⚙️Configure SDK

Get started and set up LI.FI SDK in just a few lines of code.

## Create config

To get started, you need to create an initial configuration for the LI.FI SDK. This configuration contains the shared settings and data required for the proper functioning of other SDK features that developers will use. Additionally, the configuration can be updated later as needed.

```
import { createConfig } from '@lifi/sdk'

createConfig({
  integrator: 'Your dApp/company name',
})
```

### Parameters

`integrator` (string, required)

LI.FI SDK requires an `integrator` option to identify partners and allows them to monitor their activity on the partner dashboard, such as the transaction volume, enabling better management and support.

Usually, the integrator option is your dApp or company name.

This string must consist only of letters, numbers, hyphens, underscores, and dots and be a maximum of 23 characters long.

`apiKey` (string, optional)

Unique API key for accessing LI.FI API services. Necessary for higher rate limits. Read more [Rate Limits & API Key](https://docs.li.fi/rate-limits-and-api-key)

`apiUrl` (string, optional)

_Default_: `https://li.quest/v1`

The base URL for the LI.FI API. This is the endpoint through which all API requests are routed. It can be changed to the staging environment to test new features, for example.

If you are interested in a dedicated API endpoint for your service, reach out via our [Discord](https://discord.gg/lifi) or file an issue in our repository [here](https://github.com/lifinance/sdk).

`userId` (string, optional)

A unique identifier for the user of your application. This can be used to track user-specific data and interactions within the LI.FI.

`routeOptions` (RouteOptions, optional)

Custom options for routing, applied when using `getQuote`, `getRoutes`, and `getContractCallsQuote` endpoints. These options can be configured once during SDK initialization or passed each time those functions are called. Read more [Request Routes/Quotes](https://docs.li.fi/integrate-li.fi-sdk/request-routes-quotes)

`rpcUrls` (RPCUrls, optional)

A mapping of chain IDs to arrays of RPC URLs. These URLs might be used for transaction execution and data retrieval.

```
import { createConfig, ChainId } from '@lifi/sdk'

createConfig({
  integrator: 'Your dApp/company name',
  rpcUrls: {
    [ChainId.ARB]: ['https://arbitrum-example.node.com/'],
    [ChainId.SOL]: ['https://solana-example.node.com/'],
  },
})
```

In a production app, it is recommended to pass through your authenticated RPC provider URL (Alchemy, Infura, Ankr, etc).

If no RPC URLs are provided, LI.FI SDK will default to public RPC providers.

`chains` (ExtendedChain[], optional)

_Default_: fetched from LI.FI API during initialization.

An array of chains that the SDK will support. Each chain must be configured with necessary details like chain ID, name, RPCs, etc. This information is used during the quote and route execution.

When `createConfig` is called, the SDK preloads available chains from the LI.FI API. Developers can disable chain preloading to specify the chains themselves.

`preloadChains` (boolean, optional)

_Default_: `true`

A flag indicating whether to preload chain configurations. By default, the SDK will load chain details during initialization.

`**disableVersionCheck**` (boolean, optional)

_Default_: `false`

A flag to disable version checking of the SDK. By default, the SDK checks its version on initialization and logs a message in the console if a new version is available, prompting the user to update the SDK.

`providers` (SDKProvider[], optional)

An array of provider configurations is used by the SDK. Providers are optional and only necessary if you plan to execute quotes or routes through the SDK. Read more [Configure SDK Providers](https://docs.li.fi/integrate-li.fi-sdk/configure-sdk-providers).

Setting up providers is not required if you are using the SDK solely to access the LI.FI API without quote/route SDK execution functionality and plan to handle the execution independently.

Read more [Configure SDK Providers](https://docs.li.fi/integrate-li.fi-sdk/configure-sdk-providers).

## Update SDK configuration

LI.FI SDK provides various methods to manage and manipulate the SDK settings dynamically. To update the configuration, you need to import the global configuration object and use its methods.

```
import { config } from '@lifi/sdk';
```

After creating your configuration with the `createConfig` function, `config` acts as a global configuration object.

### Configuration Methods

`get()`

Returns the current SDK configuration.

`set(options: SDKConfig)`

Sets the SDK configuration with the provided options.

`setProviders(providers: SDKProvider[])`

Sets the providers in the SDK configuration. If a provider already exists, it will be updated with the new information.

`getChains()`

Returns a promise that resolves to the list of configured chains. If the configuration is still loading, the promise will wait until the loading is complete.

`setChains(chains: ExtendedChain[])`

Sets the chains in the SDK configuration and updates chains RPC URLs. This method also clears the loading state.

`getChainById(chainId: ChainId)`

Returns a promise that resolves to the chain configuration for the specified chain ID. If the configuration is still loading, the promise will wait until the loading is complete.

`getRPCUrls()`

Returns a promise that resolves to the list of RPC URLs for the configured chains. If the configuration is still loading, the promise will wait until the loading is complete.

`setRPCUrls(rpcUrls: RPCUrls)`

Sets the RPC URLs for the chains in the SDK configuration. If some RPC URLs already exist for a chain, the new URLs will be appended to the existing ones.