# **Xar - crypto agnostic defi**

The layer 1 crypto agnostic decentralized finance platform.

Xar Network was created from a need of corporate and central banks to use blockchain technology in a private, permissioned space. As our feature set grew we noticed consistent cross-over with the decentralized finance ecosystem, so eventually the Xar toolkit grew to a full-fledged decentralized finance toolbox. Xar Network offers access to advantages of both purely traditional banking systems and blockchain systems - using blockchain based or decentralized finance (DeFi).

XAR Network’s public chain is a permissionless decentralized network with a focus on DeFi (decentralized finance). Based on Lachesis and the TxFlow protocol, Fantom Foundation's consensus mechanism allows high responsiveness with almost instantaneous full finality (~1.2 seconds), at very high transactional throughput (processing in excess of 20,000 transactions per second). As a result, Xar Network and our customized and localized chains can provide fully verifiable, transparent and truly decentralised validation of transactions in the real world - at an unprecedented speed.

XAR Network's public chain allows you to deposit any supported digital asset, collateralize it, mint Collateralized Stable Debt Tokens (CSDTs) based on this collateral, and then use these CSDTs to stake and earn rewards. All the while maintaining ownership of your underlying collateralized asset. Staking CSDT allows you to receive rewards from the fees pool, proportional to your share of the total CSDT stakes in the network. Your rewards are paid in a stable currency token, such as CSDT (collateralized stable debt/dollar/decentralized token), not in an inflationary token as in some other networks.

