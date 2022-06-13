# Blocknet Overview

### What is Blocknet? <a href="#what-is-blocknet" id="what-is-blocknet"></a>

Blocknet is a blockchain interoperability protocol that enables communication, interaction, and exchange between different public and private blockchains, as well as connect to external off-chain APIs and services via oracles. This exponentially increases the development capabilities and enables a new generation of mature blockchains and services.&#x20;

Blocknet is an open sourced, self-funded, and self-governed project with contributors around the world building an open and collaborative ecosystem.

### Technical Overview <a href="#technical-overview" id="technical-overview"></a>

Blocknet is a Proof-of-Stake (PoS) blockchain with a utility token called [BLOCK](https://docs.blocknet.co/blockchain/introduction). Unlike other currency-focused blockchains, Blocknet is a service-based blockchain comprised of 3 main components:

* [**XRouter**](https://docs.blocknet.co/protocol/xrouter/introduction) - Provides blockchain interoperability for the Blocknet Protocol with a communication layer consisting of a decentralized inter-blockchain SPV client backend that enables the verification of blockchain records without requiring users to download the full blockchain. XRouter allows applications to interface with blockchains on the TCP/IP networking layer, enabling a true Internet of Blockchains. By default, XRouter is compatible with all blockchains.
* [**XBridge**](https://docs.blocknet.co/protocol/xbridge/introduction) - Provides the ability to perform trustless exchange between any [digital assets](https://docs.blocknet.co/resources/glossary/#digital-asset) that is supported by the Blocknet Protocol via APIs. XBridge allows any application to perform decentralized exchange, opening the door to an ecosystem of decentralized trading services. See the [list of compatible assets](https://docs.blocknet.co/protocol/xbridge/compatibility).
* [**XCloud**](https://docs.blocknet.co/protocol/xcloud/introduction) - Provides a decentralized oracle network powered by XRouter. XCloud allows applications to run entirely decentralized by enabling on-chain use of off-chain data, APIs, and services, opening the door to the possibility of monetizable, fully decentralized applications.

The Blocknet Protocol is designed to maximize interoperability between different blockchains through the use of these components. **Just as the internet connected computers, the Blocknet Protocol is critical for blockchains to communicate and realize full potential**.

### Tokenomics <a href="#tokenomics" id="tokenomics"></a>

[BLOCK](https://docs.blocknet.co/blockchain/introduction) is the utility token that powers the Blocknet. Fees are paid in BLOCK when using the network and 100% of those fees are distributed to [Service Nodes](https://docs.blocknet.co/service-nodes/introduction) for supporting the network and infrastructure. Normal transaction fees on the network are also paid in BLOCK and awarded to stakers. If seeking to acquire BLOCK, [there are various options available](https://docs.blocknet.co/project/exchanges).

Blocknet involves multiple economic models with respect to the use of the BLOCK token.

* **Block Rewards** - Blocknet is Proof-of-Stake(PoS) with 1 BLOCK created every minute which is awarded to stakers. Stakers also receive the network transaction fees for the block they have validated. Read more about [staking rewards](https://docs.blocknet.co/wallet/staking/#staking-rewards).
* **Service Fees** - Service Nodes receive 100% of BLOCK fees generated from the use of services on the network, including trades performed via XBridge, interfacing with blockchains via XRouter, and use of microservices via XCloud.
* **Collateral** - BLOCK is required for collateral to operate a Service Node, as well as to use certain services on the network.
* [**Governance**](https://docs.blocknet.co/governance/introduction) - Submitting proposals to the network requires a fee to be paid in BLOCK and proposals can only be voted on by Service Nodes.
* **Transaction Fees** - Transferring funds on the network incurs a transaction fee that's paid in BLOCK and awarded to stakers.

The utility of the BLOCK token increases the buy pressure on the market, while the reward potential of operating a node reduces sell pressure on the market.

### Nodes <a href="#nodes" id="nodes"></a>

The network is powered by two types of nodes:&#x20;

* [**Staking Nodes**](https://docs.blocknet.co/wallet/staking) - Secures the network by staking BLOCK to verify the blockchain. This service earns 100% of block rewards and the fees for transactions in that block.
* [**Service Nodes**](https://docs.blocknet.co/service-nodes/introduction) - Hosts the full nodes of compatible blockchains, serves oracle data, audits interactions, and performs anti-spam and anti-DOS measures for the network. This service earns 100% of fees generated from use of the network's services ([XBridge](https://docs.blocknet.co/protocol/xbridge/introduction), [XRouter](https://docs.blocknet.co/protocol/xrouter/introduction), [XCloud](https://docs.blocknet.co/protocol/xcloud/introduction)).

The following are the requirements to operate each type of node:&#x20;

* [**Staking Nodes**](https://docs.blocknet.co/wallet/staking) - A Staking Node can be operated with any amount of BLOCK, but staking more BLOCK yields more frequent rewards.
* [**Service Nodes**](https://docs.blocknet.co/service-nodes/introduction) - A Service Node requires 5000 BLOCK.

<details>

<summary>Explore Blocknet Network to see how many Service Nodes currently support each digital asset, and much, much more...</summary>

Before an asset can be traded on BlockDX, it must be supported by one or more [Service Nodes](https://docs.blocknet.co/service-nodes/introduction). Blocknet community members have created several web based services to make it easy to discover which assets are currently supported by Service Nodes. Some of these websites actually offer much more information about the Blocknet Network than just how many Service Nodes support each digital asset:

* To list all coins currently supported by Service Nodes for trading on BlockDX, open _Tools->Debug Console_in your Blocknet wallet and enter: `dxGetNetworkTokens`. If using the CLI Blocknet wallet, issue the command, `./blocknet-cli dxGetNetworkTokens` from the directory where `blocknet-cli` is kept.
* [CloudChainsServiceExplorer](https://service-explorer.core.cloudchainsinc.com/#/) (Thank you _@lucien_!)
* [BlocknetMonitor](https://www.blocknetmonitor.com/) (Thank you _@walkjivefly_!)
* [BlockDXServiceNodes](https://block.denarius.pro/) (Thank you _@BuzzkillB_!)
* [CryptoCoreExplorer](https://block.ccore.online/) (Thank you Telegram user _@jimwal_!)
* [Raw Volume Data](https://data.blocknet.co/api/v2.0/ticker)

</details>
