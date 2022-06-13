# aaBLOCK Token

### What is aaBLOCK? <a href="#what-is-aablock" id="what-is-aablock"></a>

**aaBLOCK** is a "wrapped" version of the BLOCK coin. It's the same BLOCK we know and love, but with a wrapper around it which allows it to exist on the Avalanche blockchain as an ARC20 token. Just as a man needs to wear a spacesuit to exist on the moon, so does BLOCK need to don a wrapper to exist on a non-native blockchain.

By design, there is exactly one BLOCK coin wrapped inside each aaBLOCK token. In other words, there is a 1:1 mapping between BLOCK and aaBLOCK at the bridge where wrapping and unwrapping take place. This does not mean the price of aaBLOCK will always be exactly the same as the price of BLOCK. Just as the price of BLOCK can be different from one exchange to another, so too can the price of aaBLOCK be different from one exchange to another. Likewise, the price of aaBLOCK on one exchange can be different from the price of BLOCK on another exchange.

The only thing guaranteed about the price of aaBLOCK is that it will be exactly equal to the price of BLOCK at the wrapping/unwrapping bridge. This one guarantee, however, can create arbitrage opportunities for anyone who notices a discrepancy between the price of aaBLOCK on one exchange and the price of BLOCK on another exchange. For example, if aaBLOCK is selling for $150 / aaBLOCK on Pangolin, while BLOCK is simultaneously selling for only $125 / BLOCK on BlockDX, one can buy BLOCK on BlockDX, wrap it into aaBLOCK, then sell the aaBLOCK on Pangolin for a $25 / BLOCK profit!

### How to buy/trade aaBLOCK on Pangolin <a href="#buytrade-aablock-on-pangolin" id="buytrade-aablock-on-pangolin"></a>

