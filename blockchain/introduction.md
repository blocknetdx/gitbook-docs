# Introduction

BLOCK is the utility token that powers the Blocknet Protocol. Fees are paid in BLOCK when using the network and 100% of those fees are distributed to Service Nodes for supporting the network and infrastructure. Normal transaction fees on the network are also paid in BLOCK and awarded to stakers. If seeking to acquire BLOCK, [there are various options available](https://docs.blocknet.co/project/exchanges).

***

### BLOCK Specifications <a href="#block-specifications" id="block-specifications"></a>

| BLOCK Details            |                                                                                                                            |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| Creation Date            | October 20th, 2014                                                                                                         |
| Release Method           | ITO, No Premine                                                                                                            |
| Proof Type               | <p>Proof of Work (PoW): blocks 0-2000 (ended) <br>Proof of Stake (PoS): blocks 2001+ (current)</p>                         |
| Algo                     | Quark                                                                                                                      |
| Block Time               | 60 seconds                                                                                                                 |
| Block Reward             | 1.0 BLOCK                                                                                                                  |
| Superblock               | Up to 40,000 BLOCK                                                                                                         |
| Difficulty               | Adjusted per block, currently 7,788                                                                                        |
| Staking Requirement      | No minimum                                                                                                                 |
| Service Node Requirement | 5000 BLOCK                                                                                                                 |
| Circulation              | [Currently 8,973,656 BLOCK](https://chainz.cryptoid.info/block/)                                                           |
| Max Supply               | No maximum supply (PoS), but there is a maximum to inflation                                                               |
| Circulation Lockup       | <p>Average lockup is ~45% due to Service Node collateral <br>Average lockup is ~60% when also considering staked funds</p> |

***

### Scaling <a href="#scaling" id="scaling"></a>

The Blocknet Protocol is fast and the capacity of the protocol increases with its user base. Since order broadcast and order matching are completely decentralized, there are no bottlenecks other than the ones which lie with users, namely their local internet connections. In addition though, there is a shared capacity in the broadcasting system, which is extremely high. Here is a [relevant quotation from a Bitcoin wiki](https://en.bitcoin.it/wiki/Scalability#Scalability\_targets):&#x20;

<details>

<summary>Bitcoin Wiki</summary>

Let's assume an average rate of 2000tps, so just VISA. Transactions vary in size from about 0.2 kilobytes to over 1 kilobyte, but it's averaging half a kilobyte today.&#x20;

That means that you need to keep up with around 8 megabits/second of transaction data (2000tps \* 512 bytes) / 1024 bytes in a kilobyte / 1024 kilobytes in a megabyte = 0.97 megabytes per second \* 8 = 7.8 megabits/second.&#x20;

This sort of bandwidth is already common for even residential connections today, and is certainly at the low end of what colocation providers would expect to provide you with.

When blocks are solved, the current protocol will send the transactions again, even if a peer has already seen it at broadcast time. Fixing this to make blocks just list of hashes would resolve the issue and make the bandwidth needed for block broadcast negligible. So whilst this optimization isn't fully implemented today, we do not consider block transmission bandwidth here.&#x20;

</details>

***

### BLOCK Inflation <a href="#block-inflation" id="block-inflation"></a>

While there is no maximum limit due to the Blocknet blockchain being Proof of Stake, there is a limit to the amount that can be minted per period (limited inflation). This means that over time the inflation rate decreases as the circulation increases and the amount of BLOCK minted remains constant. Below are 2 sets of data that demonstrate this.

**Lower Bound of Inflation**

In this first set of data, the inflation rate displayed takes into account **just block rewards**. The below data represents the minimum inflation possible.

{% embed url="https://docs.google.com/spreadsheets/d/e/2PACX-1vRTbCrSUOV9epKU0oB80iiyfZesLCPTCjt3e7laywu69X0os14tb9lLtb_XEDUptg/pubhtml/sheet?gid=493878028&headers=false" %}
View data
{% endembed %}

{% embed url="https://docs.google.com/spreadsheets/d/e/2PACX-1vRTbCrSUOV9epKU0oB80iiyfZesLCPTCjt3e7laywu69X0os14tb9lLtb_XEDUptg/pubchart?format=interactive&oid=255649752" %}
View data
{% endembed %}

**Upper Bound of Inflation**

In this second set of data, the inflation rate displayed takes into account **both block rewards and the maximum** [**Superblocks**](https://docs.blocknet.co/governance/introduction#superblock) **amount**. It's important to note that the Superblock does not need to mint the full 40,000 BLOCK so in reality the inflation will likely never reach these levels. The below data represents the maximum inflation possible.

{% embed url="https://docs.google.com/spreadsheets/d/e/2PACX-1vRTbCrSUOV9epKU0oB80iiyfZesLCPTCjt3e7laywu69X0os14tb9lLtb_XEDUptg/pubhtml/sheet?headers=false&gid=974145469" %}
View data
{% endembed %}

{% embed url="https://docs.google.com/spreadsheets/d/e/2PACX-1vRTbCrSUOV9epKU0oB80iiyfZesLCPTCjt3e7laywu69X0os14tb9lLtb_XEDUptg/pubchart?oid=1635035440&format=interactive" %}
View data
{% endembed %}
