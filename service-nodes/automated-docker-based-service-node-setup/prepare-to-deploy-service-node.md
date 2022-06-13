# Prepare to Deploy Service Node

Logged in to the Ubuntu Linux server you [set up above](https://docs.blocknet.co/service-nodes/setup/#set-up-an-ubuntu-linux-server), (logged in as the user you created according to the setup instructions, not as root),

1.  Install necessary SW packages:

    ```
    sudo apt install git python3 python3-pip
    ```

    (Enter your user's password when prompted - not the root password.)
2. Add your Linux user to the _docker_ group:
   1. `sudo groupadd docker`
   2. `sudo gpasswd -a $USER docker`
   3. `exit` to disconnect from your VPS
   4. Reconnect to your VPS, logging in again as the same user as before (not as root).
3.  Change directory to the directory where you want to install the Service Node Automated Setup tools. In this guide, we'll use the user's home directory (`~`):

    ```
    cd ~
    ```
4.  Copy the Service Node Automated Setup tools from the Blocknet Github repository:

    ```
    git clone https://github.com/blocknetdx/exrproxy-env
    ```
5.  Change directory to the `autobuild` subdirectory:

    ```
    cd exrproxy-env/autobuild
    ```
6.  Install necessary Python3 libraries:

    ```
    pip3 install -r requirements.txt
    ```
7.  Copy `alldaemons.yaml` example configuration file to `custom.yaml` in preparation to configure your Service Node:

    ```
    cp examples/alldaemons.yaml custom.yaml
    ```

    Explanation: The configuration file used to specify which SPV wallets you want to deploy & support on your Service Node is called, `custom.yaml`. It lives in the `autobuild` subdirectory of the `exrproxy-env` directory. The `examples/alldaemons.yaml` configuration file is meant to be an example of how `custom.yaml` should look if you were going to configure your Service Node to support _all available SPV wallet daemons and Blocknet Services._ The way to create a `custom.yaml` which configures _only_ the SPV wallets you want to support is to start with the `alldaemons.yaml` file, then delete the entries of the SPV wallets you _don't_ want to support. This is the reason we copied `examples/alldaemons.yaml` to `custom.yaml` in the `autobuild` directory.
8.  Edit `custom.yaml` with a simple text editor like [vi](https://www.tutorialspoint.com/unix/unix-vi-editor.htm) or [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/). For example:

    ```
    vi custom.yaml
    ```
9.  Because we copied `alldaemons.yaml` to `custom.yaml` earlier, editing `custom.yaml` for the first time will reveal a file identical to `alldaemons.yaml`, something like the following:

    ```
    --- # snode daemon LIST
    - j2template: dockercompose.j2
      name: dockercompose
      daemons:
          # DO NOT DELETE XR_PROXY ENTRY
          - name: XR_PROXY # DO NOT DELETE
              image: blocknetdx/exrproxy:0.8.0 # DO NOT DELETE
              config_mount_dir: /snode/xr_proxy/config # DO NOT DELETE
              nginx_mount_dir: /snode/xr_proxy/nginx # DO NOT DELETE
          # DELETE THE FOLLOWING ETH ENTRY IF YOU DON'T WANT TO DEPLOY A 10+ TB GETH NODE
          - name: ETH # DELETE THIS ENTRY IF YOUR SERVER DOESN'T MEET HW REQUIREMENTS: 10+ TB NVMe SSD storage (21 Dec, 2021), 16 GB RAM when GETH deployed locally
              image: blocknetdx/eth-payment-processor:0.5.2 # DELETE THIS ENTRY IF YOUR SERVER DOESN'T MEET HW REQUIREMENTS
              postgresql_data_mount_dir: /snode/eth_pymt_db # DELETE THIS ENTRY IF YOUR SERVER DOESN'T MEET HW REQUIREMENTS
              geth_data_mount_dir: /snode # DELETE THIS ENTRY IF YOUR SERVER DOESN'T MEET HW REQUIREMENTS
          # DO NOT DELETE SNODE ENTRY
          - name: SNODE # DO NOT DELETE
              image: blocknetdx/servicenode:latest # DO NOT DELETE
              config_mount_dir: /snode # DO NOT DELETE
              data_mount_dir: /snode # DO NOT DELETE
          # AVALANCHE INDEXER - DELETE IF YOU DON'T WANT TO SUPPORT XQUERY
          - name: AVAX # Requires 400 GB of SSD disk, 16 GB RAM & 6 vCPUs for XQUERY (21 December, 2021)
              image: avaplatform/avalanchego:v1.7.3
              data_mount_dir: /snode
          # THE STANDARD XLITE WALLET SET - DELETE ANY YOU DON'T WANT TO SUPPORT  
          - name: BTC # Requires 451 GB of disk (15 December, 2021)
             image: blocknetdx/bitcoin:v0.20.0
             config_mount_dir: /snode
             data_mount_dir: /snode
          - name: LTC # Requires 71 GB of disk (15 December, 2021)
             image: blocknetdx/litecoin:v0.18.1
             config_mount_dir: /snode
             data_mount_dir: /snode
         - name: DGB # Requires 27 GB of disk (15 December, 2021), 4-5 GB RAM/Swap
             image: blocknetdx/digibyte:v7.17.2
             config_mount_dir: /snode
             data_mount_dir: /snode
         ...
    ```
10. **Important:** Pay close attention to the comments embedded in this file. Note that some of the entries, like **XR\_PROXY** and **SNODE**, should _never_ be deleted. Other entries, like **ETH**, **BTC**,  **AVAX**, and **LBC** for example, have comments attached to them indicating they require more HW resources than some of the other entries. If the sum total of the HW resources required by all the entries you have listed in this file exceeds the HW resources your server has available, you'll need to delete entries until the amount of HW resources required is less than what your server has available. The cumulative HW resource requirements referred to here are mainly the disk space requirements. The RAM and CPU requirements of different entries are not necessarily cumulative. For Example, ETH and AVAX both require 16 GB of RAM, but that doesn't necessarily mean you need 32 GB RAM to support both of them on your SNode. However, if you want to have the ability to sync both of them concurrently, then 32+ GB RAM would be recommended.
11. Proceed to delete the entries of those SPV wallets you do _not_ want to support on your Service Node. For example, if you don't want to support **DGB**, you would delete the following 4 lines:

    ```
        - name: DGB # Requires 27 GB of disk (15 December, 2021), 4-5 GB RAM/Swap
           image: blocknetdx/digibyte:v7.17.2
           config_mount_dir: /snode
           data_mount_dir: /snode
    ```
12. Note: The `/snode` mount point used in the `alldaemons.yaml` example can be changed as desired. If changing the mount points, the only requirements are:
    1. The two mount points in the **XR\_PROXY** entry must be unique, as they are in the `alldaemons.yaml` example.
    2. The mount point for `postgresql_data_mount_dir:` in the **ETH** entry must be unique, as it is in the `alldaemons.yaml` example.
    3. All remaining mount points will be automatically "_uniquified_" by the autobuild scripts. For example, specifying `data_mount_dir: /snode` in the **BTC** entry will cause BTC data to be stored in the unique directory, `/snode/BTC/data`.
13. If you will deploy an archival [GETH](https://docs.blocknet.co/resources/glossary/#geth) node, the mount point you choose in the **ETH** entry for `geth_data_mount_dir:` _must_ have at least 10TB of SSD storage space available as of this writing. See[Hardware Requirements For Service Node Wallet](https://docs.blocknet.co/service-nodes/setup/#hardware-requirements-for-service-node-wallet) for more details.
14. **Testnet SNODE**: If you want your Service Node to run on _testnet_ instead of _mainnet_, simply replace the line:

    ```
    - name: SNODE
    ```

    with this line:

    ```
    - name: testSNODE
    ```
15. **Trading Node**: The autobuild deployment tools also allow you to deploy a _Trading Node_ instead of a _Service Node_ if you wish. A _Trading Node_ is simply a Blocknet core wallet which is _not_ configured to run as a Service Node. When you configure `custom.yaml` to deploy a _Trading Node_ instead of a Service Node, the other wallet daemons listed in your `custom.yaml` become trading wallets rather than SPV wallets of an Service Node. The _Trading Node_ will automatically be connected to all the other wallets daemons listed in your `custom.yaml`. As such, issuing `dxGetLocalTokens` from your _Trading Node's CLI_ will return a list of all the coins you had listed in `custom.yaml`, and you can trade between any of them from the CLI of your _Trading Node_. To deploy a _Trading Node_ instead of a Service Node, simply replace the line:

    ```
    - name: SNODE
    ```

    with this line:

    ```
    - name: TNODE
    ```
16. **Testnet TNODE**: If you want your Trading Node to run on _testnet_ instead of _mainnet_, simply replace the line:

    ```
    - name: TNODE
    ```

    with this line:

    ```
    - name: testTNODE
    ```
17. (Recommended) It is recommended to deploy certain SPV Wallets in stages. The reason is because some SPV wallets are known to require large amounts of RAM and/or I/O bandwidth while they are syncing their respective blockchains. AVAX, LBC and DGB all fall into this category. For this reason, it is recommended _not_ to run more than one of those 3 while any one of them is syncing. For example, it's best _not_ to run LBC or DGB while AVAX is syncing, or to run AVAX or DGB while LBC is syncing. To learn techniques for syncing just one of these 3 at a time, see the information given in the [Maintenance of Auto-Deployed Service Node](https://docs.blocknet.co/service-nodes/setup/#maintenance-of-auto-deployed-service-node) section of this guide. Note, if you have over 32 GB of RAM and NVMe storage, you may well be able to sync all of these HW intensive blockchains in parallel without issue.
18. Save your edits to `custom.yaml` and exit the editor.

<details>

<summary><strong>Didn't see an entry in <code>alldaemons.yaml</code> for the coin/daemon you want to support?</strong></summary>

As of this writing, we don't yet have many coin/daemon/SPV wallet entries listed in `alldaemons.yaml`. This will be changing very soon. The goal is that every coin supported by BlockDX, which means every coin listed in the [Blocknet manifest-latest.json](https://github.com/blocknetdx/blockchain-configuration-files/blob/master/manifest-latest.json), will have an entry in `alldaemons.yaml` and thus be readily available for Service Nodes to support. One thing you can do to ensure you have the latest available version of `alldaemons.yaml` (and the latest version of the autobuild tools in general) is the following:

```
cd ~/exrproxy-env
git pull
```

If the `git pull` command gives errors like "Merge conflict" or "error: Your local changes to the following files would be overwritten by merge," it means you have locally changed one or more of the files `git` is trying to pull from the upstream repository. In this case, you can undo any local changes you made to any of the files tracked by `git` by issuing the command:

```
git reset --hard
```

Note, `git reset --hard` will cause any changes you made to tracked files in the `exrproxy-env` directory tree to be lost. After issuing `git reset --hard`, you should now be able to issue the `git pull` command without errors.

Note: If you are trying to add Service Node support for a new coin so the new coin can be tested and then added to the _manifest-latest.json_, please refer to the [Listing Process](https://docs.blocknet.co/blockdx/listings/#listing-process).

</details>
