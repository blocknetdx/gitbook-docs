# XRouter Introduction

XRouter provides blockchain interoperability for the Blocknet Protocol with a communication layer consisting of an inter-blockchain SPV client backend, enabling the verification of blockchain records without requiring users to download the full blockchain. This empowers development of lightweight microservice architectures that harness contracts, protocols, and services from other blockchains, laying a foundation for a decentralized API ecosystem.

Since XRouter functions on the TCP/IP level, it is compatible with any network. This includes public and private DLT's, such as Bitcoin, Ethereum, IOTA, and Hyperledger.

Here is a list of current SPV calls:

| Call                   | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| xrGetBlockCount        | Returns a blockchain's block height                   |
| xrGetBlockHash         | Returns a block number's hash                         |
| xrGetBlock             | Returns a block hash's block number                   |
| xrGetBlocks            | Returns block hashes for multiple block numbers       |
| xrDecodeRawTransaction | Returns decoded transaction HEX                       |
| xrGetTransaction       | Returns transaction data for transaction ID           |
| xrGetTransactions      | Returns transaction data for multiple transaction IDs |
| xrSendTransaction      | Submit a signed transaction to the network            |

To use XRouter, see the [XRouter API](https://api.blocknet.co/#xrouter) and [Setup Guide](https://api.blocknet.co/#xrouter-setup).

[Service Nodes](https://docs.blocknet.co/service-nodes/introduction) earn 100% of fees from [XBridge](https://docs.blocknet.co/protocol/xbridge/introduction), XRouter, and [XCloud](https://docs.blocknet.co/protocol/xcloud/introduction) services. If you'd like to operate your own Service Node, see the [Service Node Setup Guide](https://docs.blocknet.co/service-nodes/setup).

### Design <a href="#design" id="design"></a>

The XRouter system utilizes the Service Node network to route calls from the client directly to the respective blockchain. There are 2 types of XRouter calls: submissions and queries.&#x20;

XRouter submissions are calls that involve interactions with a blockchain, such as `xrSendTransaction`. With submissions, the packets are routed from the client to the respective blockchain and a response, if any, is routed back to the client.&#x20;

XRouter queries are calls requesting information from a blockchain, such as `xrGetBlockCount`. With queries, the packets are also routed from the client to the respective blockchain and the response of the information queried is routed back to the client. XRouter queries can require a specific amount of Service Nodes to receive a response from in order to achieve consensus on the final answer.&#x20;

**XRouter Overview**[(view full size image)](https://docs.blocknet.co/img/protocol/xrouter-overview-2.png)

![](https://docs.blocknet.co/img/protocol/xrouter-overview-2.png)

The following diagrams depict the events of an XRouter query and submission. As seen in the diagrams, a "client" refers to software utilizing the Blocknet Protocol, which can be a blockchain, microservice, dApp, mobile app, website, etc.

**XRouter Query**[(view full size image)](https://docs.blocknet.co/img/protocol/xrouter-query.png)

![](https://docs.blocknet.co/img/protocol/xrouter-query.png)

The flow of the diagram is top-to-bottom:

1. The client dispatches a packet for a query via API call to the Service Node network.
2. The Service Nodes supporting the queried blockchain receive the packet.
3. The Service Nodes route the packet of the query to the blockchain.
4. The Service Nodes route the response from the blockchain back to the client.
5. The client receives all responses, as well as a response for a majority consensus on the answer.

**XRouter Submission**[(view full size image)](https://docs.blocknet.co/img/protocol/xrouter-submission.png)

![](https://docs.blocknet.co/img/protocol/xrouter-submission.png)

1. The client dispatches a packet for a submission via API call to the Service Node network.
2. The Service Nodes supporting the desired blockchain receive the packet.
3. The Service Nodes route the packet of the query to the blockchain.
4. If there is a response from the blockchain, the Service Nodes route the response back to the client.

### Namespace <a href="#namespace" id="namespace"></a>

XRouter SPV wallets utlize the `xr::` namespace while [XCloud](https://docs.blocknet.co/protocol/xcloud/introduction) services utilize the `xrs::` namespace. A list of the SPV wallets and services can be viewed using [xrGetNetworkServices](https://api.blocknet.co/#xrgetnetworkservices) and you can pre-connect to the nodes with [xrConnect](https://api.blocknet.co/#xrconnect).

### Node Scoring <a href="#node-scoring" id="node-scoring"></a>

Clients keep a _local_ score of each Service Node (network-wide repuation system is planned). When a Service Node reaches a score of `-200`, the Service Node will be banned by the client for a 24hr period. After this 24hr period, the Service Node will start with a score of `-25`. The ban score threshold can be adjusted using the `xrouterbanscore` setting in `blocknet.conf` (see [setup](https://api.blocknet.co/#xrouter-setup)). This scoring used for both XRouter and [XCloud](https://docs.blocknet.co/protocol/xcloud/introduction).

| Action                                | Change in Score     |
| ------------------------------------- | ------------------- |
| Failure to respond to call within 30s | -25                 |
| Failure to meet majority consensus    | -5                  |
| Matching consensus                    | correct\_nodes \* 2 |
| Sending bad XRouter config            | -10                 |
| Sending bad XCloud config             | -2                  |

This mechanism and values are subject to change in future releases. Join the [Developer mailing list](https://eepurl.com/c5OJMj) to stay updated.

