---
pip: <to be assigned>
title: Cash++
author: Mick de Graaf (@mickdegraaf)
discussions-to: <URL>
status: Draft
type: PIEs
created: 2020-03-06
---

<!--You can leave these HTML comments in your merged PIP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new PIPs. Note that an PIP number will be assigned by an editor. When opening a pull request to submit your PIP, please use an abbreviated title in the filename, `pip-draft_title_abbrev.md`. The title should be 44 characters or less.-->


## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the PIP.-->
Tokenised interest bearing cash position which rebalances manually(by the DAO) based on risk across different lending protocols and stable coins.


## Motivation
<!--The motivation is critical for PIPs that want to change the Ethereum protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the PIP solves. PIP submissions without sufficient motivation may be rejected outright.-->
Lots of investment portfolios contain a cash position to reduce risk. In the DeFi ecosystem there is a plethora stable coins, each with their own risks and potential flaws. There are also multiple lending protocols which also have their own risks associated to them. Properly managing your wealth is about maximising your return/risk ratio. Current solutions that automatically rebalance based on interest rate only maximise for returns with catasrophic effects if one of the underlying protocols fails.

## Specification
<!--The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current Ethereum platforms (go-ethereum, parity, cpp-ethereum, ethereumj, ethereumjs, and [others](https://github.com/ethereum/wiki/wiki/Clients)).-->
The Cash++ PIE will be a token which is mintable by supplying the underlying assets. The token is always backed by and redeemable for the underlying assets. Under the hood the Cash++ PIE uses the balancer protocol behind a custom upgradeable proxy. The PieDAO is able to change the weights or underlying assets and trigger a rebalance. When a rebalance is triggered the balancer pool trading is temporarely enabled so that arbitrage traders rebalance the portfolio to the desired weights.

[pie-proxy](https://github.com/pie-dao/pie-proxy)
[proxied-balancer-factory](https://github.com/pie-dao/proxied-balancer-factory) 

## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->
I choose balancer because we think they have a very novel rebalancing mechanism and their smart contracts are very well written and are already audited.

The proxy is used to be able to pause and upgrade the pool on the lowest level and to add some custom functionality with regards to adding and removing liquidity while a pool is not actively trading.

Using the proxy also allows us to later add hooks into the smart contract to do the accounting for the future migration plan of PieDAO.

## Security Considerations
<!--All PIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the life cycle of the proposal. E.g. include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. PIP submissions missing the "Security Considerations" section will be rejected. An PIP cannot proceed to status "Final" without a Security Considerations discussion deemed sufficient by the reviewers.-->

The Cash++ Pie is built to handle possible failure of stable coins and lending protocols by not automatically rebalancing but only doing so when the PieDAO triggers this.

Pauzing can be triggered by a sepperate pauzer address which is elected by the PieDAO. At any time the PieDAO can elect a new pauzer.

We customize functionality on the proxy level to reduce the attack vector compared to writing a more complex manager for the balancer pool.


## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
