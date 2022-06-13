# XBridge Design

The following diagrams depict the events of an exchange with various outcomes. In these diagrams, a "client" refers to software utlizing the Blocknet Protocol, which can be a blockchain, microservice, dApp, mobile app, website, etc.

**Successful Exchange**

![](https://docs.blocknet.co/img/protocol/swap-success.png)

The flow of the diagram above is top-to-bottom, left-to-right:

1. The maker client creates an order locally;
   * Order put in `new` state;
2. The order is broadcasted to the network;
   * A network transaction fee for the maker asset's blockchain is charged to the maker;
3. The Service Node network verifies the order is good;
4. The order is added to the order books, which the Service Nodes sync;
   * Order put in `open` state;
5. The taker client responds to take the order;
   * A network transaction fee for the taker asset's blockchain is charged;
   * A fixed 0.015 BLOCK fee is charged to the taker;
   * Order put in `accepting` state;
6. The Service Node network verifies the response to take the order is good;
7. The maker acknowledges the taker;
   * Order put in `hold` state;
8. The maker and trader assets are deposited into the atomic swap P2SH address;
   * Order put in `created` state;
9. The Service Nodes verify the terms of the atomic swap contract are good;
10. The transactions to the P2SH meet the required amount of confirmations;
11. The P2SH secrets are spent to the opposite party;
    * Order put in `signed` state;
    * Order put in `commited` state;
12. The maker and taker successfully receive the exchanged assets;
    * Order put in `finished` state;

**Failed Exchange - Bad Maker Order**

![](https://docs.blocknet.co/img/protocol/swap-fail-1.png)

The flow of the diagram above is top-to-bottom, left-to-right:

1. The maker client creates an order locally;
   * Order put in `new` state;
2. The order is broadcasted to the network;
   * A network transaction fee for the maker asset's blockchain is charged to the maker;
3. The Service Node network verifies the order is bad;
4. The order is rejected by the network;
   * Order put in `canceled` state;

**Failed Exchange - Bad Taker Response**

![](https://docs.blocknet.co/img/protocol/swap-fail-2.png)

The flow of the diagram above is top-to-bottom, left-to-right:

1. The maker client creates an order locally;
   * Order put in `new` state;
2. The order is broadcasted to the network;
   * A network transaction fee for the maker asset's blockchain is charged to the maker;
3. The Service Node network verifies the order is good;
4. The order is added to the order books, which the Service Nodes sync;
   * Order put in `open` state;
5. The taker client responds to take the order;
   * A network transaction fee for the taker asset's blockchain is charged;
   * A fixed 0.015 BLOCK fee is charged to the taker;
   * Order put in `accepting` state;
6. The Service Node network verifies the response to take the order is bad;
   * Order put in `canceled` state;

**Failed Exchange - Bad Atomic Swap Terms**

![](https://docs.blocknet.co/img/protocol/swap-fail-3.png)

The flow of the diagram above is top-to-bottom, left-to-right:

1. The maker client creates an order locally;
   * Order put in `new` state;
2. The order is broadcasted to the network;
   * A network transaction fee for the maker asset's blockchain is charged to the maker;
3. The Service Node network verifies the order is good;
4. The order is added to the order books, which the Service Nodes sync;
   * Order put in `open` state;
5. The taker client responds to take the order;
   * A network transaction fee for the taker asset's blockchain is charged;
   * A fixed 0.015 BLOCK fee is charged to the taker;
   * Order put in `accepting` state;
6. The Service Node network verifies the response to take the order is good;
7. The maker acknowledges the taker;
   * Order put in `hold` state;
8. The maker and trader assets are deposited into the atomic swap P2SH address;
   * Order put in `created` state;
9. The Service Nodes verify the terms of the atomic swap contract are bad;
10. The funds in the P2SH addresses are redeemed back to the original party;
    * Order put in `canceled` state;
