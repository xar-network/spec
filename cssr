## Collateral Sustainable Stable Rewards (CSSR)

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

#### Fees explained

The system has quite a few fees, so we will go through the straight forward ones first (all fees are controlled via on-chain parameter governance);

- Liquidation fee (1% of lot), liquidation fees occur when a CSDT position is liquidated because it is under collateralized. The system takes a percentage of the CSDT raised on the auction and deposits it into the distribution module.
- Stability fee (2% configured via governance), the stability fee is the base cost to borrow or mint new assets in the system, this percentage is a yearly amount
  - Minting ucsdt (flat 2%)
  - Borrowing collateral (Explained below)
- Interest fee (Stability fee + Utilization ratio of market * 20%, explained below)
- Transaction fees (~%)
- Slashing (~%)
- Governance fees for proposals (~%)
- Dex trading fees (0.005% of trade)
- Coinswap fee (~%)
- Synthetic Short fee (~%)

Borrowing collateral interest fee;

Fee on borrowed assets

Utilization ratio of market:

Borrowed amount / Borrowed amount + Lending amount

Example

90 borrowed 10 remaining = 90 / 90 + 10 (90%)  
10 borrowed 90 remaining = 10 / 10 + 90 (10%)  

Borrowing interest rate:

Stability fee + (Utilization * 20%)

Example

2% + (90% * 20%) = 20%  
2% + (10% * 20%) = 4%  

All the fees are distributed to CSDT stakers proportional to their CSDT stake.
