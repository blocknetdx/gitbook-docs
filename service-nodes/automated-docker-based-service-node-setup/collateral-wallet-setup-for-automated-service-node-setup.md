# Collateral Wallet Setup for Automated Service Node Setup

{% hint style="warning" %}
**Important:** This Collateral Wallet Setup guide assumes your collateral wallet has been set up according to the [VPS Staking guide](https://docs.blocknet.co/wallet/staking/#staking-from-cli-on-a-vps-running-ubuntu-linux), and the aliases for `blocknet-cli`, `stdaemon` and `stunlock` have also been created according to that guide. If your collateral wallet is instead a GUI/Qt Blocknet wallet on a different computer, the wallet commands given in this guide in the form,`blocknet-cli wallet-command` can instead be issued in your GUI/Qt wallet under _Tools->Debug Console_. For example, a _Staking Wallet_ command given in this guide as `blocknet-cli getnewaddress snode01` can be issued in a GUI/Qt wallet under _Tools->Debug Console_ as simply `getnewaddress snode01`.
{% endhint %}

1. If your collateral wallet is not yet funded, send collateral funds to your collateral wallet. Send at least 5001 BLOCK for every Service Node your collateral wallet will support, plus 1 extra BLOCK. (The 1 extra BLOCK, and the 1 extra BLOCK per Service Node will cover transaction fees. For example, send at least 15,004 BLOCK for 3 Service Nodes' collateral.) To send BLOCK to your collateral wallet:
   1.  Create an address in your collateral wallet to which you can send the funds. On your _Collateral Wallet_computer (which could be the same as your _Service Node Wallet_ computer), issue the following command:

       ```
       blocknet-cli getnewaddress
       ```

       Note, you can optionally give a label to the new address you create by passing a _label_ parameter to the `getnewaddress` command. For example, you can label your new address, "_receive-address_" by issuing the following command:

       ```
       blocknet-cli getnewaddress receive-address
       ```
   2. Send BLOCK to the address returned by the `getnewaddress` command.
2.  Create a new public address for the Service Node. A unique name for this address will need to be provided as an alias. To do this, type `blocknet-cli getnewaddress [ALIAS]` into the terminal with `[ALIAS]` replaced with the alias you will be using for this address. Example:

    ```
    blocknet-cli getnewaddress snode01
    BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP
    ```

    In this example, `BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP` was the address returned by `getnewaddress`.
3.  Create the input(s) needed for the Service Node collateral using the following command structure (**Note:**If you already have your inputs created for your Service Node(s) you can skip this step _and_ the next step):

    ```
    blocknet-cli servicenodecreateinputs [NODE_ADDRESS] [NODE_COUNT] [INPUT_SIZE]
    ```

    * `NODE_ADDRESS` = The address returned in the previous step.
    * `NODE_COUNT` = The number of Service Nodes to create.&#x20;
      * Requires a minimum of 5001 BLOCK per Service Node (1 BLOCK extra for transaction fee).
      * If left blank, it defaults to `1`.
      * Example: 20,001 BLOCK will be needed to create 4 Service Nodes
    * `INPUT_SIZE` = The amount of BLOCK for each collateral input.&#x20;
      * Must be >= `500` and <= `5000`.
      * If left blank, it defaults to `1250`.
      * Example: `1000` will create 5 inputs of 1000 BLOCK each per Service Node

    Single Service Node Example:

    ```
    blocknet-cli servicenodecreateinputs BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP
    ```

    Single Service Node (2 inputs) Example:

    ```
    blocknet-cli servicenodecreateinputs BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP 1 2500
    ```

    Multiple Service Nodes (10k BLOCK) Example:

    ```
    blocknet-cli servicenodecreateinputs BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP 2 5000
    ```
4. Prepare to create a `servicenode.conf` file in your data directory (Linux data dir =`~/.blocknet` by default). Delete any old `servicenode.conf` file in the data directory, or delete any out-of-date service node references within your `servicenode.conf`.&#x20;
5.  Create a `servicenode.conf` configuration file. Enter the command:

    ```
    blocknet-cli servicenodesetup [NODE_ADDRESS] [ALIAS]
    ```

    Where `[NODE_ADDRESS]` is the address created for your Service Node in step 2 above, and `[ALIAS]`is any name you want to give to your Service Node. With this command, an entry will be created for the Service Node in the `servicenode.conf` file in your collateral wallet data dir. Example:&#x20;

    ```
    blocknet-cli servicenodesetup BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP snode01
    {
        "alias": "snode01",
        "tier": "SPV",
        "snodekey": "02a5d0279e484a3df81acd611e1052d2e0797e796564ecbc25c7fe19f36e9985e5",
        "snodeprivkey": "PswGMd6faZf1ceLojzGeKn7LQuXVwYgRQG8obUKrThZ8ap4pkRR7",
        "address": "BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP"
    }
    ```
6. Copy the _snodeprivkey_ and the _address_ returned in the previous step and paste them into a temporary text file. You'll need them later on. (In the above example, _snodeprivkey_ is`PswGMd6faZf1ceLojzGeKn7LQuXVwYgRQG8obUKrThZ8ap4pkRR7`, and _address_ is `BmpZVb522wYmryYLDy6EckqGN4g8pT6tNP`). Note, both the _snodeprivkey_ and the _address_ of your Service Node are also stored at this point in the `servicenode.conf` file in your collateral wallet data directory, so you can always find them there if you don't want to paste them into a temporary text file to record them.
7.  Restart the _Collateral Wallet_.

    ```
    blocknet-cli stop
    stdaemon
    ```

    Note, you will probably need to wait at least 30 seconds after issuing `blocknet-cli stop` before you'll be allowed to launch `stdaemon.` Just keep trying every 30 seconds or so to launch `stdaemon`until you no longer get, "_Error: Cannot obtain a lock on data directory._"
8.  Assuming you want to [stake](https://docs.blocknet.co/resources/glossary/#staking) your collateral, unlock your staking wallet for staking only:

    ```
    stunlock
    ```

    (Enter your wallet password when prompted.)
9.  Confirm your wallet is staking by issuing the command:

    ```
    blocknet-cli getstakingstatus
    ```

    When this command returns, `"status": "Staking is active"`, then you know your wallet is staking properly. Note, you may also want to confirm your staking wallet balance is correct with:

    ```
    blocknet-cli getbalance
    ```



Continue to [Prepare to Deploy Service Node](prepare-to-deploy-service-node.md).
