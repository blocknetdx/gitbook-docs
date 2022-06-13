# Introduction

The Blocknet Protocol is supported by a network of Service Nodes, which are similar to masternodes but with an increased level of participation. These Service Nodes are used as a DHT network overlay to support [XBridge](https://docs.blocknet.co/protocol/xbridge/introduction), [XRouter](https://docs.blocknet.co/protocol/xrouter/introduction), and [XCloud](https://docs.blocknet.co/protocol/xcloud/introduction) services. In order to support these services, they host full nodes of the blockchains the protocol is compatible with, serve oracle data, verify UTXOs, route communication between blockchains, and perform anti-spam and anti-DOS measures for the network.

<details>

<summary><strong>Explore Blocknet Network to see how many Service Nodes currently support each digital asset, and much, much more...</strong></summary>

Before an asset can be traded on BlockDX, it must be supported by one or more [Service Nodes](https://docs.blocknet.co/service-nodes/introduction). Blocknet community members have created several web based services to make it easy to discover which assets are currently supported by Service Nodes. Some of these websites actually offer much more information about the Blocknet Network than just how many Service Nodes support each digital asset:

* To list all coins currently supported by Service Nodes for trading on BlockDX, open _Tools->Debug Console_in your Blocknet wallet and enter: `dxGetNetworkTokens`. If using the CLI Blocknet wallet, issue the command, `./blocknet-cli dxGetNetworkTokens` from the directory where `blocknet-cli` is kept.
* [CloudChainsServiceExplorer](https://service-explorer.core.cloudchainsinc.com/#/) (Thank you _@lucien_!)
* [BlocknetMonitor](https://www.blocknetmonitor.com/) (Thank you _@walkjivefly_!)
* [BlockDXServiceNodes](https://block.denarius.pro/) (Thank you _@BuzzkillB_!)
* [CryptoCoreExplorer](https://block.ccore.online/) (Thank you Telegram user _@jimwal_!)
* [Raw Volume Data](https://data.blocknet.co/api/v2.0/ticker)

</details>

Service Nodes require 5000 [BLOCK](https://docs.blocknet.co/blockchain/introduction). If seeking to acquire BLOCK, [there are various options available](https://docs.blocknet.co/project/exchanges).

Operating a Service Node should be viewed as a business since the amount of revenue you generate is completely in your control. You can choose to provide as many services as you'd like. The more services you offer and the higher the quality service you provide, the greater the revenue you will be able to produce. You can also invest in your services by advertising them to developers and selling those services to them. You can develop relationships with developers and gather feedback on the type of services that they would find the most valuable and then capitalize on that by offering those services.&#x20;

For XBridge services, the fees for trades are currently set at a static 0.015 BLOCK taker fee per trade and are paid out to a random Service Node that supports **both** of the chains that the trade took place between. In a future update, these fees will be set to a percent of the trade for the taker.

For XRouter and XCloud services, it's a free market model where you are able to specify the amount you want to charge for each call and users get to specify the maximum fee they are willing to pay. The more useful and/or computationally expensive the call, the more valuable it is to the user, and the more you can charge.&#x20;

XCloud service can vary widely and not everything requires coding. For instance, you can setup a plugin file that allows you to offer CoinMarketCap pricing info via your Service Node for developers to use on-chain. You can set this up in a minute without any programming. This is just one example of an extremely useful service for developers. Not only do they want access to this data, but offering it through Blocknet allows them to pay in crypto, which is much simpler than needing to deal with fiat payments paid via on-chain functions.

More documentation will be added here progressively, but if you have any questions in the meantime feel free to ask in our [Discord](https://discord.gg/vGa7GeCu8B).
