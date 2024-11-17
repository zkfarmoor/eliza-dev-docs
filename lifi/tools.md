# ⛓️Chains and Tools

Request all available chains, bridges, and exchanges.

Get an overview of which options (chains, bridges, DEXs) are available at this moment.

## 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#get-available-chains)

Get available chains

### 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#getchains)

`getChains`

Fetches a list of all available chains supported by the SDK.

**Parameters**

- `params` (ChainsRequest, optional): Configuration for the requested chains.
    
    - `chainTypes` (ChainType[], optional): List of chain types.
        
    
- `options` (RequestOptions, optional): Additional request options.
    

**Returns**

A Promise that resolves to an array of `ExtendedChain` objects.

**Example**

Copy

```
import { ChainType, getChains } from '@lifi/sdk';

try {
  const chains = await getChains({ chainTypes: [ChainType.EVM] });
  console.log(chains);
} catch (error) {
  console.error(error);
}
```

## 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#get-available-bridges-and-dexs)

Get available bridges and DEXs

### 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#gettools)

`getTools`

Fetches the tools available for bridging and swapping tokens.

**Parameters**

- `params` (ToolsRequest, optional): Configuration for the requested tools.
    
    - `chains` ((ChainKey | ChainId)[], optional): List of chain IDs or keys.
        
    
- `options` (RequestOptions, optional): Additional request options.
    

**Returns**

A Promise that resolves to `ToolsResponse` and contains information about available bridges and DEXs.

**Example**

Copy

```
import { getTools } from '@lifi/sdk';

try {
  const tools = await getTools();
  console.log(tools);
} catch (error) {
  console.error(error);
}
```

## 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#get-available-connections)

Get available connections

A connection is a pair of two tokens (on the same chain or on different chains) that can be exchanged via our platform.

Read more [Getting all possible Connections](https://docs.li.fi/li.fi-api/li.fi-api/getting-all-possible-connections)

### 

[](https://docs.li.fi/integrate-li.fi-sdk/chains-and-tools#getconnections)

`**getConnections**`

Gets all the available connections for swapping or bridging tokens.

**Parameters**

- `connectionRequest` (ConnectionsRequest): Configuration of the connection request.
    
    - `fromChain` (number, optional): The source chain ID.
        
    - `fromToken` (string, optional): The source token address.
        
    - `toChain` (number, optional): The destination chain ID.
        
    - `toToken` (string, optional): The destination token address.
        
    - `allowBridges` (string[], optional): Allowed bridges.
        
    - `denyBridges` (string[], optional): Denied bridges.
        
    - `preferBridges` (string[], optional): Preferred bridges.
        
    - `allowExchanges` (string[], optional): Allowed exchanges.
        
    - `denyExchanges` (string[], optional): Denied exchanges.
        
    - `preferExchanges` (string[], optional): Preferred exchanges.
        
    - `allowSwitchChain` (boolean, optional): Whether connections that require chain switch (multiple signatures) are included. Default is true.
        
    - `allowDestinationCall` (boolean, optional): Whether connections that include destination calls are included. Default is true.
        
    - `chainTypes` (ChainType[], optional): Types of chains to include.
        
    
- `options` (RequestOptions, optional): Request options.
    

**Returns**

A Promise that resolves to a `ConnectionsResponse`.

**Example**

Copy

```
import { getConnections } from '@lifi/sdk';

const connectionRequest = {
  fromChain: 1,
  fromToken: '0x0000000000000000000000000000000000000000',
  toChain: 10,
  toToken: '0x0000000000000000000000000000000000000000',
};

try {
  const connections = await getConnections(connectionRequest);
  console.log('Connections:', connections);
} catch (error) {
  console.error('Error:', error);
}
```

For more detailed information on each endpoint and their responses, please refer to the [LI.FI API](https://docs.li.fi/li.fi-api/li.fi-api) documentation.