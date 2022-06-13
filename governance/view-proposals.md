# View Proposals

This guide explains how to view Blocknet's [Superblock](https://docs.blocknet.co/governance/introduction/#superblock) proposals for funding initiatives and governance management. The ability to view proposals is important for the decentralized governance model to function properly, enabling informed discussions and [voting](https://docs.blocknet.co/governance/proposal-voting).

<details>

<summary>Voting Requirements &#x26; Important Information</summary>

**5000** [**BLOCK**](https://docs.blocknet.co/blockchain/introduction) **is required in order to vote.** The [process of voting](https://docs.blocknet.co/governance/proposal-voting) can take place from a wallet containing at least 5000 BLOCK, or a Service Node collateral wallet. An active [Service Node](https://docs.blocknet.co/service-nodes/introduction) is _not_ required.

Additional important information:

* The UTXO inputs used for the 5000 BLOCK (to vote) must be 100 BLOCK or larger.
* If you spend or stake any of your 5000 BLOCK inputs after you vote, the vote is marked invalid and you will need to cast your vote(s) again (an auto-revote mechanism will be created).
* Since the votes are recorded on-chain, casting a vote requires you to pay a network fee. It is best practice to have a small UTXO input for each vote to pay for the network fees.
* Your vote is not counted until the voting transaction fee has 1 confirmation (typically 1 minute), after which your votes will be accounted for when viewing the `listproposals` command.
* If you vote again you will have to pay another network fee to do so.
* The voting system will automatically calculate how many votes you have available according to your balance (1 vote per 5000 BLOCK) and cast your full vote weight when voting (5562 BLOCK balance = 1 vote, 49635 BLOCK balance = 9 votes.
* At least 60 minutes must pass before you can change your vote(s).
* The deadline for creating proposals is 2880 blocks prior to the Superblock.
* Voting for proposals ends 60 blocks prior the Superblock.

</details>

Proposals should be carefully reviewed along with the amount requested. It's a good idea to consider the total Superblock budget (40,000 BLOCK), the other proposals amounts requested, the priorities of the project, and if the proposal aligns with those priorities and greater vision of the project. The link for each proposal should lead to a description of what the proposal is for with background information and objectives.

### Viewing from the Qt Wallet <a href="#viewing-from-the-qt-wallet" id="viewing-from-the-qt-wallet"></a>

There are two Qt wallets, with the Redesign geared towards being more user friendly. Below is a comparison between the Classic and Redesign Qt wallets.

| Qt Version              | Redesign (GUI) | Redesign (console) | Classic (console) |
| ----------------------- | -------------- | ------------------ | ----------------- |
| Doesn't require console | Yes            | No                 |  No               |
| Lists proposals         | Yes            | Yes                | Yes               |
| Shows descriptions      | (has link)     | (has link)         | (has link)        |
| Shows vote counts       | No             | Yes                | Yes               |
| Shows pass/fail status  | Yes            | No                 | No                |
| Shows amounts requested | Yes            | Yes                | Yes               |
| Shows deposit addresses | No             | Yes                | Yes               |
| Shows past proposals    | Yes            | Yes                | Yes               |
| Easy to navigate        | Yes            | No                 | No                |
| Simple voting UI        | Yes            | No                 | No                |

<details>

<summary>View using the redesigned wallet</summary>

1. Open the [wallet](https://docs.blocknet.co/wallet/setup) and in the side menu, go to _Proposals_. The wallet does not need to be unlocked.
2.  The Proposals screen shows all the proposals submitted to the network. Above the list of proposals there is an option to filter by _Upcoming_, which displays the proposals that can currently be voted on. Select this filter to view all proposals currently open for voting.

    <img src="https://docs.blocknet.co/img/wallet-redesign/proposals-filter.png" alt="Filter Proposals" data-size="original">
3. [Vote on a proposal](https://docs.blocknet.co/governance/proposal-voting/#voting-from-the-qt-wallet).

</details>

<details>

<summary>View using the classic wallet</summary>

1. In the program menu, go to _Window_ > _Console_. The debug console will open in a new window.
2. In the input field at the bottom, type in `listproposals`, then press the _Enter_ key. To view proposals since a specific block, use `listproposals [BLOCK_NUMBER]` instead. Example: `listproposals 1209600`
3. A message showing all proposals will be returned.
4. [Vote on a proposal](https://docs.blocknet.co/governance/proposal-voting/#voting-from-the-qt-wallet).

</details>

### Viewing from the Browser <a href="#viewing-from-the-browser" id="viewing-from-the-browser"></a>

There are various options for viewing the proposals in the browser. Each option has its own unique features. As of this writing, the websites where proposals can be viewed include the following:

[Proposal Forum](https://forum.blocknet.co/c/draft-proposals)

[Blocknet Monitor](https://blocknetmonitor.com/?p=proposals)

### Viewing from the Terminal <a href="#viewing-from-the-terminal" id="viewing-from-the-terminal"></a>

#### Linux

1. Start the wallet. If it's not already running, use the following instructions to start it.&#x20;
   1. Navigate to the `bin` folder within your Blocknet wallet installation directory (EG: `~/blocknet/bin/`)
   2.  Type in the following command, replacing `[USERNAME]` and `[PASSWORD]` with the respective `rpcuser=` and `rpcpassword=` values from your `blocknet.conf` file located in your `~/.blocknet/` directory.

       ```
       ./blocknetd -rpcuser=[USERNAME] -rpcpassword=[PASSWORD] -daemon
       ```

       _Example:_

       ```
       ./blocknetd -rpcuser=JohnBlocknet -rpcpassword=supersecretpassword -daemon
       ```
2. The wallet process will begin in the current terminal window. You will need to open a new terminal window or tab and navigate to the same location before continuing.
3.  If your wallet was just started, you may need to wait a few minutes for the proposals to sync, otherwise you may not see the full list of proposals. Use the following command to view the proposals:

    ```
    ./blocknet-cli listproposals
    ```
4.  To view proposals since a specific block:

    ```
    ./blocknet-cli listproposals [BLOCK_NUMBER]
    ```

    _Example:_

    ```
    ./blocknet-cli listproposals 1209600
    ```
5. [Vote on a proposal](https://docs.blocknet.co/governance/proposal-voting/#voting-from-the-terminal).

#### Windows

1. Start the wallet. If it's not already running, use the following instructions to start it.&#x20;
2.  Type in the following command, replacing `[USERNAME]` and `[PASSWORD]` with the respective `rpcuser=` and `rpcpassword=` values from your `blocknet.conf` file located in the `C:\Users\[YourUsername]\AppData\Roaming\Blocknet` directory. This directory can be found by opening the file explorer and pasting in `%appdata%\Blocknet\` into the file explorer path field.

    ```
    blocknetd -rpcuser=[USERNAME] -rpcpassword=[PASSWORD]
    ```

    _Example:_

    ```
    blocknetd -rpcuser=JohnBlocknet -rpcpassword=supersecretpassword
    ```
3. The wallet process will begin in the current terminal window. You will need to open a new terminal window or tab and navigate to the same location before continuing.
4.  If your wallet was just started, you may need to wait a few minutes for the proposals to sync, otherwise you may not see the full list of proposals. Use the following command to view the proposals:

    ```
    ./blocknet-cli listproposals
    ```
5.  To view proposals since a specific block:

    ```
    ./blocknet-cli listproposals [BLOCK_NUMBER]
    ```

    _Example:_

    ```
    ./blocknet-cli listproposals 1209600
    ```
6. [Vote on a proposal](https://docs.blocknet.co/governance/proposal-voting/#voting-from-the-terminal).

#### Mac OS



1. Navigate to the `bin` folder within your Blocknet wallet installation directory (EG: `~/Downloads/blocknet/bin/`)\
   _NB: This requires the blocknet-\[version]-osx64.tar.gz download version_
2. Start the wallet. If it's not already running, use the following instructions to start it.&#x20;
3.  Type in the following command, replacing `[USERNAME]` and `[PASSWORD]` with the respective `rpcuser=` and `rpcpassword=` values from your `blocknet.conf` file located in your `~/Library/Application Support/Blocknet/` directory. This directory can be found by opening the Finder, in the program menu selecting _Go_ > _Go to Folder_, entering `~/Library/Application Support/Blocknet/` in the path, and pressing _Enter_.

    ```
    ./blocknetd -rpcuser=[USERNAME] -rpcpassword=[PASSWORD] -daemon
    ```

    _Example:_

    ```
    ./blocknetd -rpcuser=JohnBlocknet -rpcpassword=supersecretpassword -daemon
    ```
4. The wallet process will begin in the current terminal window. You will need to open a new terminal window or tab and navigate to the same location before continuing.
5.  If your wallet was just started, you may need to wait a few minutes for the proposals to sync, otherwise you may not see the full list of proposals. Use the following command to view the proposals:

    ```
    ./blocknet-cli listproposals
    ```
6.  To view proposals since a specific block:

    ```
    ./blocknet-cli listproposals [BLOCK_NUMBER]
    ```

    _Example:_

    ```
    ./blocknet-cli listproposals 1209600
    ```
7. [Vote on a proposal](https://docs.blocknet.co/governance/proposal-voting/#voting-from-the-terminal).
