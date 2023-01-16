# WHIP-005: Form Autofill

```
Number:  WHIP-005
Title:   Form Autofill
Type:    Standard
Status:  Draft
Authors: Blake Regalia (@blake-regalia)
Created: 2023-01-16
```


## Abstract

WHIP-005 allows Apps to specify how form elements within their HTML document can be autofilled by Wallets.


## Motivation

Many single-page web apps such as testnet faucets, fee grants, airdrops, and so on, present a simple front-end interface for some back-end service that dispatches an operation on-chain requiring the client's public address. Oftentimes, these front-end Apps don't require interaction with the Wallet, as users only need to copy-paste their public address into the input form element.

Rather than requesting to connect to the Wallet with a set of permissions, this proposal aims to streamline the input process by allowing Wallets to augment the form elements with controls for selecting and autofilling the desired content.


## Specification

### 1. Input for Account Address

Describes an `<input>` element whose value desires the user's public address on some given chain(s).


##### TLDR;

Add the `data-whip-005-type` and `data-whip-005-chains` attributes to the input element in question:
```html
  <!-- Input desires user's public address on cosmos:secret-4 -->
  <input type="text" data-whip-005-type="account" data-whip-005-chains="cosmos:secret-4">
```


##### Purpose

Apps may use this to enhance the end-user experience when inputting their public address.


##### Requirements

An `<input>` element with the following requirements:
1. Must be a descendent of the document's `<body>` element.
2. Must have its `type` attribute set to `"text"`.
3. Must have its `data-whip-005-type` attribute set to `"account"`.
4. Must have its `data-whip-005-chains` attribute set to a space-separated list of acceptable [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md) identifiers.

> NOTE: The `data-whip-005-chains` attribute may specify multiple chains, however this should only be used on a set of chains that have distinct Bech32 HRPs. For example, `"cosmos:cosmoshub-4 cosmos:secret-4"` is acceptable since "cosmos1" and "secret1" are mutually exclusive, however `"cosmos:secret-4 cosmos:pulsar-2"` is not acceptable since both chains use the "secret1" Bech32 HRP. Furthermore, `"eip155:1 eip155:56"` (Ethereum mainnet and BSC) is not acceptable since the address namespaces are indistinguishable.


##### Supplementals

Wallets may use the following JavaScript snippet to obtain a list of autofillable account inputs:
```js
const accountInputs = document.body.querySelectorAll('input[type="text"][data-whip-005-type="account"][data-whip-005-chains]');
for(const accountInput of accountInputs) {
  const caip2s = accountInput.dataset['whip-005Chains'].split(/\s+/g);
}
```


## Backwards Compatibility

WHIP-005 augments form elements with custom data attributes. Apps should expect to employ minimal changes in order to meet these criteria.


## Examples

A snippet showing an example of an implementing WHIP-005:

```html
<!doctype html>
<html lang="en">
<body>
  <label for="address">Secret Network address:</label>
  <input name="address" type="text" data-whip-005-type="account" data-whip-005-chains="cosmos:secret-4">
  <button>Claim</button>
</body>
</html>
```


## References

- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
