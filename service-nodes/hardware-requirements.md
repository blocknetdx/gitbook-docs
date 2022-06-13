# Hardware Requirements

Hardware requirements for a Service Node vary depending on which [SPV wallets](https://docs.blocknet.co/resources/glossary/#spv) and services your node will support.

Probably the minumum HW requirements for _any_ Service Node would be:

### Minimum System

* 4 CPU cores (or 4 vCPUs if the Service Node runs on a VPS)
* 8 GB RAM
* 200 GB SSD Storage (doubtful that slower, HDD drives would work).
* 25+MBit/s Internet download speed. (100+ MBit/s is much better for faster syncing.)

Such a system could support a few small SPV wallets and a Blocknet staking wallet. As of this writing, the most economical place to rent a VPS with the above specs seems to be [Contabo](https://contabo.com/en/vps/). In fact, Contabo's "S" size VPS has exactly those minimum level specs and currently rents for €4.99 / mo.

### Medium & Large Systems

If you want to host the [Hydra](https://docs.blocknet.co/resources/glossary/#hydra) and/or [XQuery Indexer](https://docs.blocknet.co/resources/glossary/#indexer) services (and maybe a few SPV wallets as well), youll need 16 GB of RAM and 400+ GB of SSD storage space. Hosting Hydra or XQuery services requires hosting an EVM (Ethereum Virtual Machine) blockchain like Ethereum/ETH, Avalanche/AVAX, Fantom/FTM, Solana/SOL, Polkadot/DOT, Cardana/ADA, Etc. As of this writing, the smallest EVM blockchain supported by Blocknet is Avalanche/AVAX. AVAX blockchain _alone_ requires 300-400 GB of storage space, so if you want to host XQuery/Hydra services _and_ a few SPV wallets, you should really have 400+ GB of SSD storage space.

{% hint style="warning" %}
16 GB of RAM and 300-400 GB of SSD storage space are required to host the Avalanche/AVAX blockchain for Hydra/XQuery services.
{% endhint %}

Minumum HW requirements for a medium to large Service Node would be something like this:

* 6-8 CPU cores (or 6-8 vCPUs if the Service Node runs on a VPS)
* 16 GB RAM
* 400+ GB SSD Storage
* 25+MBit/s Internet download speed (100+ MBit/s is much better for faster syncing.)

### Extra Large System for supporting ETH archival node

To support [Hydra](https://docs.blocknet.co/resources/glossary/#hydra) and/or [XQuery Indexer](https://docs.blocknet.co/resources/glossary/#indexer) services of the Ethereum/ETH blockchain, a Service Node must host an ETH archival node. In terms of CPU and RAM requirements, running an ETH archival node requires:

* 8 CPU Cores (or 8 vCPUs if the ETH archival Node runs on a VPS)
* 16 GB RAM

The storage space requirements for an ETH archival node are a bit more demanding. The Go-Ethereum (GETH) archival node, which is the core wallet needed to run an ETH archival node, occupies about 8TB of space as of this writing (July 17, 2021). Furthermore, it is growing by 3TB per year. (Its current size can be found [here](https://etherscan.io/chartsync/chainarchive).) Therefore, a Service Node supporting an ETH archival node should probably have at least 10TB for ETH alone, plus maybe another 1.5-2TB for running other SPV wallets. It should also have the ability to expand its storage space by 3TB per year.

_Update Sept. 27, 2021: Some Blocknet community members are researching the possibility of using the_ [_Erigon ETH archival node_](https://github.com/ledgerwatch/erigon) _instead of the Go ETH (GETH) archival node. This is promising research as the Erigon ETH archival node occupies only about a quarter of the space of the GETH archival node. In other words, only about 2TB instead of 8TB as of this writing. Erigon ETH archival node also syncs in about one quarter the time it takes GETH to sync. As of this writing, it appears Erigon ETH may well be able to support Hydra services of ETH in its current stage of development, but until Erigon has standard ETH filter methods, it won't support XQuery services of ETH. Please join discussions in the #hydra channel of_ [_Blocknet Discord_](https://discord.gg/cQ9JNyNRW4) _to keep up with the latest developments on Erigon ETH._

It's also important to note that the storage for the ETH full archival node _must_ be very fast. In other words, it must use SSDs, not HDDs. There are 3 types of SSDs: SATA, SAS and NVMe/PCIe. Of the 3, SATA are the slowest, SAS are a little faster, and NVMe are by far the fastest. NVMe are _definitely_ the preferred variety of SSD drive when it comes to hosting an ETH archival node. In fact, it looks doubtful that SATA or SAS SSD drives will be fast enough to allow the ETH node to sync.

It is also recommended that the SSDs used for an ETH archival node be configured in a RAID mirror configuration (e.g. RAID-1, RAID-10, RAID-Z2). Without RAID mirroring, an SSD failure will almost certainly mean you'll have to resync the entire ETH full archival node, which takes over a month for a GETH node (but probably only a quarter of that time for an Erigon ETH node). Your ETH archival node will be offline for the duration of the resync.

As of this writing, it's not clear that any of the VPS Provider Options mentioned above are capable of providing a VPS which meets the HW requirements for an ETH archival node, or if they are capable, the cost can be a bit extreme and it's not clear they can expand storage space as needed to support the growing ETH full archival node. There may well be some smaller VPS providers who are capable of both meeting current HW requirements and allowing for storage space expansion in the future. There are also efforts underway to coordinate "package discounts" from such VPS provider(s) for a person or group of people to rent a number of ETH archival-capable VPS's at a discounted rate. Please join discussions on this topic in the #hydra channel of [Blocknet Discord](https://discord.gg/cQ9JNyNRW4).

Another option for meeting the HW requirements of an ETH archival node is to purchase your own hardware and run it at home or in a _colocation hosting_ data center. (Colocation hosting services can be found for USD $50 per month per server, as of Feb., 2022.) If purchasing your own SSD drives, be aware that ETH core will be writing to your SSDs continuously, so you'll want to get SSDs with a high "durability" rating. For example, a company called _Sabrent_ offers an 8TB NVMe SSD. On the surface, it may look like a good choice to use for building a system with lots of fast storage space. Unfortunately, this particular drive only has a TBW (Total Bytes Written) durability rating of 1,800 TB TBW, which, according to [this review](https://www.youtube.com/watch?v=iFXjC7k1OOw) makes it not very suitable to be used in an application that writes to it frequently. (Note, Samsung NVMe drives and/or any NVMe drives rated for industrial use are probably quite _durable_ and suitable for supporting an archival ETH node.) More discussions about HW details can be found in the #hydra channel of [Blocknet Discord](https://discord.gg/cQ9JNyNRW4).To support [Hydra](https://docs.blocknet.co/resources/glossary/#hydra) and/or [XQuery Indexer](https://docs.blocknet.co/resources/glossary/#indexer) services of the Ethereum/ETH blockchain, a Service Node must host an ETH archival node. In terms of CPU and RAM requirements, running an ETH archival node requires:

* 8 CPU Cores (or 8 vCPUs if the ETH archival Node runs on a VPS)
* 16 GB RAM

The storage space requirements for an ETH archival node are a bit more demanding. The Go-Ethereum (GETH) archival node, which is the core wallet needed to run an ETH archival node, occupies about 8TB of space as of this writing (July 17, 2021). Furthermore, it is growing by 3TB per year. (Its current size can be found [here](https://etherscan.io/chartsync/chainarchive).) Therefore, a Service Node supporting an ETH archival node should probably have at least 10TB for ETH alone, plus maybe another 1.5-2TB for running other SPV wallets. It should also have the ability to expand its storage space by 3TB per year.

_Update Sept. 27, 2021: Some Blocknet community members are researching the possibility of using the_ [_Erigon ETH archival node_](https://github.com/ledgerwatch/erigon) _instead of the Go ETH (GETH) archival node. This is promising research as the Erigon ETH archival node occupies only about a quarter of the space of the GETH archival node. In other words, only about 2TB instead of 8TB as of this writing. Erigon ETH archival node also syncs in about one quarter the time it takes GETH to sync. As of this writing, it appears Erigon ETH may well be able to support Hydra services of ETH in its current stage of development, but until Erigon has standard ETH filter methods, it won't support XQuery services of ETH. Please join discussions in the #hydra channel of_ [_Blocknet Discord_](https://discord.gg/cQ9JNyNRW4) _to keep up with the latest developments on Erigon ETH._

It's also important to note that the storage for the ETH full archival node _must_ be very fast. In other words, it must use SSDs, not HDDs. There are 3 types of SSDs: SATA, SAS and NVMe/PCIe. Of the 3, SATA are the slowest, SAS are a little faster, and NVMe are by far the fastest. NVMe are _definitely_ the preferred variety of SSD drive when it comes to hosting an ETH archival node. In fact, it looks doubtful that SATA or SAS SSD drives will be fast enough to allow the ETH node to sync.

It is also recommended that the SSDs used for an ETH archival node be configured in a RAID mirror configuration (e.g. RAID-1, RAID-10, RAID-Z2). Without RAID mirroring, an SSD failure will almost certainly mean you'll have to resync the entire ETH full archival node, which takes over a month for a GETH node (but probably only a quarter of that time for an Erigon ETH node). Your ETH archival node will be offline for the duration of the resync.

As of this writing, it's not clear that any of the VPS Provider Options mentioned above are capable of providing a VPS which meets the HW requirements for an ETH archival node, or if they are capable, the cost can be a bit extreme and it's not clear they can expand storage space as needed to support the growing ETH full archival node. There may well be some smaller VPS providers who are capable of both meeting current HW requirements and allowing for storage space expansion in the future. There are also efforts underway to coordinate "package discounts" from such VPS provider(s) for a person or group of people to rent a number of ETH archival-capable VPS's at a discounted rate. Please join discussions on this topic in the #hydra channel of [Blocknet Discord](https://discord.gg/cQ9JNyNRW4).

Another option for meeting the HW requirements of an ETH archival node is to purchase your own hardware and run it at home or in a _colocation hosting_ data center. (Colocation hosting services can be found for USD $50 per month per server, as of Feb., 2022.) If purchasing your own SSD drives, be aware that ETH core will be writing to your SSDs continuously, so you'll want to get SSDs with a high "durability" rating. For example, a company called _Sabrent_ offers an 8TB NVMe SSD. On the surface, it may look like a good choice to use for building a system with lots of fast storage space. Unfortunately, this particular drive only has a TBW (Total Bytes Written) durability rating of 1,800 TB TBW, which, according to [this review](https://www.youtube.com/watch?v=iFXjC7k1OOw) makes it not very suitable to be used in an application that writes to it frequently. (Note, Samsung NVMe drives and/or any NVMe drives rated for industrial use are probably quite _durable_ and suitable for supporting an archival ETH node.) More discussions about HW details can be found in the #hydra channel of [Blocknet Discord](https://discord.gg/cQ9JNyNRW4).
