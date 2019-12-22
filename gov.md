## Xar Governance

There are 3 kinds of proposals in Xar

- Upgrade proposal
- Param Change proposal
- Text Proposal

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
