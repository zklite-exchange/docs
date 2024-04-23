# Overview

[**zkLite Exchange**](https://zklite.io) was launched on zkSync Lite (previously zkSync 1.0) in Apr 2024 based on ZigZag legacy source codes. On this page, you will find more information about how the DEX works.

## Atomic swaps <a href="#atomic-swaps" id="atomic-swaps"></a>

zkSync Lite does not support smart contracts, but only pre-compiled contracts by MatterLabs. zkLiteExchange is utilizing the built-in [atomic swap](https://docs.lite.zksync.io/dev/swaps/#atomic-swaps) feature to provide swaps to users. **zkLite Exchange** matches users with market maker bots. Users and market-maker bots can post liquidity in the order book, but only market-maker bots can fill orders. Unfortunately, zkSync Lite does **not support partial fills**. This means that orders will only get executed when a market maker can fully fill the order. More information on market maker bots can be found on the [Market Maker page](market-maker-bot.md).

## Swap fees <a href="#swap-fees" id="swap-fees"></a>

There are no fees for placing or canceling orders. **zkLite Exchange** is also not charging any protocol fee for the use of the platform. Users only pay swap fees (around $0.05) to cover[ zkSync network fees ](https://docs.lite.zksync.io/userdocs/tokens/#fee-costs)(as found on [transactions in the explorer](https://zkscan.io/), or on [L2Fees](https://l2fees.info/)). Market maker bots pay these network fees, but users pay the swap fee to the market maker. Swap fees are [paid with the token you're trading](https://docs.lite.zksync.io/userdocs/tokens/#supported-tokens). You don't need ETH for swap fees for example. If you bridge over DAI to zkSync, you can trade DAI for ETH and pay the gas fee with your DAI.

zkSync network fees depend on network activity and L1 gas. With more activity on zkSync, swap fees will go down. Thus, swap fees will lower over time. In the beginning, network fees were $1 on zkSync, but have now lowered to $0.05.

## Limit order system <a href="#limit-order-system" id="limit-order-system"></a>

The limit order system is live on zkSync Lite. After 7 days of placing a limit order, it will expire and a new order has to be placed. On zkSync Lite you can only have **one** order open at a time. If you have a limit order open, you can't place other orders on that account. If you make a normal transaction (sending funds from your account) or a bridge transaction, your limit order will be canceled.

## Bridging/Deposit/Withdraw <a href="#bridging-and-fees" id="bridging-and-fees"></a>

* zkSync Lite portal: [https://lite.zksync.io/](https://lite.zksync.io/)
* LayerSwap: [https://www.layerswap.io/app](https://www.layerswap.io/app)

## **List your pair on zkLite Exchange**

If your token isn't available on **zkLite Exchange**,  you can submit a request via our [community channels](../links.md#social-media-and-community). We will list your token as soon as liquidity providers are ready for it.

## What is the account activation fee? (Change Pubkey transaction) <a href="#what-is-the-account-activation-fee-change-pubkey-transaction" id="what-is-the-account-activation-fee-change-pubkey-transaction"></a>

The account activation fee is a one-time fee imposed by zkSync to[ register your account with zkSync](https://docs.lite.zksync.io/userdocs/tutorials/#account-activation). This fee only applies to your first zkSync transaction. The registration process happens directly on the Ethereum smart contract and therefore it is an L1 transaction, so the activation fee is to pay the Ethereum miners and not zkSync validators.

## Tokens listed on zkLite Exchange <a href="#tokens-listed-on-zigzag" id="tokens-listed-on-zigzag"></a>

All tokens listed on **zkLite Exchange** can be found here: [https://zkscan.io/explorer/tokens/](https://zkscan.io/explorer/tokens/). zkSync filters out tokens and lists the correct ones based on CoinGecko and Uniswap. This means that only legit tokens will get their correct ticker. Scam tokens will be listed as ERC20-XXX tokens. **zkLite Exchange** can only list tokens that have been bridged through zkSync's smart contract. The token name and ticker are pulled from the token contract and can be found in the pair.

Clarification on certain tokens:

* FTM - Native
* MATIC - Native
* SOL - Wormhole
* AVAX - Wormhole

## What is the difference between an Initiated, Committed, and Verified transaction on zkScan? <a href="#what-is-the-difference-between-an-initiated-committed-and-verified-transaction-on-zkscan" id="what-is-the-difference-between-an-initiated-committed-and-verified-transaction-on-zkscan"></a>

The differences can be found in [zkSync's FAQ](https://docs.lite.zksync.io/userdocs/faq/#faq):

* **Initiated:** the zkSync server has received and processed the transaction.
  * If you made a **transfer** or **swap**, your funds are available immediately.
* **Pending:** the transaction appears in a block that is committed to the L1 smart contract.
* **Complete:** the transaction’s block has been proven and verified on the L1 smart contract.

## Nonce mismatch <a href="#nonce-mismatch" id="nonce-mismatch"></a>

Occasionally a ‘nonce mismatch’ error can come up when placing an order, resulting in a rejected order. This does **not** result in deducted gas or trading fees. What you can do as user is to refresh, reconnect your wallet, and place a new order.

When a user signs an order, the nonce is included in the signed message. So when the swap is submitted, the user's nonce has to match the signed nonce. If the user or the market maker increases their nonce before the swap is submitted (by making any other transaction, eg transfer, withdraw or another swap) then the order they signed becomes invalid. This becomes especially apparent when a market maker has to process a lot of swaps at a time.
