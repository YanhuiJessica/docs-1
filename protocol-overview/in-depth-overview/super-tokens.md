---
description: Tokens that possess Superfluid functionality
---

# Super Tokens

## Definition

We usually experience on-chain value transfer through the ERC20 token. ERC20 token contracts work like bank balances, moving value through discrete lump-sum transfers (i.e. my balance goes down "X" and your balance goes up "X").

The Super Token is our extension of the ERC20 token standard that plugs into the Superfluid Protocol to include Super Agreement abilities. These Super Agreements allow Super Tokens to be transferred in powerful ways such as in streams or instant distributions. Super Tokens come in two forms: **wrapper** and **custom.**

{% hint style="info" %}
Super Tokens can do everything that a traditional ERC20 token can PLUS new modes of value transfer enabled by Superfluid (i.e., money streaming)
{% endhint %}

## **Real-Time Balance**

The real-time balance is what lets Super Tokens keep track of an account's balance across changes caused by both regular transfers and Super Agreements. An account's actual current Super Token balance is the sum of its **static balance** and its **real-time balances**.&#x20;

* Static Balance: balance figure that is affected by basic lump-sum transfers (the usual ERC20 stuff)
* Real-Time Balances: the individual impact that each Super Agreement has on an account's balance. That impact can either be positive or negative.

By combining these two parts, we can get an account's actual current balance.

> Current Balance = Real-Time Balances<mark style="color:green;">**\***</mark> + Static Balance

<mark style="color:green;">**\***</mark> Bear in mind that there are multiple Super Agreements ([CFA](https://docs.superfluid.finance/superfluid/protocol-overview/in-depth-overview/super-agreements/constant-flow-agreement-cfa) and [IDA](https://docs.superfluid.finance/superfluid/protocol-overview/in-depth-overview/super-agreements/instant-distribution-agreement-ida)) each with their own real-time balances. So to arrive at the current balance, the real-time balance for each one is added to the static balance.&#x20;

**Example**&#x20;

* Account A's Static Balance: 1,000 USDCx
* Account A has an active CFA stream going that has streamed out 100 USDCx so far.
  * CFA Real-Time Balance = <mark style="color:red;">-100</mark> USDCx
* Account A has received 200 USDCx through IDA distributions.
  * IDA Real-Time Balance = <mark style="color:green;">+200</mark> USDCx

> Current Balance = 1000 + <mark style="color:red;">-100</mark> + <mark style="color:green;">200 =</mark> **1100 USDCx**

The bottom line is that while a regular ERC20 just tracks a static balance which it shows when you call `balanceOf()`, a Super Token takes that layers on real-time balances to account for Super Agreements.

## Types of Super Tokens

### **Wrapper**

A wrapper Super Token is an _existing underlying token_ that's been "wrapped" into a Super Token to gain Super Agreement functionality.

**Wrapping and Unwrapping**

When getting wrapper Super Tokens, you first deposit the underlying tokens into its wrapper Super Token contract after which you are minted an equal quantity of wrapper Super Tokens. Basically, you gave up the plain underlying token and got the "Super Token version" of it.&#x20;

To unwrap, the opposite happens; a desired amount of Super Tokens are burned and an equal amount of the underlying token is returned.

**Example**

![](<../../.gitbook/assets/image (40).png>)

### Custom

Custom Super Tokens don't have an underlying token. They exist only as Super Tokens so there's no wrapping or unwrapping required. Custom Super Tokens are deployed directly as Super Tokens with all of the associated Superfluid functionality out of the box. These tokens inherently have all the functionality of a basic ERC20 token plus Superfluid's Super Agreement abilities.

**Example**

$RIC is a governance token deployed by [Ricochet DAO](https://ricochet.exchange/), a community building Superfluid-powered investment tools. Knowing that they would be heavily using Super Agreements (money streaming and instant distributions) on $RIC, they chose to deploy it directly as a Custom Super Token, rather than a plain ERC20 with an accompanying Wrapper Super Token.

![](<../../.gitbook/assets/image (31).png>)