- [Project Overview](#project-overview)
  * [Project Name](#project-name)
  * [Coin Name](#coin-name)
  * [Official website](#official-website)
  * [Elevator Pitch](#elevator-pitch)
- [Problem Statement](#problem-statement)
  * [Inflationary Staking](#inflationary-staking)
  * [Stable Staking Rewards](#stable-staking-rewards)
  * [The role of tokens as network security](#the-role-of-tokens-as-network-security)
  * [Staking security vs DeFi collateral](#staking-security-vs-defi-collateral)
  * [Split fees and split collateral](#split-fees-and-split-collateral)
- [Solution](#solution)
  * [Collateralized Stable Debt Tokens](#collateralized-stable-debt-tokens)
  * [Stable Staking](#stable-staking)
  * [Non-Inflationary](#non-inflationary)
  * [Shared Collateral and Fees](#shared-collateral-and-fees)
  * [Maintaining CSDT value (Rebalancing explained)](#maintaining-csdt-value--rebalancing-explained-)
- [Solution Summary](#solution-summary)
- [Project Details](#project-details)
  * [Feature Set](#feature-set)
  * [Traditional Use Cases](#traditional-use-cases)
  * [Supported Collateral](#supported-collateral)
  * [Planned support](#planned-support)
  * [Target Demographic (High Level)](#target-demographic--high-level-)
  * [Long term vision](#long-term-vision)
  * [Relevant milestones in the past and upcoming 24 months](#relevant-milestones-in-the-past-and-upcoming-24-months)
  * [Necessity of a new native coin](#necessity-of-a-new-native-coin)
  * [Project Competitors](#project-competitors)
- [Product](#product)
  * [Development status](#development-status)
  * [Relevant product links](#relevant-product-links)
  * [Open Source License](#open-source-license)
  * [Github Repo link](#github-repo-link)
- [Features of the coin (CSDT)](#features-of-the-coin--csdt-)
  * [CSDT use cases](#csdt-use-cases)
  * [Voting Rights via CSDT](#voting-rights-via-csdt)
    + [Upgrade Proposal](#upgrade-proposal)
    + [Param Change Proposal](#param-change-proposal)
    + [Text Proposal](#text-proposal)
    + [Voting Explained](#voting-explained)
  * [Collateral Sustainable Stable Rewards (CSSR)](#collateral-sustainable-stable-rewards--cssr-)
    + [Proof of Stake](#proof-of-stake)
    + [Collateralized Stable Tokens](#collateralized-stable-tokens)
    + [Liquidity based lending](#liquidity-based-lending)
    + [Collateral Sustainable Stable Rewards](#collateral-sustainable-stable-rewards)
  * [On-chain Fees](#on-chain-fees)
  * [Simulated Staking Rewards](#simulated-staking-rewards)
- [Token Economics](#token-economics)
  * [Current Market capitalization (at the time of writing)](#current-market-capitalization--at-the-time-of-writing-)
  * [Total coin supply](#total-coin-supply)
  * [Listed Exchanges](#listed-exchanges)
  * [Bootstrapping](#bootstrapping)
  * [Slashing](#slashing)
- [Wallet](#wallet)
  * [ERC20](#erc20)
  * [Blockchain Explorer](#blockchain-explorer)
  * [Web Wallet](#web-wallet)
  * [SDKs](#sdks)
  * [Coin protocol](#coin-protocol)
  * [Project team full nodes](#project-team-full-nodes)
- [Technical Overview](#technical-overview)
  * [Module Auction](#module-auction)
  * [Module Lending / CSDT](#module-lending---csdt)
  * [Module CSDT / Decentralized Stable Tokens](#module-csdt---decentralized-stable-tokens)
  * [Module Escrow](#module-escrow)
  * [Module Issue](#module-issue)
  * [Module Liquidator](#module-liquidator)
  * [Module Market](#module-market)
  * [Module Order](#module-order)
  * [Module NFT](#module-nft)
  * [Module Oracle](#module-oracle)
  * [Module Record (Proof of Existence)](#module-record--proof-of-existence-)
  * [Module Coinswap](#module-coinswap)
  * [Module Synthetic](#module-synthetic)
  * [DEX Matching Engine](#dex-matching-engine)
- [Xar FAQ](#xar-faq)
- [Users](#users)
  * [User Basics](#user-basics)
    + [Q: How to create a wallet?](#q--how-to-create-a-wallet-)
    + [Q: How to transfer funds from erc20/bep2 to Xar?](#q--how-to-transfer-funds-from-erc20-bep2-to-xar-)
    + [Q: How to confirm that you received funds?](#q--how-to-confirm-that-you-received-funds-)
  * [User CSDT](#user-csdt)
    + [Q: What is CSDT and how does it work?](#q--what-is-csdt-and-how-does-it-work-)
    + [Q: What is ucsdt and uftm?](#q--what-is-ucsdt-and-uftm-)
    + [Q: How to mint ucsdt from uftm?](#q--how-to-mint-ucsdt-from-uftm-)
    + [Q: How to calculate how much CSDT I can create?](#q--how-to-calculate-how-much-csdt-i-can-create-)
  * [User Staking](#user-staking)
    + [Q: How much staking rewards will I get?](#q--how-much-staking-rewards-will-i-get-)
    + [Q: How much is currently staked?](#q--how-much-is-currently-staked-)
- [Developers](#developers)
    + [Q: Where can I find general resources?](#q--where-can-i-find-general-resources-)
  * [Developer Blockchain](#developer-blockchain)
    + [Q: How do I install Xar?](#q--how-do-i-install-xar-)
    + [Q: How do I run a testnet?](#q--how-do-i-run-a-testnet-)
  * [Developer JavaScript / NodeJS](#developer-javascript---nodejs)
    + [Q: How can I interact with the chain?](#q--how-can-i-interact-with-the-chain-)
    + [Q: Where can I find code samples?](#q--where-can-i-find-code-samples-)
    + [Q: What functions are currently supported?](#q--what-functions-are-currently-supported-)
  * [Developer Web / HTTPS](#developer-web---https)
    + [Q: Is there an API I can interact with?](#q--is-there-an-api-i-can-interact-with-)
    + [Q: Where can I find documentation in the API?](#q--where-can-i-find-documentation-in-the-api-)
- [Validators](#validators)
    + [Q: How do I install a Xar node?](#q--how-do-i-install-a-xar-node-)
    + [Q: How do I join the mainnet?](#q--how-do-i-join-the-mainnet-)
    + [Q: What should I know as a validator?](#q--what-should-i-know-as-a-validator-)
    + [Q: What should I know about security as a validator?](#q--what-should-i-know-about-security-as-a-validator-)
- [General](#general)
- [Publications](#publications)
    + [The Economics of Smart Contracts](#-the-economics-of-smart-contracts)
    + [Fast Stochastic Peer Selection in Proof-of-Stake Protocols](#-fast-stochastic-peer-selection-in-proof-of-stake-protocols)
    + [StairDag: Cross-DAG Validation For Scalable BFT Consensus](#-stairdag--cross-dag-validation-for-scalable-bft-consensus)
    + [StakeDag: Stake-based Consensus For Scalable Trustless Systems](#-stakedag--stake-based-consensus-for-scalable-trustless-systems)
    + [ONLAY: Online Layering for scalable asynchronous BFT system](#-onlay--online-layering-for-scalable-asynchronous-bft-system)
    + [Fantom: A scalable framework for asynchronous distributed systems](#-fantom--a-scalable-framework-for-asynchronous-distributed-systems)
    + [OPERA: Reasoning about continuous common knowledge in asynchronous distributed systems](#-opera--reasoning-about-continuous-common-knowledge-in-asynchronous-distributed-systems)

## Project Overview

### Project Name

Xar Network

### Coin Name

CSDT (Collateralized Stable Debt Tokens)

### Official website

[Xar Network](https://xar.network/)

### Elevator Pitch

*   Non-Inflationary, Stable, Sustainable Proof Of Stake
*   Consolidated liquidity across DeFi offerings
*   Decentralized, Stable, Unbiased currency that offers stable rewards
*   The framework for Cosmos and Fantom-based decentralized finance.

## Problem Statement

*   Staking rewards vs DeFi liquidity of assets
*   Inflationary tokens used as rewards for staking
*   Non stable rewards, impacting Opex planning
*   Non linearly scalable on-chain security via staking
*   No shared fees between DeFi offerings
*   No optimized liquidity provider between DeFi offerings

### Inflationary Staking

More tokens are minted as reward for validators providing security to a network. This only works if you measure your rewards in the inflationary token, however server costs are measured in fiat, for the sake of simplicity, USD. When a token’s supply inflates, it normally suffers a direct inverse correlation with price. If you double supply, you would halve the price. So the net result for validators is often negative. Cost in USD-USD value of tokens received over time.

Inflationary models are also unsustainable as you can’t infinitely keep minting new tokens, supply should be limited to ensure ongoing viability for early adopters.

_A sustainable staking solution would need non-inflationary rewards._


### Stable Staking Rewards

As mentioned in the previous section, server costs are measured in USD, however rewards are in tokens, to offset this, you need to sell tokens, when a tokens price depreciates to the point where it no longer covers the opex expenses, you need to discontinue the service. For this reason, staking is mostly a very mutable solution where staking farms will move from one coin to the next to ensure maximized profit due to fluctuating prices.

_A stable staking solution would need to pay rewards in a stable token._


### The role of tokens as network security

A token provides security for its network. If you have a public blockchain that tokenized real-estate. And let’s assume it has $200M worth of tokenized real-estate. However, the underlying token staking value is worth $2M. Then in a staking model, it would cost you ~$2M to attack an object of value equal to $200M. The value of the underlying securitized token is what protects the network and its assets. So the value of the underlying security assets, should exceed, or at least match, the value of the managed assets.

_A linearly scalable network would require to accept multiple collateral types._


### Staking security vs DeFi collateral

The role of a token as a layer 1 network is network security. It offers a numeric value that must be overpowered to gain control of the network. With more DeFi offerings there are very competitive interest and reward rates to cannibalize the underlying network securing token into DeFi instead. This split reducing network security, and reducing DeFi liquidity. 

_An effective layer 1 solution needs to combine both of these practices._


### Split fees and split collateral

Each new DeFi solution competes with each other over fees, and collateral. Increased fees, lead to increased collateral. Users need to move their collateral from one solution to the next to micromanage where they get the most benefit and rewards.

If collateral was shared across all DeFi solutions, then fees could be consolidated. This would lead to greater fees for the collateral provider, and lower rates for the borrower (to offset the current collateral & fee war)

## Solution

To circumvent this, we designed a system that has;

*   Stable Rewards
*   Multi asset support
*   Non-inflationary
*   Shared liquidity
*   Shared fees

This was achieved via 2 popular DeFi mechanisms, over collateralization, and liquidity pool lending.


### Collateralized Stable Debt Tokens

Collateralized Stable Debt Tokens or CSDT are USD pegged stable tokens minted from provided collateral. This allows validators / delegators to provide collateral in any native supported asset (FTM/BTC/ETH/BNB on genesis), and mint CSDT. The collateralized ratio of each asset is set via governance and on genesis would be FTM 150%, BTC 150%, ETH 150%, BNB 150%

A practical example of how this works;

We deposit 100,000 FTM into our Collateralized Contract, the validators via their approved oracles have agreed (via consensus) that the current price for 1 FTM is $0.20. The value of the deposited FTM is $20,000. FTM is collateralized at 100%, so the minting value would be $20,000, or 20,000 CSDT that can be minted. 

An important disclaimer here, it is best practice to not mint the maximum allowed as this sets a very high liquidation price for your assets. The way the stability of the price is managed is via the liquidation of assets should the token price depreciate. In the above example, should FTM price fall to $0.18 the collateral FTM would be rebalanced and made available for auction at discount, so that another user could purchase the FTM for CSDT (raised CSDT is used to pay off partial debt). If however in the example above the collateral provider instead decided to mint 5,000 CSDT, then the liquidation price would be ~$0.10 and they have a lot more safety and room to manage their collateral.


### Stable Staking

With CSDT created, we can now create a validator by staking CSDT. Rewards will be paid out in CSDT. Current rewards are set at 7% with a staked target of 67%. So if there is 1,00 CSDT minted, and 67 are staked the reward will be 7% annually. Should more than 67% be staked, this will decrease to 6% over time, and should less than 67% be staked, then this will grow to 30% over time.

Since CSDT is USD pegged, it means that your returns are fixed against your operational costs.


### Non-Inflationary

Now that there is a liquidity pool available of assets (via the Collateral Contracts) it means that users of the system can borrow assets. This is collateralized lending with the ratio set per supported asset. Additional assets over and above CSDT assets can be supported. 

Practically, this would mean a borrower can provide BTC as collateral, and borrow ETH against this, with the interest being set based on the ratio of liquidity providers to borrowers. Judging by current rates, this is around ~4%. This interest is then paid to the liquidity providers (stakers) and offsets that value of staking rewards. 

Eventually with network growth and liquidity providers, this will offset the ~7%–10% of required staking rewards and arrive at a non-inflationary model.


### Shared Collateral and Fees

All DeFi solutions are built into the protocol as native layer 1 solutions. They do not interact on a secondary smart contract layer. But instead interact directly with the protocol layer.

Stakers provide collateral to a shared liquidity pool via staking their collateral. The native layer 1 DeFi modules; coinswap, DEX, synthetic, and loan modules borrow from this consolidated liquidity pool. The pool receives consolidated rewards from all modules. This optimized collateral provides lower fees and interest rates for borrowers.

All fees are shared to this liquidity pool, fees are generated as follows;

*   Transaction fee, 0.025ucsdt on every transaction
*   Governance proposal fee, fixed fee per proposal
*   Rebalancing fee (default 30%)
*   Issuance fee, fixed fee per asset issued
*   Auction fees (volume based, default 0.0025% Maker/Taker)
*   DEX fees (volume based, default 0.0025% Maker/Taker)
*   Synths (volume based, default ~0.0025% - 3% Long/Short)
*   Coinswap (trade size based, ~0.0025 - 3%) per trade
*   Lending (Utilization % formula)

All these fees are awarded to the distribution pool. The distribution pool distributes to the stakers & delegators

This is why the chain can provide much higher staking rewards, and much lower borrower fees. All CSDT collateral goes into the liquidity pool. Coinswap, DEX, Lending, Synthetics, and Auctions modules all loan from the liquidity pool

Shared liquidity (cheaper rates) and consolidated fees (higher rewards)

### Maintaining CSDT value (Rebalancing explained)

Let’s say you create a CSDT with 150% collateral of FTM and at a price of $0.0121. Your total collateral is $181 (15,000 FTM). You withdraw $100. Your “liquidation” price is $0.01.

So what happens when the price of 1 FTM decreases to $0.01. Your CSDT position becomes eligible for “rebalancing”. The system takes a minimum amount of collateral, configured via the “rebalancing” module. The minimum for FTM is currently configured as 10,000 FTM. This 10,000 FTM is removed from your collateral and auctioned off to the highest bidder. So let’s assume we get market value for it, so we receive; 10,000 * 0.01 (current price that triggered your “rebalancing”). So we received $100. This $100 pays off the debt of the CSDT ($100), and the CSDT now has a balance of 5,000 FTM (15,000 FTM original-10,000 FTM (auctioned)), and a debt of $0. Your holdings are, 5,000 FTM and $100. The candidate that won the auction has 10,000 FTM and -$100.

Now let’s assume we did not get the market price of 0.01, and only received $90, in this case, debt is decreased by $90, leaving $10. So the CSDT has collateral 5,000 FTM (worth $50), and your debt is $10. Giving you a collateral ratio of 303%.


## Solution Summary

CSDT is a non-inflationary, stable reward, sustainable Proof-Of-Stake solution, that provides greater yield for stakers (via consolidated DEFI) and lower interest rates and fees for borrowers and traders (via consolidated liquidity).

Stakers provide collateral to the coinswap, DEX, synthetic, and loan modules, and receive consolidated rewards from all modules. Collateral is consolidated in a collateral pool and each module borrows from this pool and pays interest rates and fees. This optimized collateral provides lower fees and interest rates for borrowers.

(For the Staker/Validator) Consolidated fees for higher DeFi rewards 

(For the borrower/trader) Lower interest rates/fees because of consolidated liquidity 

(For chain security) Shared security between DeFi and Staking

From an economics perspective;

Non inflationary, stable rewards

For better Opex and reward management from a coin that won't devalue because of Inflationary supply

## Project Details

### Feature Set

The following is a high level description of the base instruments made available via the technological modules that have been designed. Following this section there will be examples of how these instruments can be used to create DeFi and decentralized derivative markets.

Here is a brief overview of Xar modules. We will later cover these modules in more detail.

*   auth – basic account management and account queries
*   bank – basic transfer management
*   coinswap – liquidity pool based swaps
*   staking – how to stake and delegate minted CSDT
*   supply – read only overview of current bank balances
*   auction – create and bid on forward & reverse auctions for denomination lots as well as NFT
*   csdt – create and manage collateral stable debt tokens via accepted on-chain collateral
*   issue – create and manage erc20 compatible assets
*   liquidator – trigger liquidation events on undercollateralized csdt and start auction bids on seized lots
*   market – read only list of current DEX markets
*   oracle – price and time feed oracles for near real time price and time values
*   order – place bids and asks on the DEX markets
*   record – record / anchor immutable proofs on-chain
*   synthetic – synthetic crypto buy and sell denominated in CSDT

The above are the raw instruments required to build a variety of traditional finance tooling on top of the existing DeFi ecosystem.


### Traditional Use Cases

Coins for Open Finance

*   Increases the Bank’s FIAT Deposits (Liquidity) by attracting customer funds
    *   Offer customers’ new utility on funds (Transacting)
    *   Provides new savings products (Fixed Term / Call Accounts)
    *   Application for Securitisation (Collateralisation)
*   Readiness for Central Bank Digital currencies
    *   Commercial Bank Stable Tokens
    *   Commercial Bank money as well as Coin and Note on and off-ramp to CBDC

Tokenised Markets for Investment Banks

*   Primary Debt & Equity Markets
    *   Issuance, Book Building, Auction, Interest Payment, and Term Renegotiations
*   Secondary Debt & Equity Spot Markets
*   Alternative Token Markets
    *   Gold, Silver, Platinum, Diamonds, Oil, and more
*   Tokenised P2P Synthetic Futures
    *   No exportation of value, capital flight, or BoP requirements
    *   Forex Futures (Hedging / Cover) Markets
    *   Global Shares and/or Commodity Futures Markets
    *   Carbon Credit / Green Energy Futures Markets
    *   Equity Future Markets

Digital Currency for Central Banks

*   Net Interbank Settlements
*   Treasury Notes, Bills and Bonds Management
*   Foreign Stable Token Exchange
    *   B2B Cross Border Payments
*   Mass Market Digital Currency
    *   Remittance of Social Grants

Managing Debentures Issuing

*   Debt tokenisation
*   Debt modelling through capital and interest tokens
*   IOI / book building
*   Auction / sale processes
*   Extension to support Equity Token issuance

### Supported Collateral

*   FTM

### Planned support

*   BNB
*   BTC
*   ETH

*Governance dependent

### Target Demographic (High Level)

*   Retail DeFi investors
*   Central and corporate banks on the FinTech side

### Long term vision

Grow on-chain AUM to ~$100MM, accomplishing this via competitive interest rates and higher APR yield. Stakers provide liquidity and security. We are also working with multiple Central and Corporate bank projects in 3 different geographic regions.

### Relevant milestones in the past and upcoming 24 months

*   Feb 2019 Signed agreement with 1st Corporate Bank for application of [DLT technologies](https://www.blog.xar.network/the-case-for-bank-stable-coins/)
*   Apr 2019 Partnership with Fantom Foundation as technology partner
*   June 2019 Deployment of internal DLT solution for Corporate Bank
*   July 2019 Addition of token issuance and KYC/AML management
*   Sept 2019 Deployment of CSDT for cross-border payments
*   Oct 2019 Deployment of CSDT as [stable staking reward mechanism](https://www.blog.xar.network/xar-network-staking-explained/)
*   Nov 28 2019 Soft Launch
*   Nov 29 2019 Partnership with [Open Market for NFT based auctions](https://www.blog.xar.network/announcing-technical-collaboration-of-openmarket-and-xar-network/)
*   Nov 29 2019 Open validator participation
*   Dec 5 2019 [Upgrade to hub_2](https://www.blog.xar.network/xar-dora-hub-2-changelog-03-12-2019/)
*   Dec 18 2019 Over [$1,000,000 worth of assets on-chain, over $500k CSDT minted, over $300k CSDT staked](https://twitter.com/xarnetwork/status/1207286330557943808)
*   Dec 18 2019 15 public validators, scheduled [hub_3 upgrade](https://github.com/xar-network/xar-network/tree/hub_2_invariants/x/csdt/spec)
*   Jan 2020 Hub_3 upgrade ~ including [synthetic trading & coinswap](https://www.blog.xar.network/interacting-with-xar-modules/)
*   Feb 2020 Synthetics trading
*   Mar 2020 DEX trading
*   Mar 2020 Ledger Support
*   Apr 2020 [CBDC](https://www.blog.xar.network/central-bank-digital-currency/) MVP
*   Sep 2020 CBDC Deployment

### Necessity of a new native coin

Premined tokens can't be used as they break the economics of stable, sustainable, non-inflationary staking. This rules out all current existing tokens. But we also did not want to do an ICO, or raise any funds, and so we incorporated popular and existing cryptocurrencies to provide them additional value and utility.

### Project Competitors

Crypto: MakerDAO, Uniswap, Compound, Synthetixs

While the following is an inaccurate analogy, we find it is an effective way to explain the difference. With ETH moving to proof of stake, CSDT is equivalent to Staking ETH, this ETH is made available as liquidity to MakerDAO, Uniswap, Compound and Synthetixs. Sharing liquidity and security, while additionally providing you rewards from tx fees, DAI DSR, Compound interest rates, Uniswap trade fees, and Synthetix trade fees. This consolidated DeFi solution built as a layer 1 instead of a DAPP, allows for lower interest rates for borrowers, with higher yield for stakers / liquidity providers, while sharing on-chain security with DeFi liquidity.

Non-crypto: R3, Hyperledger

Our suite has been built from the last 12 month journey we have had with multiple corporate and 1 central bank. The toolset is built around usability and ease-of-use, with existing solutions like R3, and Hyperleder, these tools and ecosystem components must still be built, we provide them pre-packaged, with regulatory compliance, and even licensing for CSDT as an investment vehicle.

## Product

### Development status

Mainnet was launched in Nov 2019

### Relevant product links

[Xar Explorer](https://explorer.xar.network/)  
[Xar Wallet](https://wallet.xar.network/)  

### Open Source License

Apache-2.0

### Github Repo link

[https://github.com/xar-network](https://github.com/xar-network)

## Features of the coin (CSDT)

### CSDT use cases

*   Stable Staking / Delegating ~ Network Security
*   Transaction fees (0.0025ucsdt / tx)
*   Rebalancing fee (default 30% of debt raised)
*   Auctions (default 0.0025% Maker/Taker)
*   Dex (default 0.0025% Maker/Taker)
*   Synths (default ~0.0025% - 3% Long/Short)
*   Coinswap (default ~0.0025 - 3%) per trade
*   Lending (Utilization % formulate to get interest fee)
*   Stable payments

### Voting Rights via CSDT

There are 3 kinds of proposals in Xar

*   Upgrade proposal
*   Param Change proposal
*   Text Proposal

#### Upgrade Proposal

An upgrade proposal is specific to validators, and allows validators to signal if they are ready to upgrade, if the majority of validators have confirmed they are ready to upgrade, a software upgrade can commence, this is a 1:1 voting relationship with 1 validator having 1 vote.

#### Param Change Proposal

Parameter change proposals allow updates to parameters. There are two classes of parameters, system parameters and feature parameters. System parameters include basic configurations, such as voting period, governance costs, CSDT inflation adjustments. For these changes, validators can vote, and all CSDT stake is registered as voting power, irrespective of the source of asset.

Feature parameters include feature configuration, such as which assets are allowed to trade on the DEX, or coinswap modules, which synthetics can be minted and tracked, which collateral and at what ratio is collateral accepted to create CSDT. These changes are governed by the governance token.

#### Text Proposal

Text proposals are generic or signalling proposals that allow participants to communicate with other validators or governance token holders, this allows to pre-empt upgrades, software changes, or just allows the community to vote on future features, or ecosystem changes that could effect the system. These changes are governed by full delegated stake.

#### Voting Explained

One a proposal has been created and has entered into the voting period. Governance token holders can participate. To vote, you have to have delegated stake. If you have delegated stake, you can vote on a proposal by simply submitting yes or no on a given proposal. This is currently available through the xarcli

```
xarcli tx gov vote <proposal-id> <yes|no> --from <key> --chain-id xar-chain-dora-2
```

This is also available via the REST interfaces, or Javascript SDK.

If a delegator does not vote, they inherit their validators vote. If a validator voted first, a delegator can still override this vote, by submitting a new vote.

### Collateral Sustainable Stable Rewards (CSSR)

Blockchains need to bootstrap their networks. To achieve this, they create inflationary models. Inflation decreases as transactional volume increases, until transactional fees are enough to cover the costs to maintain the network.

CSSR is a mechanism to expedite this and increase rewards for participation in securing the network. In order to understand this, we need to first look at a few traditional models.

#### Proof of Stake

You put collateral (stake) to vouch that you are a non malicious actor and are willing to be slashed (lose stake) should you act maliciously. For doing this, you are rewarded in inflationary stake (the same coin you staked)

#### Collateralized Stable Tokens

The most well known is SAI/DAI by MakerDAO, the concept is as follows;

Users provide collateral (~stake), that collateral is worth an amount of USD (if my collateral is 1 ETH and 1 ETH is worth $200, then my collateral (read stake) is $200). For providing this stake you can mint SAI up to the value of the collateralization ratio. If ETH is 100%, then you can mint $200 worth of SAI

#### Liquidity based lending

The most well known protocol is Compound, the concept is as follows;

Users provide collateral (~stake), that collateral is worth an amount of USD (if my collateral is 1 ETH and 1 ETH is worth $200, then my collateral (read stake) is $200 - Yes, this is the exact same sentence as above). For providing this stake, I can borrow other assets that other users staked. I would like to borrow BTC, and I can borrow 0.02 BTC if BTC was $10,000 and my collateral ratio was 100%

#### Collateral Sustainable Stable Rewards

So what if we put all the above together? What if you could provide stake, that you could earn borrower interest on, while using this to secure the network, and receive rewards in a stable token?

CSSR allows you to take any supported asset, collateralize it, mint Collateralized Stable Debt Tokens (CSDT) from the collateral, and then use this CSDT to stake. Staking allows you access to the fees pool proportional to all stakers.

### On-chain Fees

The system has quite a few fees, so we will go through the straight forward ones first (all fees are controlled via on-chain parameter governance);

*   Rebalancing fee (30% of debt raised), rebalancing fees occur when a CSDT position is liquidated because it is under collateralized. The system takes a percentage of the CSDT raised on the auction and deposits it into the distribution module.
*   Stability fee (2% configured via governance), the stability fee is the base cost to borrow or mint new assets in the system, this percentage is a yearly amount
    *   Minting ucsdt (flat 2%)
    *   Borrowing collateral (Explained below)
*   Interest fee (Utilization ratio of market * 20%, explained below)
*   Transaction fees (0.0025ucsdt per transaction)
*   Slashing (0.0001% for downtime, 5% for double signing)
*   Governance fees for proposals (fixed fees)
*   DEX trading fees (0.0025% Maker/Taker)
*   Coinswap fee (~0.0025% - 3% Maker/Taker)
*   Synthetic fee (~0.0025% - 3% Maker/Taker)

All the fees are distributed to CSDT stakers proportional to their CSDT stake.

### Simulated Staking Rewards

Data Analytics on 21/12/2019

*   IDEX trading volume (24hrs) $300,000
*   IDEX fees 0.2% taker, 0.1% maker
*   IDEX 50% maker, 50% taker
*   Uniswap volume (24hrs) $1,531,500
*   Uniswap fees (0.3%)
*   Synthetix Exchange Volume (24hrs) $8,652,251
*   Synthetix fees (0.3%)
*   Compound total market size $121,134,000
*   Compound yearly supply APR 10.59%

IDEX daily taker fees: $300.00  
IDEX daily maker fees: $150.00  
Uniswap daily fees: $4,594.50  
Synthetix daily fees: $25,956.75  
Compound daily fees: $34,145.45  

Total daily fees: $65,146.70  
Monthly fees: $1,981,547.62  

**Assuming 1% of above liquidity;**  

Assets Staked: $1,211,340.00  
Monthly fees: $19,815.47  
Yearly fees: $237,785.64  
**Yearly APR: 19.62%**  

## Token Economics

### Current Market capitalization (at the time of writing)

[$541,909.91](https://wallet.xar.network/)

### Total coin supply

Debt limit of $25,000,000

### Listed Exchanges

None

### Bootstrapping

As proposed the system will gain equilibrium when it fulfills two requirements;

* On-chain assets (collateral)
* On-chain volume (DeFi modules)

It is unlikely that these will be sufficient for the first year after the launch of the chain, for that purpose the distribution modules can act as a Special Purpose Vehicle (SPV) that accepts donations and provides these donations via a bonded yield ratio. This ratio is currently set at a minimum of 6% and a maximum of 30%. Should there be enough donation rewards or community rewards, these will be distributed to offset the initial lack of liquidity and volume.

Donations are simply transferred to the distribution address and the normal delegation distribution takes care of the validator and delegator distribution ratio.

The ratio of yield is dependent on the target bonded percentage. Currently set to 67%. If the amount of CSDT staked is less than 67% the yield number will increase to the maximum of 30%, should it be greater than 67% this number will decrease to 6%.

The first years interest will be donated by Xar to a maximum of $1,500,000.00

For this reason, specific debt limits have been chosen related to each proposed collateral. With the current debt limits set to $500,000.00 per asset.

### Slashing

Slashing is triggered by negative behavior events, there are two primary events

* Downtime
* Double-signing

If a validator fails to sign at least 500 blocks in a 10,000 block period, they will be slashed and jailed. The slashing penalty is 0.1%.

If a validator double signs a transaction (double spend) they will be slashed and jailed. The double sign penalty is 5%.

These penalties are applied to the full validator stake, including delegations.

## Wallet

### ERC20

No

### Blockchain Explorer

*   [Xar Explorer](https://explorer.xar.network/)

### Web Wallet

*   [Xar Portal](https://portal.xar.network/)
*   [Xar Wallet](https://wallet.xar.network/)

### SDKs

*   [Javascript SDK](https://www.npmjs.com/package/@xar-network/javascript-sdk)
*   [GO SDK](https://github.com/xar-network/go-sdk)

### Coin protocol

Xar is a custom toolchain built on top of the Cosmos SDK which is integrated into Fantom TxFlow & Fantom Lachesis Consensus

### Project team full nodes

There are 3 nodes under management;

*   Fantom Foundation ~ Capped at $30k CSDT minted
*   Xar Enterprise ~ Capped at $30k CSDT minted
*   Xar Network ~ Capped at $30k CSDT minted

## Technical Overview

The following is the high level and technical description of the designed modules

The following contains full technical specifications, below this will be a user friendly summary of each;

*   [Xar Network - Auction](https://github.com/xar-network/spec/blob/master/auction.md)
*   [Xar Network - CSDT](https://github.com/xar-network/spec/blob/master/csdt.md)
*   [Xar Network - Denominations](https://github.com/xar-network/spec/blob/master/denominations.md)
*   [Xar Network - Issue](https://github.com/xar-network/spec/blob/master/issue.md)
*   [Xar Network - Liquidator](https://github.com/xar-network/spec/blob/master/liquidator.md)
*   [Xar Network - Market](https://github.com/xar-network/spec/blob/master/market.md)
*   [Xar Network - NFT](https://github.com/xar-network/spec/blob/master/nft.md)
*   [Xar Network - Oracle](https://github.com/xar-network/spec/blob/master/oracle.md)
*   [Xar Network - Order](https://github.com/xar-network/spec/blob/master/order.md)
*   [Xar Network - Record](https://github.com/xar-network/spec/blob/master/record.md)
*   [Xar Network - Coinswap](https://github.com/xar-network/spec/blob/master/coinswap.md)
*   [Xar Network - Synthetic](https://github.com/xar-network/spec/blob/master/synthetic.md)
*   [Xar Network - Message Types](https://github.com/xar-network/spec/blob/master/types.md)
*   [Xar Network - JSON format](https://github.com/xar-network/spec/blob/master/openapi.md)

### Module Auction

[Full Specification](https://github.com/xar-network/spec/blob/master/auction.md)

Generic module for creating auctions and allowing users to place bids until a timeout is reached

*   StartForwardAuction starts a normal auction. Known as flap in Maker.
*   StartReverseAuction starts an auction where sellers compete by offering decreasing prices. Known as flop in Maker.
*   StartForwardReverseAuction starts an auction where bidders bid up to a maximum bid, then switch to bidding down on price. Known as flip in Maker.
*   StartAuction triggers the creation of an auction on a lot and subtracts coins from the initiator.
*   PlaceBid places a bid on any auction

**Use Cases**

*   Auctions (NFT)
*   CSDT rebalancing auctions

### Module Lending / CSDT

[Full Specification](https://github.com/xar-network/spec/blob/master/csdt.md)

Collateral lending module based on borrowing from liquidity pools and paying liquidity providers with interest.

Users provide liquidity to liquidity pools. This liquidity also acts as collateral. If the user does not borrow against the collateral they receive interest. Interest is calculated based on liquidity to borrowing ratio. The less liquidity available for borrowers the higher the interest rates. Interest is split between all liquidity providers for a given asset. So borrowing interest rates will be higher than liquidity provider interest received.

*   DepositFundFromAddress allows the user to deposit any denom they own as liquidity / collateral

Price values are set in CSDT (explained below, for simplicity sake this is a USD pegged stable coin). Each denom has a set collateral ratio. Assuming BNB at 150%, means you have to provide $1.5 worth of BNB to borrow $1 worth of ETH. It is recommended to over collateralize to avoid liquidation.

*   WithdrawFundToAddress allows the user to take the specified amount from the pool and store into the given account balance as long as they have sufficient collateral.

Interest is accrued every block or 10 seconds, whichever is longer.

DistributeReward distributes the given reward between all the funders

**Use cases**

*   Decentralized collateralized lending, required for decentralized shorting solutions

### Module CSDT / Decentralized Stable Tokens

[Full Specification](https://github.com/xar-network/spec/blob/master/csdt.md)

Collateralized Stable Debt Tokens (CSDT) that are asset pegged (asset is USD, but can any other asset, BNB for example).

Similar to compound, but non-interest bearing for liquidity providers (currently, this will be enhanced with interest bearing accounts from Module Compound in the future as these are shared liquidity pools)

Allows the creation of CSDT from multi asset collateralization. Assets supported are set via governance and genesis. Recommended BTC, ETH, BNB, and potentially some stable coins.

Users provide collateral. The collateral has price oracles that submit the current value. Users can then withdraw debt (CSDT) equal to their risk appetite or liquidation. The closer to 100% of the collateral value the closer the liquidation point becomes.

Once collateral is no longer enough to support the debt, the lot goes up for rebalancing and eventually auction.

Should the collateral value increase, more debt can be withdrawn against it.

CSDT is the recommended supported staking token for the chain, as it supports multiple assets.

Module supports setting global debt limits as well as per asset debt limits to minimize volatility risk in certain assets

Debt Limits, Collateral assets accepted, and collateralized ratio can all be controlled via governance.

**Use Cases**

*   Multi asset staking tokens
*   Collateralized debt (NFT or other)
*   Can collateralized debt into collateralized debt (CDO)

### Module Escrow

Allows for the creation of account based escrow locks. Three types are supported, classic 2 party deposit escrow, future escrow and lock based escrow.

Deposit - two parties need to deposit a prefixed value, and if both parties have matched the deposit funds are swapped.

Future - based on a time based trigger.

Users can create lock boxes to deposit denoms into, these boxes have set conditions, either time, multi party, or oracle conditions to release. The box itself is a tradeable asset and can be used as a derivative of the underlying asset.

**Use Cases**

*   Escrow
*   Futures
*   Forwards
*   Options

### Module Issue

[Full Specification](https://github.com/xar-network/spec/blob/master/issue.md)

Allows for the creation of ERC20 standard mapped token issuance with fixed (governance controlled) creation and management fees.

CreateToken allows the creation of a token, the denom itself is not reserved for the symbol, but instead an incrementing ID prefixed, for example bnb128e12c while the metadata preserves the symbol, for example FTM

*   Mint allows mintable tokens to be minted, only if the token is created as a mintable asset
*   BurnOwner allows the owner to burn tokens they hold
*   BurnHolder allows the token owner to burn tokens from another address
*   Freeze allows the owner to lock transfers from an address (In, Out, or In & Out)
*   TransferOwnership allows a token owner to transfer ownership to another address
*   Approve allows a token holder to approve another account to use up to a certain limit of tokens in the account
*   IncreaseApproval allows the token holder to increase the token limit set in Approve
*   DecreaseApproval decreases the allowance
*   SendFrom allows the owner to transfer tokens from another address

Parameters per token are as follows;

*   Name
*   Symbol
*   TotalSupply
*   Description
*   BurnOwnerDisabled
*   BurnHolderDisabled
*   BurnFromDisabled
*   MintingFinished
*   FreezeDisabled

Global parameters (set via governance) are as follows;

*   CreateFee
*   MintFee
*   FreezeFee
*   BurnFee
*   BurnFromFee
*   TransferOwnerFee
*   DescribeFee

### Module Liquidator

[Full Specification](https://github.com/xar-network/spec/blob/master/liquidator.md)

The liquidator module settles bad debt from undercollateralized CSDT’s by seizing them and raising funds through auctions.

*   SeizeAndStartCollateralAuction pulls collateral out of a CSDT and sells it in an auction for CSDT. Excess collateral is goes back to the contract
*   StartDebtAuction sells off minted gov (native) tokens to raise set amount of stable coin (if collateral needs to be bought to keep the price of CSDT stable)
*   SettleDebt removes equal amounts of debt from the liquidators reserves 

Global parameters allows governance to set max auction debt sizes for removed collateral (to ensure smaller lots for bidding)

### Module Market

[Full Specification](https://github.com/xar-network/spec/blob/master/market.md)

The market module creates new markets on the DEX, and allows the Order module to trade against.

Global parameters via governance set the acceptable markets for DEX trading

**Use cases**

*   Trading
*   Swaps
*   Liquidity

### Module Order

[Full Specification](https://github.com/xar-network/spec/blob/master/oracle.md)

Order module allows user to place BID and ASKS on the Market module

*   PlaceBid places a BID or ASK in the given market ID
*   CancelBID cancels a BID with a given BID ID

**Use cases**

*   Trading


### Module NFT

[Full Specification](https://github.com/xar-network/spec/blob/master/nft.md)

Allows for the creation of Non Fungible Token collections and Non Fungible Tokens (NFTs)

MintNFT creates a new NFT object with a collection and owner(s)

**Use cases**

*   Debt Issuance
*   Debentures

### Module Oracle

[Full Specification](https://github.com/xar-network/spec/blob/master/oracle.md)

Allows a group of white-listed oracles to post price information of specific assets that are tracked by the protocol.

*   AddOracle allows governance to add additional white-listed oracles
*   AddAsset adds an asset to track it’s price / value
*   SetPrice allows an Oracle to submit information with regards to the tracking value

After each block all submitted prices are aggregated and a median (weighted by stake) value is created as the current price.

### Module Record (Proof of Existence)

[Full Specification](https://github.com/xar-network/spec/blob/master/record.md)

Allows the creation of proof as an immutable record. 

*   CreateRecord creates a record set, for example University Certificates
*   AddRecord allows the storing of a record with metadata. Such as a unique certificate

**Use cases**

*   Luxury good proofs
*   Certification proofs
*   Anti fraud mechanism

### Module Coinswap

[Full Specification](https://github.com/xar-network/spec/blob/master/coinswap.md)

Generic system coinswap protocol. Users can provide liquidity and set pool based swap ratios.

*   AddLiquidity allows a user to add liquidity to a pool. User can specify the token they wish to swap for.
*   Swap allows a user to swap from a liquidity pool for the swap requested asset for the counter pool.

This allows swaps based on liquidity ratio in the pool, so if the pool is 100:1 and you add 100, you can withdraw 1.

Supported swap markets are controlled via governance.

### Module Synthetic

[Full Specification](https://github.com/xar-network/spec/blob/master/synthetic.md)

Allows the minting, selling, and buying of synthetic assets. Supported assets are controlled via governance.

*   MintSynthetic allows the creation of synthetics to allow shorting
*   BuySynthetic allows buying of synthetic assets
*   SellSynthetic allows selling of synthetic assets

All available assets are controlled via governance

**Use cases**

*   No liquidity limits trading
*   Shorting mechanisms

### DEX Matching Engine

The matching engine uses batch auctions to execute orders. Batch auctions reduce the impact of frontrunning on exchanges. According to this paper [https://arxiv.org/abs/1904.05234](https://arxiv.org/abs/1904.05234) frontrunning on blockchains occur as a result of priority gas auctions. Batch auctions avoid this problem. The engine is based off of the batch auction engine described in this paper [https://faculty.chicagobooth.edu/eric.budish/research/HFT-FrequentBatchAuctions.pdf](https://faculty.chicagobooth.edu/eric.budish/research/HFT-FrequentBatchAuctions.pdf)

This process runs at  the end of every block for every market

1. All orders for the given market are collected

2. Orders beyond their time-in-force are cancelled (based on blocks, maximum 600 blocks, ~40 hours)

3. Orders are placed into separate lists by market side, and aggregate supply and demand curves are calculated.

4. The engine discovers the price at which the aggregate supply and demand curves cross, which yields the clearing price. If there is a horizontal cross - i.e., two prices for which aggregate supply and demand are equal - then the clearing price is the midpoint between the two prices.

5. IF both sides of the market have equal volume, then all orders are completely filled. If one side has more volume than the other, then the side with higher volume is rationed pro-rate based on how much its volume exceeds the other side. For example, if aggregate demand is 100 and aggregate supply is 90, then every order on the demand side of the market will be matched 90%.

Order sorting is based on price, and order ID. Because rationing happens pro-rata, fractional assets below the smallest representable amount may be included. To avoid this pro-rata amounts are rounded up to the nearest whole asset.

The matching engine ends when all volume is exhausted.

Example;


<table>
  <tr>
   <td>
   </td>
   <td><strong>Bids</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td><strong>Asks</strong>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td><strong>ID</strong>
   </td>
   <td><strong>Price</strong>
   </td>
   <td><strong>Volume</strong>
   </td>
   <td><strong>ID</strong>
   </td>
   <td><strong>Price</strong>
   </td>
   <td><strong>Volume</strong>
   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
1</p>

   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
2</p>

   </td>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
3</p>

   </td>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
25</p>

   </td>
   <td><p style="text-align: right">
4</p>

   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
5</p>

   </td>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
25</p>

   </td>
   <td><p style="text-align: right">
6</p>

   </td>
   <td><p style="text-align: right">
11</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
7</p>

   </td>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
</table>


We collect the volume distribution


<table>
  <tr>
   <td><strong>Price</strong>
   </td>
   <td><strong>Bid Vol</strong>
   </td>
   <td><strong>Ask Vol</strong>
   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
200</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
200</p>

   </td>
   <td><p style="text-align: right">
200</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
11</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
300</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
300</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
   <td><p style="text-align: right">
400</p>

   </td>
  </tr>
</table>


To explain the above, look at the first table, the lowest price point is 8, there are 4 bids that are > 8, those 4 bids have a total volume of 100+25+25+50 = 200, so the bid volume for 8 is 200. The lowest bid is 10, so at 11, there are only 3 bids > 11, and that is 25+25+50 = 100.

The volume crossover point is at price 10 (200 bid volume = 200 ask volume), so this becomes the clearing price. Since both the bid volume and the ask volume are equal, all bid orders with a price greater than or equal to 10 will be matched completely, and all ask orders with a price equal to or less than 10 will be matched completely. 

Next, let's look at a less elegant example;


<table>
  <tr>
   <td>
   </td>
   <td><strong>Bids</strong>
   </td>
   <td>
   </td>
   <td>
   </td>
   <td><strong>Asks</strong>
   </td>
   <td>
   </td>
  </tr>
  <tr>
   <td><strong>ID</strong>
   </td>
   <td><strong>Price</strong>
   </td>
   <td><strong>Volume</strong>
   </td>
   <td><strong>ID</strong>
   </td>
   <td><strong>Price</strong>
   </td>
   <td><strong>Volume</strong>
   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
1</p>

   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
2</p>

   </td>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
3</p>

   </td>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
4</p>

   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
5</p>

   </td>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
   <td><p style="text-align: right">
6</p>

   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
7</p>

   </td>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
11</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td>-
   </td>
   <td>-
   </td>
   <td>-
   </td>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
</table>



<table>
  <tr>
   <td><strong>Price</strong>
   </td>
   <td><strong>Bid Vol</strong>
   </td>
   <td><strong>Ask Vol</strong>
   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
8</p>

   </td>
   <td><p style="text-align: right">
350</p>

   </td>
   <td><p style="text-align: right">
100</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
10</p>

   </td>
   <td><p style="text-align: right">
350</p>

   </td>
   <td><p style="text-align: right">
200</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
11</p>

   </td>
   <td><p style="text-align: right">
250</p>

   </td>
   <td><p style="text-align: right">
300</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
12</p>

   </td>
   <td><p style="text-align: right">
250</p>

   </td>
   <td><p style="text-align: right">
300</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
14</p>

   </td>
   <td><p style="text-align: right">
50</p>

   </td>
   <td><p style="text-align: right">
400</p>

   </td>
  </tr>
</table>


Crossover at price 11 and 12 (same aggregate supply and demand). The midpoint is 11.50, and this is chosen as the clearing price (to be equal to both buyers and sellers)

The aggregate supply exceeds the aggregate demand, the supply side will be rationed 83.33%. Orders 2, 4, 6, and 8 will be matched on the supply side. Order of execution is 2, 4, 6, 8 because:

1. First sort criteria is the price

2. Second sort criteria is the ID of the order (time at which it hit the order book)


<table>
  <tr>
   <td><strong>ID</strong>
   </td>
   <td><strong>Match Amount</strong>
   </td>
   <td><strong>Available Volume</strong>
   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
2</p>

   </td>
   <td>CEIL(100*0.83333) = 84
   </td>
   <td><p style="text-align: right">
250-84 = 166</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
4</p>

   </td>
   <td>CEIL(50*0.83333) = 42
   </td>
   <td><p style="text-align: right">
166-42 = 124</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
6</p>

   </td>
   <td>CEIL(50*0.83333) = 42
   </td>
   <td><p style="text-align: right">
124-42 = 82</p>

   </td>
  </tr>
  <tr>
   <td><p style="text-align: right">
8</p>

   </td>
   <td>CEIL(100*0.83333) = 84
   </td>
   <td><p style="text-align: right">
82 - 84 > 0 = 0</p>

   </td>
  </tr>
  <tr>
   <td>
   </td>
   <td><strong>Total: 250</strong>
   </td>
   <td>
   </td>
  </tr>
</table>


So a few important things to note here;

1. The input value to the contract would be the clearing price, in example 1 this would be 10 in example 2 this would be 11.5

2. The quantity would be the aggregate matched volume and not necessarily the actual bid value.

So looking at example 2;

Order 2 would match with order 3 for price 11.5 and quantity 84

Order 4 would match with order 3 for price 11.5 and quantity 16 and order 5 for price 11.5 and quantity 26

Order 6 would match with order 5 for price 11.5 and quantity 42

Order 8 would match with order 5 for price 11.5 and quantity 32 and order 7 for price 11.5 and quantity 50


## Xar FAQ

- [Users](#users)  
- [User Basics](#user-basics)  
- [User CSDT](#user-csdt)  
- [User Auctions](#user-auctions)  
- [User Trading](#user-trading)  
- [User Lending](#user-lending)  
- [User Liquidity Pools](#user-liquidity-pools)  
- [User Issuing Tokens](#user-issuing-tokens)  
- [User Issuing NFTs](#user-issuing-nfts)  
- [User Record Proofs](#user-record-proofs)  
- [Developers](#developers)  
- [Developer Blockchain](#developer-blockchain)  
- [Developer JavaScript / NodeJS](#developer-javascript--nodejs)  
- [Developer Web / HTTPS](#developer-web--https)  
- [Validators](#validators)  
- [General](#general)  

## Users

### User Basics

#### Q: How to create a wallet?
Can currently be done via the [CLI]( https://xar-network.github.io/xar-network/installation.html), [javascript-sdk]( https://www.npmjs.com/package/@xar-network/javascript-sdk), [Xar Wallet](https://wallet.xar.network) (non custodial), or [Xar Portal](https://portal.xar.network) (custodial)

#### Q: How to transfer funds from erc20/bep2 to Xar?
[Fantom Bridge](https://bnbridge.exchange)

#### Q: How to confirm that you received funds?
[Xar Explorer](https://explorer.xar.network)

### User CSDT

#### Q: What is CSDT and how does it work?
[Xar Network staking explained](https://www.blog.xar.network/xar-network-staking-explained/)

#### Q: What is ucsdt and uftm?
USD and FTM 1:1,000,000 so 1FTM = 1,000,000uftm

#### Q: How to mint ucsdt from uftm?
You can mint, via the [CLI]( https://xar-network.github.io/xar-network/installation.html), [javascript-sdk]( https://www.npmjs.com/package/@xar-network/javascript-sdk), [Xar Wallet](https://wallet.xar.network), or [Xar Portal](https://portal.xar.network)

#### Q: How to calculate how much CSDT I can create?
[Xar Wallet](https://wallet.xar.network) has a calculator

### User Staking

#### Q: How much staking rewards will I get?
[Xar Wallet](https://wallet.xar.network) has a calculator

#### Q: How much is currently staked?
[Xar Wallet](https://wallet.xar.network) shows the current staked data, you can also view validators on [Xar Explorer](https://explorer.xar.network)

## Developers

#### Q: Where can I find general resources?
[Xar Resources]( https://xar-network.github.io/awesome/)

### Developer Blockchain

#### Q: How do I install Xar?
[Installing the Xar application]( https://xar-network.github.io/xar-network/installation.html)

#### Q: How do I run a testnet?
[Setup your own Xar testnet]( https://xar-network.github.io/xar-network/deploy-testnet.html)

### Developer JavaScript / NodeJS

#### Q: How can I interact with the chain?
[JavaScript-SDK]( https://www.npmjs.com/package/@xar-network/javascript-sdk)

#### Q: Where can I find code samples?
[JavaScript Examples]( https://xar-network.github.io/examples/)

#### Q: What functions are currently supported?
[Function coverage]( https://github.com/xar-network/javascript-sdk/blob/master/__tests__/client.test.js)

### Developer Web / HTTPS

#### Q: Is there an API I can interact with?
[Node REST API](https://node.xar.network)

#### Q: Where can I find documentation in the API?
[Xar Network REST API](https://docs.xar.network)

## Validators

#### Q: How do I install a Xar node?
[Installing the Xar Node]( https://xar-network.github.io/xar-network/)

#### Q: How do I join the mainnet?
[Joining the mainnet]( https://xar-network.github.io/xar-network/join-mainnet.html)

#### Q: What should I know as a validator?
[Validators Overview]( https://xar-network.github.io/xar-network/validators/overview.html)

#### Q: What should I know about security as a validator?
[Validators Security]( https://xar-network.github.io/xar-network/validators/security.html)

## General
[Xar blog](https://www.blog.xar.network/)  
[Xar FAQ](https://xar.network/faqs)  

## Publications

#### [The Economics of Smart Contracts](https://arxiv.org/abs/1910.11143)
Oct 23, 2019

Ethereum is a distributed blockchain that can execute smart contracts, which inter-communicate and perform transactions automatically. The execution of smart contracts is paid in the form of gas, which is a monetary unit used in the Ethereum blockchain. The Ethereum Virtual Machine (EVM) provides the metering capability for smart contract execution. Instruction costs vary depending on the instruction type and the approximate computational resources required to execute the instruction on the network. The cost of gas is adjusted using transaction fees to ensure adequate payment of the network. In this work, we highlight the "real" economics of smart contracts. We show that the actual costs of executing smart contracts are disproportionate to the computational costs and that this gap is continuously widening. We show that the gas cost-model of the underlying EVM instruction-set is wrongly modeled. Specifically, the computational cost for the SLOAD instruction increases with the length of the blockchain. Our proposed performance model estimates gas usage and execution time of a smart contract at a given block-height. The new gas-cost model incorporates the block-height to eliminate irregularities in the Ethereum gas calculations. Our findings are based on extensive experiments over the entire history of the EVM blockchain.

#### [Fast Stochastic Peer Selection in Proof-of-Stake Protocols](https://arxiv.org/abs/1911.04629)
Nov 12, 2019 

The problem of peer selection, which randomly selects a peer from a set, is commonplace in Proof-of-Stake (PoS) protocols. In PoS, peers are chosen randomly with probability proportional to the amount of stake that they possess. This paper presents an approach that relates PoS peer selection to Roulette-wheel selection, which is frequently used in genetic and evolutionary algorithms or complex network modelling. In particular, we introduce the use of stochastic acceptance algorithm [6] for fast peer selection. The roulette-wheel selection algorithm [6] achieves O(1) complexity based on stochastic acceptance, whereas searching based algorithms may take O(N ) or O(logN ) complexity in a network of N peers.

#### [StairDag: Cross-DAG Validation For Scalable BFT Consensus](https://arxiv.org/abs/1908.11810)
Aug 29, 2019

This paper introduces a new consensus protocol, so-called \emph{\stair}, for fast consensus in DAG-based trustless system. In \stair, we propose a new approach to creating local block DAG, namely \emph{x-DAG} (cross-DAG), on each node. \emph{\stair} protocol is based on our Proof-of-Stake StakeDag framework \cite{stakedag} that distinguishes participants into users and validators by their stake. Both users and validators can create and validate event blocks. Unlike StakeDag's DAG, x-DAG ensures that each new block has to have parent blocks from both Users and Validators to achieve more safety and liveness. Our protocol leverages a pool of validators to expose more validating power to new blocks for faster consensus in a leaderless asynchronous system. Further, our framework allows participants to join as observers / monitors, who can retrieve DAG for post-validation, but do not participate in onchain validation.

#### [StakeDag: Stake-based Consensus For Scalable Trustless Systems](https://arxiv.org/abs/1907.03655)
Jul 5, 2019

Trustless systems, such as those blockchain enpowered, provide trust in the system regardless of the trust of its participants, who may be honest or malicious. Proof-of-stake (PoS) protocols and DAG-based approaches have emerged as a better alternative than the proof of work (PoW) for consensus. This paper introduces a new model, so-called \emph{\stakedag}, which aims for PoS consensus in a DAG-based trustless system. We address a general model of trustless system in which participants are distinguished by their stake or trust: users and validators. Users are normal participants with a no assumed trust and validators are high profile participants with an established trust. We then propose a new family of stake-based consensus protocols S, operating on the DAG as in the Lachesis protocol~\cite{lachesis01}. Specifically, we propose a stake-based protocol Sϕ that leverages participants' stake as validating weights to achieve more secure distributed systems with practical Byzantine fault tolerance (pBFT) in leaderless asynchronous Directed Acyclic Graph (DAG). We then present a general model of staking for asynchronous DAG-based distributed systems.

#### [ONLAY: Online Layering for scalable asynchronous BFT system](https://arxiv.org/abs/1905.04867)
May 13, 2019

This paper presents a new framework, namely \emph{\onlay}, for scalable asynchronous distributed systems. In this framework, we propose a consensus protocol Lϕ, which is based on the Lachesis protocol~\cite{lachesis01}. At the core of Lϕ protocol, it introduces to use layering algorithm to achieve practical Byzantine fault tolerance (pBFT) in leaderless asynchronous Directed Acyclic Graph (DAG). Further, we present new online layering algorithms for the evolutionary DAGs across the nodes. Our new protocol achieves determistic scalable consensus in asynchronous pBFT by using assigned layers and asynchronous partially ordered sets with logical time ordering instead of blockchains. The partial ordering produced by Lϕ is flexible but consistent across the distributed system of nodes. We then present the formal model of our layering-based consensus. The model is generalized that can be applied to abstract asynchronous DAG-based distributed systems.

#### [Fantom: A scalable framework for asynchronous distributed systems](https://arxiv.org/abs/1810.10360)
Oct 22, 2018

We describe \emph{Fantom}, a framework for asynchronous distributed systems. \emph{Fantom} is based on the Lachesis Protocol~\cite{lachesis01}, which uses asynchronous event transmission for practical Byzantine fault tolerance (pBFT) to create a leaderless, scalable, asynchronous Directed Acyclic Graph (DAG).
We further optimize the \emph{Lachesis Protocol} by introducing a permission-less network for dynamic participation. Root selection cost is further optimized by the introduction of an n-row flag table, as well as optimizing path selection by introducing domination relationships.

We propose an alternative framework for distributed ledgers, based on asynchronous partially ordered sets with logical time ordering instead of blockchains.

This paper builds upon the original proposed family of \emph{Lachesis-class} consensus protocols. We formalize our proofs into a model that can be applied to abstract asynchronous distributed system.

#### [OPERA: Reasoning about continuous common knowledge in asynchronous distributed systems](https://arxiv.org/abs/1810.02186)
Oct 4, 2018

his paper introduces a new family of consensus protocols, namely \emph{Lachesis-class} denoted by L, for distributed networks with guaranteed Byzantine fault tolerance. Each Lachesis protocol L in L has complete asynchrony, is leaderless, has no round robin, no proof-of-work, and has eventual consensus.

The core concept of our technology is the \emph{OPERA chain}, generated by the Lachesis protocol. In the most general form, each node in Lachesis has a set of k neighbours of most preference. When receiving transactions a node creates and shares an event block with all neighbours. Each event block is signed by the hashes of the creating node and its k peers. The OPERA chain of the event blocks is a Directed Acyclic Graph (DAG); it guarantees practical Byzantine fault tolerance (pBFT). Our framework is then presented using Lamport timestamps and concurrent common knowledge.

Further, we present an example of Lachesis consensus protocol L0 of our framework. Our L0 protocol can reach consensus upon 2/3 of all participants' agreement to an event block without any additional communication overhead. L0 protocol relies on a cost function to identify k peers and to generate the DAG-based OPERA chain. By creating a binary flag table that stores connection information and share information between blocks, Lachesis achieves consensus in fewer steps than pBFT protocol for consensus.





