# WHIP-003: Entity Declarations in HTML Metadata

```
Number:  WHIP-003
Title:   Entity Declarations in HTML Metadata
Type:    Standard
Status:  Draft
Authors: Blake Regalia (@blake-regalia)
Created: 2022-09-01
```


## Abstract

WHIP-003 allows Web3 Apps to declare a set of blockchains, accounts, and assets (e.g., contracts, tokens, etc.), collectively referred to here as _Entities_, and their associated metadata (i.e., addresses, token symbols, human-readable names, and icons) that the App intends to represent or interact with.


## Motivation

The diverse ecosystem of decentralized Apps is ever-growing and ever-changing, and the number of smart contracts and tokens associated with those Apps is ever-increasing. Rather than tracking everything in a centralized repository, WHIP-003 aims to allow the Apps themselves to declare metadata about these Entities to provide Wallets with all the information they need to store and represent them.


## Specification


### 1. Entity Icons

Declares the icon to use when representing an Entity.


##### TLDR;

Use [`<link rel="prefetch" as="image" ...>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/prefetch) in metadata along with a speicific `data-` attribute to identify the Entity and its type .


##### Entity Type and Identity

The three distinct types of Entity that can be represented by a WHIP-003 icon include blockchains, accounts, and assets. Each type is respectively identified by a [CAIP](https://github.com/ChainAgnostic/CAIPs) identifier:
| Entity type | Identifier                                                                     |
|-------------|--------------------------------------------------------------------------------|
| Blockchains | [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)   |
| Accounts    | [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md) |
| Assets      | *[CAIP-19](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md) |

* = Note: CAIP-19 can only identify native currencies (such as ETH, SCRT), Layer 2 tokens (such as USDC, SHD), and NFTs. For non-token smart contracts, you must use a CAIP-10 identifier.


##### Requirements

A `<link>` element with the following requirements:
1. Must be a direct descendent of the document's `<head>` element.
2. Must have its `rel` attribute set to `"prefetch"`.
3. Must have its `as` attribute set to `"image"`.
4. Must have its `href` attribute set to the URL of the Entity's icon.
5. Must have one of the following data attributes defined:
   - `data-caip-2` -- a [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) identifier to represent a blockchain's icon.
   - `data-caip-10` -- a [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md) identifier to represent an account's icon, either for a non-token smart contract or an account owned by a human.
   - `data-caip-19` -- a [CAIP-19](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md) identifier to represent an asset, such as a chain's native currency, Layer 2 token, or NFT.


#### Reasoning

Aside from being semantically correct, the `<link>` element also provides several benefits for App developers such as CORS and subresource integrity via the [integrity attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link#attr-integrity), allowing you to safely host Entity icon on a remote CDN.

The [`prefetch` link type](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/prefetch) was deliberately selected for several reasons: (1) it allows the browser to make an informed decision about when to fetch the resource (2) it allows Wallets to fetch the resource from cache without leaking to the endpoint that the request originated from a Wallet, thus preventing remote extension sniffing.


##### Supplementals

Wallets may use the following JavaScript snippet to obtain the URL of an Entity's icon:
```js
// chains use CAIP-2
const chainIcons = document.head.querySelectorAll('link[rel="prefetch"][as="image"][href][data-caip-2]');
for(const chainIcon of chainIcons) {
  const chainIconUrl = chainIcon.href;
}

// accounts use CAIP-10
const accountIcons = document.head.querySelectorAll('link[rel="prefetch"][as="image"][href][data-caip-10]');
for(const accountIcon of accountIcons) {
  const accountIconUrl = accountIcon.href;
}

// assets use CAIP-19
const assetIcons = document.head.querySelectorAll('link[rel="prefetch"][as="image"][href][data-caip-19]');
for(const assetIcon of assetIcons) {
  const assetIconUrl = assetIcon.href;
}
```


### 2. Entity Definitions

Declares a machine-readable set of attributes that define an Entity for Wallets to use when storing and representing them.


##### TLDR;

Fill in the contents of a `<script type="application/toml" data-whip-003>` in metadata to declare the Entities your App intends to interact with or provide to the user.


##### Requirements

A `<script>` element with the following requirements:
1. Must be a direct descendent of the document's `<head>` element.
2. Must have a `type` attribute set to one of the following Media Types:
   - `"application/toml"` - TOML is the preferred format for its readability and ease-of-reuse. [TOML Spec](https://toml.io/en/)
   - `"application/json"` - JSON is also allowed in order to alleviate server-side generated content. [JSON Spec](https://www.json.org/json-en.html)
3. Must have the `data-whip-003` attribute set with no value (as it is reserved for future use).

The contents of the script are used to provide any meaningful data about each Entity. The interface for the definitions are provided as follows in TypeScript, which applies to both the TOML and JSON serialization formats:
```ts
// see: https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md
type Caip2NamespaceString = string;  // [-a-z0-9]{3,8}
type Caip2ReferenceString = string;  // [-a-zA-Z0-9]{1,32}
type Caip2String = `${Caip2NamespaceString}:${Caip2ReferenceString}`;

// see: https://github.com/satoshilabs/slips/blob/master/slip-0044.md
type Slip44CoinTypeId = number;

// /^([a-z]{0,3}[A-Z0-9]{1,12})([ .-_/!:+]{1,2}[a-z]{0,3}[A-Z0-9()[\]]{1,12}){0,2}$/
type SymbolString = string;

// lowercase, hyphen-less token interface identifier, e.g., "erc20", "erc721", "snip20", "snip721", etc.
type ContractInterfaceString = string;

// the bech32 HRP string to use when prefixing account addresses
type Bech32HrpString = string;


/** WHIP-003 interface for Entity Definitions.
 * The interface consists of a set of optional dictionaries having the distinct keys: chains, accounts, coins, and contracts.
 * Each dictionary is keyed by `Alias`, an arbitrary string defined by the author for the sole purpose of identifying it locally.
 * The value of each dictionary is a struct with the required and optional known keys defined below.
 */
interface Whip003EntityDefinitions {
  // corresponding icon will have `data-caip-2="{namespace}:{reference}"`
  chains?: {
    [Alias: string]: {
      namespace: Caip2NamespaceString;
      reference: Caip2ReferenceString;
      label?: string;
      bech32s?: Bech32HrpString | {
        [Space: string]: Bech32HrpString;
      };
    };
  };
      
  // corresponding icon will have `data-caip-10="{chain}:{address}"`
  accounts?: {
    [Alias: string]: {
      chain: Caip2String;
      address: string;
      label?: string;
    };
  };
      
  // corresponding icon will have `data-caip-19="{chain}/slip44:{slip44}"`
  coins?: {
    [Alias: string]: {
      chain: Caip2String;
      slip44: Slip44CoinTypeId;
      symbol: SymbolString;
      label?: string;
    };
  };
      
  // corresponding icon will have ONE OF:
  //   `data-caip-19="{chain}/{interfaces[0]}:{address}"`
  //   `data-caip-10="{chain}:{address}"` (if interfaces is undefined or empty)
  contracts?: {
    [Alias: string]: {
      chain: Caip2String;
      address: string;
      label?: string;
      interfaces?: Array<ContractInterfaceString>;
    };
  };
}
```

##### Example

TOML is the preferred serialization format for its readability and ease-of-reuse. An example WHIP-003 declaration in TOML:
```toml
[chains.secret-network]
namespace = "cosmos"
reference = "secret-4"
label = "Secret Network"
bech32s = "secret"

[accounts.spongebob]
chain = "cosmos:secret-4"
address = "secret1aqfw3gmp6h9e2ggtpmm7q245dwnyjggq7n32ag"
label = "Spongebob Squarepants"

[coins.scrt]
chain = "cosmos:secret-4"
slip44 = 529
symbol = "SCRT"
label = "Secret"

[contracts.authenticator]
chain = "cosmos:secret-4"
address = "secret10mtm48ul5mcgjj4hm0a4j3td4l5pt590erl3k9"
label = "MyApp Authenticator"

[contracts.myTKN]
chain = "cosmos:secret-4"
address = "secret1dfdv860jwy0zq686zcaejl0s0c3axwgxy6xcc0"
interfaces = [ "snip20" ]
label = "My Special Token"
```

Or, the exact same definitions in JSON:
```json
{
  "chains": {
    "secret-network": {
      "namespace": "cosmos",
      "reference": "secret-4",
      "label": "Secret Network",
      "bech32s": "secret"
    }
  },
  "accounts": {
    "spongebob": {
      "chain": "cosmos:secret-4",
      "address": "secret1aqfw3gmp6h9e2ggtpmm7q245dwnyjggq7n32ag",
      "label": "Spongebob Squarepants"
    }
  },
  "coins": {
    "scrt": {
      "chain": "cosmos:secret-4",
      "slip44": 529,
      "symbol": "SCRT",
      "label": "Secret"
    }
  },
  "contracts": {
    "authenticator": {
      "chain": "cosmos:secret-4",
      "address": "secret10mtm48ul5mcgjj4hm0a4j3td4l5pt590erl3k9",
      "label": "MyApp Authenticator"
    },
    "myTKN": {
      "chain": "cosmos:secret-4",
      "address": "secret1dfdv860jwy0zq686zcaejl0s0c3axwgxy6xcc0",
      "interfaces": [ "snip20" ],
      "label": "My Special Token"
    }
  }
}
```


## Backwards Compatibility

WHIP-003 is intended to be minimally intrusive to existing web pages by leveraging the appropriate semantics within HTML metadata.


## Examples

A complete example of an App abiding to WHIP-003:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Homepage for MyApp: Doing Stuff Right</title>

  <!-- chain icon -->
  <link rel="prefetch" as="image" href="/secret-network.svg" data-caip-2="cosmos:secret-4">

  <!-- account icon for human contact -->
  <link rel="prefetch" as="image" href="/spongebob.png" data-caip-10="cosmos:secret-4:secret1aqfw3gmp6h9e2ggtpmm7q245dwnyjggq7n32ag">

  <!-- asset icon for native coin -->
  <link rel="prefetch" as="image" href="/scrt.png" data-caip-19="cosmos:secret-4/slip44:529">

  <!-- account icon for non-token smart contact -->
  <link rel="prefetch" as="image" href="/auth.png" data-caip-10="cosmos:secret-4:secret10mtm48ul5mcgjj4hm0a4j3td4l5pt590erl3k9">

  <!-- asset icon for token -->
  <link rel="prefetch" as="image" href="/susdc.svg" data-caip-19="cosmos:secret-4:snip20/secret1k0jntykt7e4g3y88ltc60czgjuqdy4c9e8fzek">

  <!-- entity definitions, with an entry corresponding to each icon above -->
  <script type="application/toml" data-whip-003>
    [chains.secret-network]
    namespace = "cosmos"
    reference = "secret-4"
    label = "Secret Network"
    bech32s = "secret"

    [accounts.spongebob]
    chain = "cosmos:secret-4"
    address = "secret1aqfw3gmp6h9e2ggtpmm7q245dwnyjggq7n32ag"
    label = "Spongebob Squarepants"

    [coins.scrt]
    chain = "cosmos:secret-4"
    slip44 = 529
    symbol = "SCRT"
    label = "Secret"

    [contracts.authenticator]
    chain = "cosmos:secret-4"
    address = "secret10mtm48ul5mcgjj4hm0a4j3td4l5pt590erl3k9"
    label = "MyApp Authenticator"

    [contracts.myTKN]
    chain = "cosmos:secret-4"
    address = "secret1dfdv860jwy0zq686zcaejl0s0c3axwgxy6xcc0"
    interfaces = [ "snip20" ]
    label = "My Special Token"
  </script>
</head>
<body>
  <h1>Welcome to MyApp</h1>
</body>
</html>
```


## References
- [`<link rel="prefetch" as="image" ...>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/prefetch)
- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [CAIP-10](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md)
- [CAIP-19](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-19.md)
- [TOML Spec](https://toml.io/en/)
- [JSON Spec](https://www.json.org/json-en.html)
- [SLIP-0044](https://github.com/satoshilabs/slips/blob/master/slip-0044.md)
