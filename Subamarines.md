# Alice, Bob, and the Tale of Entwined Submarines

### Abstract

We propose an alternative architecture for white label exchange, which connects with Exchange Union daemon to facilitate
end-to-end trading of digital assets in trustless and decentralised manner.

### Pain points

The previous proposed architecture for white label exchange incorporates the tradeoff of trusting Xchange service providers,
for usability benefit of users not needing to run a full node or light client to be able to trade. This model requires Xchange
service providers to host a hot wallet of user funds, which in turn escalates the security risks and raises the bar for normal
entrepreneurs to be a Xchange service provider. Furthermore, this architecture requires Xchanages to stake up XUC and also control user's XUC in hot wallet. This centralises the architecture and makes it hard to explore the utility of XUC for decentralised governance akin to ZRX token in [0x architecture](https://blog.0xproject.com/governance-in-0x-protocol-86779ae5809e). This proposed model also doesn't work with on-chain wallets, ipso facto, pushing the prospect of widespread adoption further in future.

Our model reduces the maximum user fund lock-up time from 96 hours to 10 minutes (1 confirmation on BTC mainnet).

## Approach

Submarine Swaps lets users send Lightning payments to a middleman on the Lightning Network; that middleman will send a corresponding amount of bitcoin to a regular (on-chain) Bitcoin address. It also works the other way around: users can send regular on-chain payments to the middleman; that middleman will then send a corresponding amount of bitcoin to a receiving Lightning node on the Lightning Network. A submarine swap has an on-chain side that can be on virtually any chain, so the altcoins don’t need to have SegWit or an lightning implementation for this to work. Go Doge! Submarine swaps between on-chain LTC to off-chain BTC haven been successfully [tested](https://twitter.com/alexbosworth/status/1025168088595984384) recently by Alex Bosworth.

Apart from aforementioned on-chain to off-chain swap, it is also possible to implement off-chain to on-chain swaps. Both being hooked up to one other, will result in on-chain to on-chain swaps. This will allow users to swap funds without needing a second layer wallet. Two submarine swaps tangled together can make any permutations of on-chain and off-chain swaps possible. We propose to utilise this novel technology to help us achieve our goal of connecting digital asset exchanges in Exchange Union ecosystem.

This picture depicts our proposed architecture:

![Image](https://github.com/dopetard/Documents/blob/master/pic1.png)

Walli-server is a white label exchange (Xchange) that has a centralised matching engine order book, it is running a XUD full node and connecting to all other XUDs through it. 

The picture below depicts one specific case of tangled subamarine swap that allows off-chain to on-chain exchange of assets. Consider a scenario where Alice is using Walli, but she only has Ethereum in her off-chain wallet. She intends to buy 2000 XUC for her 1 ETH. Alice sends her 1 ETH to walli-server via her off-chain wallet. Walli-server puts on the order to exchange Alice's Ether for XUC via XUD instance. After successful completion of atomic swap, Walli-server has 2000 XUC in it's second layer wallet which should be sent to Alice, but here's a catch - Alice doesn't have enough deposit or want her XUC in layer two walli wallet, so Walli-server uses submarine swap to transfer her XUC on-chain to walli-vault - all this while maintaing the trustless-ness of the system. In the case of walli-server not being able to liquidate those 1 Ether, it initiates the refund via the swap again. The business model made possible by this architecture is also pretty strightforward - walli-server is essentially a submarine swap provider and makes money via swap and routing fees. It is also possible for walli-server to accept limit orders from users. The problem of stale orders can also be mitiagated by constant pruning of order book.




![Image](https://github.com/dopetard/Documents/blob/master/secondpic.png)

### Future work
Chains with high block mining time like BTC (10 minutes for 1 confirmation) makes limit orders to be sent to walli-server via an on-chain wallet unbidden and requires users to take the inevitable volatility into account. Under this model, BTC on-chain limit orders can only be delegated to walli-server via an off-chain lightning wallet.

The XUC governance model utility can also be easy to implement under this model. These are all high level ideas and needs further exploration.  
