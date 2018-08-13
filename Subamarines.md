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

Submarine Swaps is a concept that lets users send Lightning payments to a middleman on the Lightning Network; that middleman will send a corresponding amount of bitcoin to a regular (on-chain) Bitcoin address. It also works the other way around: users can send regular on-chain payments to the middleman; that middleman will then send a corresponding amount of bitcoin to a receiving Lightning node on the Lightning Network. A submarine swap has an on-chain side that can be on virtually any chain, so the altcoins don’t need to have SegWit or an LN implementation for this to work. Go Doge! Submarine swaps between on-chain LTC to off-chain BTC haven been successfully [tested](https://twitter.com/alexbosworth/status/1025168088595984384) recently by Alex Bosworth.

Apart from aforementioned on-chain to off-chain swap, it is also possible to implement off-chain to on-chain swaps. Both being hooked up to one other, will result in on-chain to on-chain swaps. This will allow users to swap funds without needing a second layer wallet. Two submarine swaps tangled together can make any permutations of on-chain and off-chain swaps possible. We propose to utilise this novel technology to help us achieve our goal in Exchange Union ecosystem.

This picture depicts our proposed architecture:

![Image](https://github.com/dopetard/Documents/blob/master/pic1.png)

Walli-server is a white label exchange (Xchange) that has a centralised matching engine order book, it is running a XUD full node and connecting to all other XUDs through it. There are users connected to walli-server via a client app. The client app can be an on-chain or off-chain wallet. The user sends a 100 Ether market order that expires in 45 seconds to Walli-server via a submarine swap, walli-server liquidates that 100 Ether for 1000 BNB by using decentralised layer two trading powered by XUD. The walli-server swaps 1000 BNB back to user via an on-chain to off-chain submarine swap. In the case of walli-server not being able to liquidate those 100 Ether within 45 seconds, it initiates the refund via the swap again. Walli-server is essentially a submarine swap provider and makes money via routing fees. It is also possible for walli-server to accept limit orders from users. The front running isn’t a problem because walli-server is running a centralised matching engine orderbook and queuing the orders itself. The problem of stale orders can also be mitiagated by constant pruning of order book.

The picture below depicts the one specific case of tangled subamarine swap that allows on-chain to on-chain exchange of assets.

![Image](https://github.com/dopetard/Documents/blob/master/pictwo.png)

### Future work
Chains with high block mining time like BTC (10 minutes for 1 confirmation) wouldn’t allow for BTC limit orders to be sent to walli-server via an on-chain wallet. Under this model, BTC on-chain limit orders can only be delegated to walli-server via an off-chain lightning wallet.

We also propose to consider integrating BTCD into XUD itself, it will allow market makers to send market orders directly to XUD via an on-chain wallet by bypassing white label exchanges and save lots of fees. It will also help liquidate the base BTC pair market in the XU ecosystem and allow for more decentralisation of XUC (since market makers will need to stake it). The XUC governance model utility can also be easy to implement under this model. These are all high level ideas and needs further exploration.  
