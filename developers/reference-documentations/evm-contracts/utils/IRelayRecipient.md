# Solidity API

## IRelayRecipient

_A contract must implement this interface in order to support relayed transactions
It is better to inherit the BaseRelayRecipient as its implementation_

### isTrustedForwarder

```solidity
function isTrustedForwarder(address forwarder) external view returns (bool)
```

Returns if the forwarder is trusted to forward relayed transactions to us.

_the forwarder is required to verify the sender&#x27;s signature, and verify
     the call is not a replay._

### versionRecipient

```solidity
function versionRecipient() external view returns (string)
```

_EIP 2771 version

NOTE:
- It is not clear if it is actually from the EIP 2771....
- https://docs.biconomy.io/guides/enable-gasless-transactions/eip-2771_
