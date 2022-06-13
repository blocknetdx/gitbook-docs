# Maintenance of Auto-Deployed Service Node

### Changing Configuration of a Docker-Based Service Node (or Trading Node)

1.  Before you can add or subtract coin daemons, or change the configuration of your Service Node in any way, you first need to shut it down as follows:

    ```
    cd ~/exrproxy-env
    docker-compose down
    ```

    This will not only stop all the docker containers you deployed from the `docker-compose.yml` file, it will also remove all those docker containers. It will _not_ remove the blockchain data for each of the coin daemons you deployed. That data is safely stored in the place(s) you had specified as the `config_mount_dir` and `data_mount_dir` in `custom.yaml` (`/snode` by default). That means you won't have to wait for the blockchains of the various coin daemons to sync again the next time you bring up your Service Node.
2.  Once your Service Node has been brought down, you can edit the configuration file, `~/exrproxy-env/autobuild/custom.yaml`, to add or subtract coin daemons as desired. You can also, for example, convert your Service Node into a _testnet_ Service Node by replacing `SNODE` with `testSNODE` in `custom.yaml`. To make sure you have a current reference for all coin daemons currently available (and the latest version of the autobuild tools in general), it is recommended to _pull_ the latest changes from the Github repository:

    ```
    cd ~/exrproxy-env
    git pull
    ```

    If the `git pull` command gives errors like "Merge conflict" or "error: Your local changes to the following files would be overwritten by merge," it means you have locally changed one or more of the files `git` is trying to pull from the upstream repository. In this case, you can undo any local changes you made to any of the files tracked by `git` by issuing the command:

    ```
    git reset --hard
    ```

    Note, `git reset --hard` will cause any changes you made to tracked files in the `exrproxy-env`directory tree to be lost. After issuing `git reset --hard`, you should now be able to issue the `git pull` command without errors. `git pull` will pull all available updates to your local `exrproxy-env` repository, including any updates to `~/exrproxy-env/autobuild/examples/alldaemons.yaml`. The remote/upstream version of `alldaemons.yaml`will be updated frequently with new coin daemons/SPV wallets, so it'll be good to pull the latest version frequently. When you have the latest `alldaemons.yaml`, you can copy/paste coin daemon entries from `alldaemons.yaml` into `~/exrproxy-env/autobuild/custom.yaml`, as desired.