1. [Setup & Fund MetaMask1 w/ AVAX](https://pangolin.exchange/tutorials/getting-started/) (skip the part about adding **PNG** token)
2. Add **aaBLOCK** token to MetaMask:
   1. Open MetaMask1 and scroll to the bottom of your Assets list.
   2. Click "Add Token"
   3. Select "Custom Token."
   4. Paste `0xC931f61B1534EB21D8c11B24f3f5Ab2471d4aB50` into Token Contract Address
   5. Click "Next."
   6. Click "Add Tokens."
3. To buy/trade aaBLOCK on Pangolin:
   1. Visit [Pangolin aaBLOCK](https://app.pangolin.exchange/#/swap?outputCurrency=0xc931f61b1534eb21d8c11b24f3f5ab2471d4ab50)
   2. Make sure MetaMask1 is unlocked and connected to Pangolin.
   3. Choose the swap direction as desired (WAVAX=>aaBLOCK or aaBLOCK=>WAVAX).
   4. Fill in the desired amount.
   5. Click, "Swap."
   6. Note: WAVAX (Wrapped AVAX) is not exactly the same as AVAX. Swapping WAVAX=>aaBLOCK will work if you only hold AVAX in your MetaMask wallet because AVAX will automatically be wrapped into WAVAX as needed. However, when swapping aaBLOCK=>WAVAX, you may not see the WAVAX you acquire from the swap in your MetaMask wallet (unless you add WAVAX custom token to MetaMask). Instead, you may need to perform an additional step of swapping WAVAX=>AVAX (at a ratio of 1:1). After that, you'll see your AVAX appear in your MetaMask wallet.

#### Redeem aaBLOCK for BLOCK or Bridge BLOCK to aaBLOCK on Anyswap <a href="#redeem-aablock-for-block-or-bridge-block-to-aablock-on-anyswap" id="redeem-aablock-for-block-or-bridge-block-to-aablock-on-anyswap"></a>

1. Make sure MetaMask1 has been set up and funded with some AVAX according to steps 1 & 2 above.
2. Navigate to [Anyswap Bridge](https://v1.anyswap.exchange/bridge)
3. Select _Avalanche Mainnet_ at the top of the Anyswap page, then click "Connect to Wallet" and select, "MetaMask." Make sure MetaMask is unlocked and the network dropdown menu at the top of MetaMask is set to _Avalanche Network_.

**Unbridge aaBLOCK->BLOCK (redeem aaBLOCK for BLOCK)**

1. Ensure your aaBLOCK is in your MetaMask1 wallet.
2. Set up the bridge to go from "aaBLOCK" to "BLOCK" on the _Avalanche Mainnet_.&#x20;
3. Enter the amount of BLOCK you want to redeem.
4. Enter the "Recipient BLOCK address"
5. Click, "Redeem."

![](https://docs.blocknet.co/img/blockchain/aablock-block.png)

**Bridge BLOCK->aaBLOCK**

1. Set up the bridge to go from "BLOCK" to "aaBLOCK" on the _Avalanche Mainnet_.&#x20;
2. Enter the amount of BLOCK you want to bridge
3. Send that amount of BLOCK to the "Deposit BLOCK address"
4. Click "CrossChain Deposit." After your deposit has enough confirmations, you will then have ARC20 aaBLOCK in your MetaMask1 wallet.

![](https://docs.blocknet.co/img/blockchain/block-aablock.png)

**Bridging Fees**[**¶**](https://docs.blocknet.co/blockchain/aablock/#bridging-fees)

There is no fee for bridging BLOCK to aaBLOCK (a.k.a. wrapping BLOCK into aaBLOCK). However, when unwrapping aaBLOCK to redeem the BLOCK inside, there is a 0.1% "gateway" fee, payable in BLOCK. (min gateway fee = 5 BLOCK; min redeem amount = 10 BLOCK). Also, to cover gas fees, users should maintain a small amount of AVAX in their wallets.

#### Add Liquidity on Pangolin <a href="#add-liquidity-on-pangolin" id="add-liquidity-on-pangolin"></a>

1. Visit [Pangolin aaBLOCK Liquidity](https://app.pangolin.exchange/#/add/0xc931f61b1534eb21d8c11b24f3f5ab2471d4ab50/AVAX)
2. Make sure your MetaMask1 wallet contains the aaBLOCK and AVAX you want to add to the liquidity pool.
3. Make sure MetaMask1 is unlocked and connected to Pangolin.
4. Fill in the amount of liquidity you want to add, then click "Supply."

**See Current USD Prices of aaBLOCK on Pangolin at** [**Pangolin aaBLOCK**](https://info.pangolin.exchange/#/token/0xc931f61b1534eb21d8c11b24f3f5ab2471d4ab50)

**1 Note About MetaMask Security**

MetaMask Chrome Browser extension is a convenient wallet to use for interacting with Anyswap and Pangolin. Be aware, however, that it is the target of many scammers, some of whom have written very ingenious malware to steal your MetaMask private keys. The Internet is full of reports of funds being stolen from MetaMask wallets. If you use MetaMask, take prudent safety precautions:

1. Run a good Anti-Virus program, such as Bitdefender, at all times. Configure it to give Web protection for Chrome browsing.
2. Never leave MetaMask unlocked any longer than you must to complete your transactions.
3. Never surf the web in Chrome with MetaMask unlocked, and never unlock MetaMask with tab(s) open to questionable sites. Even if a malicious site is open in a different tab, its malware can still access MetaMask.
4. Only confirm transactions in MetaMask after carefully reading _all_ the details of the transaction. Note, some malware can display fake transaction details on top of parts of the transaction. That's why you need to read _all_ the details of the transaction before confirming it.

### Why aaBLOCK? <a href="#why-aablock" id="why-aablock"></a>

aaBLOCK has been created to improve accessibility to BLOCK

As of this writing, BLOCK is not listed on many high liquidity exchanges. Our own BlockDX has also not yet acheived a high level of liquidity. Even if BlockDX had high liquidity, at present it still requires more setup than is convenient for some potential investors. Furthermore, the exchange on which BLOCK currently has the highest liquidity (Bittrex Global) is not even accessible to investors in the USA. The net result of all this is that those wanting to invest in BLOCK sometimes feel it is inconvenient to do so, or they feel it's difficult to invest in volume at a fair market price.

aaBLOCK will make it possible for people from every country to buy BLOCK (as aaBLOCK) on Pangolin, an easily accessible, easy to use, very high liquidity, decentralized exchange. (Note, aaBLOCK may also be tradable on Anyswap and other exchanges in the future.)

Having purchased aaBLOCK, investors will then have several options of what to do with it:

1. They can HODL it and watch it increase in value over time.
2. They can trade it on Pangolin for some other asset.
3. They can earn steady income with it by adding liquidity to the aaBLOCK/AVAX liquidity pool on Pangolin.
4. They can "unwrap" it. In other words, they can unbridge it back to native BLOCK at a ratio of 1:1. Native BLOCK can then be used for [Blocknet network staking](https://docs.blocknet.co/wallet/staking/) and/or [Blocknet Service Node collateral](https://docs.blocknet.co/service-nodes/introduction/).

### How aaBLOCK? <a href="#how-aablock" id="how-aablock"></a>

BLOCK is wrapped into aaBLOCK, and aaBLOCK is unwrapped to redeem the BLOCK inside at [https://v1.anyswap.exchange/bridge](https://v1.anyswap.exchange/bridge). Management of wrapping and unwrapping is powered by Fusion's [Distributed Control Rights Management (DCRM)](https://www.fusion.org/en/tech/dcrm). DCRM uses a decentralized custodian model which locks BLOCK coins as it wraps them into aaBLOCK, and keeps them securely locked until an equal amount of aaBLOCK is burnt/unwrapped.

***

**For administrative purposes only:**

**aaBLOCK ARC20 token contract address (Do not send any funds here):**

`0xC931f61B1534EB21D8c11B24f3f5Ab2471d4aB50`
