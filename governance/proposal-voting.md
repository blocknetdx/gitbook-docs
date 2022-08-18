# Proposal Voting

This guide explains how to vote on Blocknet's [Superblock](https://docs.blocknet.co/governance/introduction/#superblock) proposals for funding initiatives and governance management. Voting on proposals is important for the decentralized governance model to function properly.

{% hint style="warning" %}
**Voting Requirements & Important Information**

**5000** [**BLOCK**](https://docs.blocknet.co/blockchain/introduction) **is required in order to vote.** The process of voting can take place from a wallet containing at least 5000 BLOCK, or a Service Node collateral wallet. An active [Service Node](https://docs.blocknet.co/service-nodes/introduction) is _not_required.

* **Voting for proposals ends 60 blocks prior the Superblock.** It'd be safer to make sure you vote no later than 61 blocks before the Superblock to make sure your voting transaction gets at least 1 confirmation. See next voting deadline [here](https://docs.blocknet.co/governance/introduction/#superblock-voting-deadline).
* The inputs (UTXOs) used for the 5000 BLOCK (to vote) must be 100 BLOCK or larger.
* The inputs used for the 5000 BLOCK must be in the same address.
* Since the votes are recorded on-chain, casting a vote requires you to pay a network fee. This requires _each address_ to have an input _separate_ from the inputs used for the 5000 BLOCK to pay for the network fees. **This input used for the fee cannot be immature**. Funds will remain immature for about 60 minutes (60 blocks) after they staked.
* If you are staking, your vote will automatically re-cast.
* Your vote is not counted until the voting transaction fee has 1 confirmation (typically 1 minute), after which your votes will be accounted for when viewing the `listproposals`command.
* If you vote again you will have to pay another network fee to do so.
* The voting system will automatically calculate how many votes you have available according to your balance (1 vote per 5000 BLOCK) and cast your full vote weight when voting (5562 BLOCK balance = 1 vote, 49635 BLOCK balance = 9 votes.
* The deadline for creating proposals is 2880 blocks prior to the Superblock. See next proposal submission deadline [here](https://docs.blocknet.co/governance/create-proposal/#proposal-submission-deadline).
{% endhint %}



****