3. Once you've finished editing `~/exrproxy-env/autobuild/custom.yaml` according to the new configuration you want (or even if you didn't edit `custom.yaml` at all), you can bring your Service Node back up as you did before in [Auto-Deploy Service Node](https://docs.blocknet.co/service-nodes/setup/#auto-deploy-service-node), using the `app.py` script and the `deploy.sh` script as instructed there.
4.  IMPORTANT: If you are likely to bring your Service Node down and back up again multiple times, it is _highly recommended_ to create a simple Bash Shell script like the following to avoid having to use `~/exrprox-env/deploy.sh` each time you want to bring your Service Node up. That way you can avoid answering all the questions asked by `deploy.sh` each time you bring your Service Node up:

    ```
    #!/bin/bash

    export PUBLIC_IP="75.120.155.29"  # Update with your public ip address
    export SN_NAME="snode01"  # Update with your snode name
    export SN_KEY="PswGMd6gaZf1ceLojzGeKn7PQuXVwYgRQG8obUKrThZ8ap4pkRR7"  # Update with your snode private key
    export SN_ADDRESS="BqNaZmLJt9wEGBHDNid9FvsgrG2x7Hbfex"  # Update with your snode address
    export RPC_USER="my-rpc-user"   # Update with your rpc user
    export RPC_PASSWORD="my-rpc-pw"    # Update with your rpc password

    docker-compose -f "docker-compose.yml" up -d --build
    ```

    Create the above Bash Shell script and give it a name like, `dockerup.sh`. You can keep it anywhere, but `~/exrproxy-env` is probably a convenient place to keep it. Give it executable permissions too: `chmod +x dockerup.sh`. Now, instead of running `./deploy.sh` in step 6 of the [Auto-Deploy Service Node](https://docs.blocknet.co/service-nodes/setup/#auto-deploy-service-node) instructions, you can run `./dockerup.sh`.
5.  If you've subtracted one or more coin daemons from your `custom.yaml` because you want to save the disk space used by the blockchains of those coin daemons, please remember that the blockchain data is not deleted/removed when the docker container is removed. As mentioned above, the blockchain data of a coin daemon persists in a special mounted directory. If you kept the default data and config dir mount points given in `alldaemons.yaml`, which is `/snode`, then the blockchain data for DGB, for example, will be stored in `/snode/DGB/config`, and it can occupy many GB of space. To find out exactly how much space is being used by each coin daemon, you can enter:

    ```
    sudo du -d 1 -h /snode
    57G   /snode/LTC
    3.6G  /snode/MONA
    222M  /snode/testsnode
    3.3G  /snode/snode
    27G   /snode/DGB
    16K   /snode/xr_proxy
    11G   /snode/RVN
    48M   /snode/eth_pymt_db
    ```

    Sudo is necessary here because `/snode` directory is owned by `root`, not by $USER. So, if you want to stop supporting DGB coin, for example, and you also want to free up the 27GB of space the DGB blockchain is taking up, you'll need to first make sure your Service Node is shut down according to step 1 above, then make sure the DGB entry has been removed from `custom.yaml` according to step 2 above, then issue the following command to permanently remove DGB blockchain data and free the space it is occupying:

    ```
    sudo rm -rf /snode/DGB
    ```



{% hint style="warning" %}
Be very careful to enter the `rm -rf` command very precisely. A typo could be disastrous. Also, be aware that adding support for DGB again after deleting its blockchain data will require the DGB blockchain to sync from scratch.
{% endhint %}

### About Docker

For the most part, the _docker-compose_ commands given thus far in this guide will suffice to manage your Service Node. However, if something "out of the ordinary" happens, or if you want to do something fancy with your docker objects, there are a few more things it will be good to know about docker:

* Let's say, for example, you want to interact directly with the DGB daemon, but you aren't sure the name of the DGB CLI executable command. Here's one way to find it:
  1.  Start an interactive _Bash_ shell in the DGB container:

      ```
      docker exec -it exrproxy-env_DGB_1 /bin/bash
      ```

      You should see a prompt like this:

      ```
      root@f4c21d83d6fe:/opt/blockchain#
      ```
  2.  Find which daemons are running in the DGB container:

      ```
      root@f4c21d83d6fe:/opt/blockchain# ps uax
      ```

      It should show you something like this:

      ```
      USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
      root         1 46.4 28.7 8132896 4726660 ?     SLsl 11:37  25:38 digibyted -conf=/opt/blockchain/config/digibyte.conf
      root        29  1.7  0.0  18248  3280 pts/0    Ss   12:33   0:00 /bin/bash
      root        39  0.0  0.0  34424  2788 pts/0    R+   12:33   0:00 ps uax
      ```
  3.  Note there is one running process called, `digibyted`. This is the name of the Digibyte daemon process and it is also a great clue about the name of the CLI command for interacting with the Digibyte daemon. The name of the CLI command can usually be derived from the name of the daemon process by simply replacing the `d` at the end of the daemon process with `-cli`, like this:

      ```
      digibyted -> digibyte-cli
      ```
  4.  If you want to verify there is a `digibyte-cli` command, you can do this:

      ```
      which digibyte-cli
      ```

      which should return this:

      ```
      /usr/bin/digibyte-cli
      ```
  5.  Now you can interact with the Digibyte daemon as follows:

      ```
      root@f4c21d83d6fe:/opt/blockchain# digibyte-cli getblockcount
      13535747
      ```

      Alternatively, we can exit the Bash shell running in the DGB container, then execute the `digibyte-cli` command from outside the docker container:

      ```
      root@f4c21d83d6fe:/opt/blockchain# exit
      exit
      ~$ docker exec exrproxy-env_DGB_1 digibyte-cli getblockcount
      13535762
      ```
*   Now let's consider the case where the docker container with which you want to interact does _not_ have _Bash_ shell available. This is the case for the Syscoin container, for example. Attempting to invoke the _Bash_ shell in the Syscoin container will result in an error:

    ```
    docker exec -it exrproxy-env_SYS_1 /bin/bash
    OCI runtime exec failed: exec failed: container_linux.go:380:
    starting container process caused: exec: "/bin/bash": stat
    /bin/bash: no such file or directory: unknown
    ```

    The solution is to invoke a shell which _does_ exist in the container, like this:

    ```
    docker exec -it exrproxy-env_SYS_1 /bin/sh
    ```
*   Another unique feature of \[an earlier version of] the Syscoin container is that the `syscoin-cli`command requires certain parameters to be passed to it in order to work properly. For example:

    ```
    docker exec exrproxy-env_SYS_1 syscoin-cli getblockcount 
    ```

    returns

    ```
    error: Could not locate RPC credentials. No authentication cookie could be found, and RPC password is not set.  See -rpcpassword and -stdinrpcpass.  Configuration file: (/root/.syscoin/syscoin.conf)
    ```

    But invoking `syscoin-cli` as follows, works properly:

    ```
    docker exec exrproxy-env_SYS_1 syscoin-cli -conf=/opt/blockchain/config/syscoin.conf getblockcount
    1218725
    ```

    Alternatively, this also works:

    ```
    docker exec exrproxy-env_SYS_1 syscoin-cli -datadir=/opt/blockchain/config getblockcount
    1218725
    ```

    Note: The DASH container, and perhaps others containers, will also require these same parameters to be passed to the CLI command. \[edit: The latest SYS container does _not_ require the additional parameter]
*   Now let's consider another case where more _docker_ knowledge could be required. Let's consider the case where `docker-compose down` fails to complete due to receiving a timeout error something like the following:

    ```
    UnixHTTPConnectionPool(host='localhost', port=None): Read timed out.
    ```

    Some users have actually seen this exact error when trying to run `docker-compose down` while an I/O intensive process (e.g. `lbrycrdd`) is running on the system. [Here are some potentially helpful suggestions on how to fix/avoid this timeout error](https://stackoverflow.com/questions/42230536/docker-compose-up-times-out-with-unixhttpconnectionpool). However, once `docker-compose down` has failed to complete even once, it can leave your docker environment in a state where some docker containers have been _stopped_, but have not yet been removed. This state is problematic because your next attempt to bring up your Service Node with `deploy.sh` (or `dockerup.sh`) will give errors saying the container names you're trying to create, already exist. If you suspect such a situation has developed, one thing you can do is to list _all_ docker containers - both running and stopped:

    ```
    docker ps -a
    ```

    If this command shows some containers with a _stopped_ STATUS, then you probably need to remove those _stopped_ containers. Fortunately, docker has a handy _prune_ utility for removing all _stopped_containers:

    ```
    docker container prune
    ```

    Also, if your docker containers, images, volumes and/or networks get messed up for any reason, or if you end up with docker images on your server which are no longer used and taking up space unnecessarily,[docker offers a variety of _prune_ utilities to clean up the current state of your _docker_ environment](https://docs.docker.com/config/pruning/).
*   Note: In the context of a docker-based Service Node auto-deployment, executing the following 2 command should be equivalent to `docker-compose down`:

    ```
    docker stop $(docker ps -q -f name=exrproxy-env_*)
    docker rm $(docker ps -a -q -f name=exrproxy-env_*)
    ```

    This trick can be useful if, for example, `docker-compose.yml` is accidentally reconfigured before `docker-compose down` is executed, causing `docker-compose down` to fail.
*   _docker_ offers a variety of useful utilities for managing and interacting with various docker objects. To see a list of all docker options and commands, enter:

    ```
    docker --help
    ```

    To get help on a specific docker command, enter:

    ```
    docker COMMAND --help
    ```

    For example,

    ```
    docker export --help
    ```

    There are also docker guides available at [https://docs.docker.com/go/guides/](https://docs.docker.com/go/guides/).
