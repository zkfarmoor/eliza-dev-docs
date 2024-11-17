# Install LI.FI SDK

Integrate our LI.FI SDK to your dApp/Wallet/Swap UI

The LI.FI SDK package provides access to the LI.FI API to find and execute the best on-chain and cross-chain routes across various bridges and exchanges.

Our API is free to use but rate-limited.

Please see [Rate Limits & API Key](https://docs.li.fi/rate-limits-and-api-key) if you need more requests per second.

## Installation

To get started, install the latest version of LI.FI SDK.

```
pnpm add @lifi/sdk
```

Check out our complete examples in the [SDK repository](https://github.com/lifinance/sdk/tree/main/examples), and feel free to [file an issue](https://github.com/lifinance/sdk/issues) if you encounter any problems.

As an integrator, you can monetize your LI.FI SDK integration and collect fees. See our [**monetization guide**](https://docs.li.fi/monetization-take-fees) for more information.

Contact our [business partnerships team](https://docs.li.fi/overview/partnership) to discover how you can partner with us and integrate [LI.FI](https://li.fi/?utm_source=docs&utm_medium=lifi_sdk_installation_links&utm_campaign=docs_to_lifi) into your platform.

## Quick Start

### Set up the SDK

Firstly, create SDK config with your integrator string.

```
import { createConfig } from '@lifi/sdk'

createConfig({
  integrator: 'Your dApp/company name',
})
```

### Request a Quote

Now you can interact with the SDK and for example request a quote.

```
import { ChainId, getQuote } from '@lifi/sdk'

const quote = await getQuote({
  fromAddress: '0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045',
  fromChain: ChainId.ARB,
  toChain: ChainId.OPT,
  fromToken: '0x0000000000000000000000000000000000000000',
  toToken: '0x0000000000000000000000000000000000000000',
  fromAmount: '1000000000000000000',
})
```

You can learn more about the configuring the SDK in the next section.