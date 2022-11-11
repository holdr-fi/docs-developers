# How Gauges Work

## Voting

Liquidity Mining emissions are distributed among different Gauges according to veBAL voting. **All veBAL voting happens on Ethereum mainnet** whether the pools are on Ethereum, Polygon, Arbitrum, or any other network on which Balancer has been deployed since this writing. veBAL holders can vote for one or more Gauges, choosing the percentage of their voting power to allocate to a specific Gauge.

## Staking

Each pool eligible for Liquidity Mining has a Gauge contract associated with it. In order for Liquidity Providers to be eligible for Liquidity Mining, they must stake their Balancer Pool Tokens (BPTs) in the pool's corresponding Gauge.

## Mainnet vs Alternate Chains

### Mainnet

On Ethereum mainnet, pool gauges get their BAL directly. Since Ethereum is the core network for Balancer Protocol, it is referred to as the `RootChain`.

### Alternate Chains

We use the term `ChildChain` for non-mainnet chains, whether those are Layer 2 solutions, sidechains, etc. After voting on the `RootChain`, liquidity mining tokens are minted by the `RootChainGauge`, and bridged to the respective `ChildChain`s. The tokens are sent to `ChildChainStreamer`contracts and then sent to `RewardsOnlyGauge` contracts. As with the `RootChain`, Liquidity Providers on `ChildChain`s must stake their BPT in a pool's `RewardsOnlyGauge` to be eligible for distributions.

## Multi-Token Liquidity Mining

Each pool's Gauge contract can distribute up to 8 different kinds of tokens. This allows for multiple partners/protocols/DAOs to incentivize a given pool by adding their own tokens.

In order to prevent spam tokens from occupying those 8 slots and blocking out legitimate tokens, Balancer Governance has the power to allow addresses to be able to add tokens to a Gauge using the Authorizer.

## Dividing a pool's LM among LPs

To be eligible for a given pool's BAL emissions, a user must stake their corresponding LP tokens to that pool's gauge. Their share of the BAL emission scales with their proportional stake of LP tokens for that pool.

#### Additional veBAL Boost

On Ethereum, a user's claimable BAL also depends on their amount of veBAL. This extra boost is determined just as [Curve's CRV boost is calculated](https://curve.readthedocs.io/dao-gauges.html#boosting). **Since veBAL balances are not queryable on other chains (Polygon, Arbitrum, etc), pools on those chains do not get this boost.**

## How are Gauges Deployed for a Pool?

Governance has the power to authorize accounts for gauge deployment. Projects interested in proposing pools eligible for voting, please refer to the [instructions on the community forum](https://forum.balancer.fi/t/instructions-overview/2674).

Please note that Balancer [governance approved](https://snapshot.org/#/balancer.eth/proposal/0x63fab7ab9ef5b9579dabb82058b8ea309e39c766d435438b55fff8db7c1f69fd) an Emergency subDAO, that empowers a small group to “kill” pools and gauges in the event of malicious activity and/or potential loss of funds. Ultimately, veBAL holders have the collective power over gauges activity, being able to kill gauges at anytime through governance regular voting process.
