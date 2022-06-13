# XBridge Fees

XBridge is a decentralized exchange protocol that provides the ability to perform peer-to-peer exchanges between any blockchains that are supported by the Blocknet Protocol.

***

### Maker Fee <a href="#maker-fee" id="maker-fee"></a>

When creating an order with XBridge, there is no fee other than the transaction fee for the network of the token being sold. This is the same type of fee you would incur if sending this token to another party.

Having no fee to place an order encourages market makers to add liquidity. This also makes it possible to acquire the BLOCK needed to take orders.

***

### Taker Fee <a href="#taker-fee" id="taker-fee"></a>

When accepting an order with XBridge, a static fee of 0.015 BLOCK is charged at the time the order is taken. This fee is charged even if a trade is canceled or fails and is meant to discourage malicious behavior on the network.

In addition to the 0.015 BLOCK fee, there is also the transaction fee for the network of the token being sold. This is the same type of fee you would incur if sending this token to another party.

If the taker asset is BLOCK, there needs to be _at least_ two UTXOs - one or more to cover the 0.015 BLOCK fee and one or more to cover the traded amount.

In a future update, there will be a percent-based fee that’s charged when accepting an order, but the details of this are not yet finalized.

***

### Fees Distribution <a href="#fees-distribution" id="fees-distribution"></a>

100% of trade fees are distributed to Service Node operators for supporting the network.
