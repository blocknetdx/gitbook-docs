# Auto-Deploy Service Node

1. At this point in the process, your _Present Working Directory_ ($PWD) should be `~/exrproxy-env/autobuild` and the `custom.yaml` file in that directory should contain a list of coins/SPV wallets/daemons you want to deploy and support on your Service Node. (Type `pwd` to confirm your _Present Working Directory_. Review the contents of `custom.yaml` with: `less custom.yaml`.)
2. Run the _autobuild_ script to translate your `custom.yaml` configuration file into a `dockercompose-custom.yaml` file which can be used by _docker-compose_ to launch all the docker containers needed to run your Service Node:
   *   If your Service Node will _not_ be supporting a [GETH](https://docs.blocknet.co/resources/glossary/#geth) node, issue the following command:

       ```
       ./app.py
       ```
   *   If your Service Node will support a [GETH](https://docs.blocknet.co/resources/glossary/#geth) node locally, issue the following command:

       ```
       ./app.py --deploy_eth
       ```
   *   If your Service Node will support an _external_ [GETH](https://docs.blocknet.co/resources/glossary/#geth) node, issue the following command:

       ```
       ./app.py --gethexternal [IP-Address-of-External-GETH-Node]
       ```

       Note, this _--gethexternal_ option has not been fully tested as of this writing.
3.  Move the `dockercompose-custom.yaml` we just generated to the `exrproxy-env` directory and give it the name _docker-compose_ will be looking for:

    ```
    mv  dockercompose-custom.yaml ../docker-compose.yml
    ```
4.  Change directory to the `exrproxy-env` directory:

    ```
    cd ..
    ```
5. Prepare to enter all the details you'll need when you launch the `deploy.sh` script:
   1.  Fetch your Service Node computer's Public IP address, then copy/paste it to a temporary text file for easy access. Some options for fetching your Service Node computer's Public IP include:

       ```
       curl ipconfig.io
       curl ifconfig.co
       dig +short myip.opendns.com @resolver1.opendns.com
       ```
   2. Make sure you have easy copy/paste access to your _Servicenode Private Key_ and _Servicenode Address_, which you got earlier from the [Collateral Wallet Setup Procedure](https://docs.blocknet.co/service-nodes/setup/#collateral-wallet-setup-for-automated-service-node-setup).
   3. Think of a name for your Service Node. It doesn't have to be the same name you chose to label the address of your Service Node during the _Collateral Wallet Setup_, but it can be.
   4. Think of a name and a password for the RPC user your Service Node will use for communication with the coin daemons it supports.
6.  Run the `deploy.sh` script:

    ```
    ./deploy.sh
    ```

    You'll be asked if you want to install _docker_. If you have not yet installed _docker_ on your Service Node computer, enter _y_ for "yes." Then proceed to enter the information you prepared in the previous step as the `deploy.sh` script prompts you for each item individually. Note, the values you enter for _Servicenode Private Key_ and _RPC Password_ will not be displayed. If you are pasting in these values, be sure not to paste twice.
7.  (Informational) You should now see the scripts do their magic and launch [docker containers](https://www.docker.com/resources/what-container) for all the daemons you configured your Service Node to support. You can see all the running docker containers by issuing the command:

    ```
    docker ps
    ```

    This command will display the CONTAINER ID, the IMAGE used to build it, the COMMAND running in the container, when it was CREATED, its current STATUS, which PORTS it uses, and any NAMES assigned to it.
8.  To complete the Service Node deployment, we'll need to know either the CONTAINER ID or container NAME of the Service Node container. For that, we can filter the above `docker ps` output through `grep` like this:

    ```
    docker ps | grep snode
    ```

    That command should return information about the _snode_ container, something like this:

    ```
    f9b910221ca2   blocknetdx/servicenode:latest              "/opt/blockchain/sta…"   26 hours ago   Up 26 hours   41412/tcp, 41414/tcp, 41419/tcp, 41474/tcp         exrproxy-env_snode_1
    ```

    The first item returned in this example (`f9b910221ca2`) is the CONTAINER ID, and the last item returned (`exrproxy-env_snode_1`) is the NAME of the container. Either of these two values can be used to access the _snode_ container.
9.  It will take 3.5+ hours for the Blocknet blockchain to sync in your _snode_ container. Periodically monitor the current block height of the Blocknet wallet running in the _snode_ container by issuing the following command:

    ```
    docker exec exrproxy-env_snode_1 blocknet-cli getblockcount
    ```

    Note, here we are executing the command, `blocknet-cli` within the `exrproxy-env_snode_1`container, which is the name we found for the _snode_ container in the previous step. Also note, initial calls to `getblockcount` may return errors until headers finish syncing. This is normal and nothing to be concerned about.
10. When the block height in the _snode_ container matches that of the [Blocknet blockchain explorer](https://chainz.cryptoid.info/block/), your Service Node wallet is fully synced and you can now activate your Service Node as follows:

    1. On your _Collateral Wallet_, issue the command, `servicenoderegister`. If your _Collateral Wallet was set up according to the_ [_VPS Staking guide_](https://docs.blocknet.co/wallet/staking/#staking-from-cli-on-a-vps-running-ubuntu-linux)_, and the alias for `blocknet-cli` was also created according to that guide, you can issue the `servicenoderegister` command as follows:Otherwise, if your \*Collateral Wallet_ is a GUI/Qt wallet running on a different computer, simply enter`servicenoderegister` in _Tools->Debug Console_ of your _Collateral Wallet_.
    2.  On your _Service Node Wallet_, issue the `servicenodesendping` command like this:

        ```
        docker exec exrproxy-env_snode_1 blocknet-cli servicenodesendping
        ```

        (Note, if you created the `snode-cli` alias or shell script as suggested in the _Tip_ above, you can enter simply, `snode-cli servicenodesendping`.)


11. On your _Service Node Wallet_, check to confirm your Service Node is running and supporting all the right coins/SPV wallets like this:

    ```
    docker exec exrproxy-env_snode_1 blocknet-cli servicenodestatus
    ```

    This command should return `"status": "running",` and also the corrrect/expected list of supported services.


12. You can also verify your Service Node is visible on the network by issuing the following command on your _Collateral Wallet_:

    ```
    blocknet-cli servicenodestatus 
    ```



<details>

<summary>Tips for monitoring block height during syncing, and generally accessing blocknet-cli more easily.</summary>

To make access to the `blocknet-cli` program more convenient, you may want to create an alias something like the following:

```
alias snode-cli='docker exec exrproxy-env_snode_1 blocknet-cli'
```

If you add that alias to `~/.bash_aliases` (or any file sourced on login), it will be defined automatically every time you login to your Linux system. Another idea is to create a small Bash Shell script something like this:

```
#!/bin/bash
docker exec exrproxy-env_snode_1 blocknet-cli $*
```

If you create such a shell script, give it a name like `snode-cli`, give it executable permissions (`chmod +x snode-cli`), then move it to some directory in your _$PATH_, then you can use the Linux `watch` utility like this:

```
watch snode-cli getblockcount
```

(Enter `echo $PATH` to see which directories are in your _$PATH_. Enter`man watch` to learn about the `watch`utility and its options.)

</details>

#### Install `fail2ban` to protect your EXR SNode from malicious http attacks (recommended)&#x20;

The following steps are for setting up `fail2ban v0.11.1-1` on `Ubuntu 20.04.3 LTS`. The steps for setting up other versions of `fail2ban` should be very similar, but they may not be exactly the same.

1.  Get the _xr\_proxy-log-path_:

    ```
    docker inspect exrproxy-env_xr_proxy_1 | grep '"LogPath":'
    ```

    This will return something like the following:

    ```
     "LogPath": "/var/lib/docker/containers/6554ded0f7dd2abc0f415a511ff0099c5233fca6e17f2b409e9f40be4d43d9cf/6554ded0f7dd2abc0f415a511ff0099c5233fca6e17f2b409e9f40be4d43d9cf-json.log",
    ```

    The `/var/lib/docker/containers/<big-hex-number>-json.log` part of what's returned is the _xr\_proxy-log-path_ we'll need in future steps, so copy it someplace for future use.
2.  Find your LAN address range. Your LAN address range can be found by issuing this command:

    ```
    ip addr
    ```

    The `ip addr` command will return something like this:

    ```
    1: lo: mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
    valid_lft forever preferred_lft forever
    2: wlp58s0: mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 9c:b6:d0:d0:fc:b5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.20/24 brd 192.168.1.255 scope global dynamic noprefixroute wlp58s0
    valid_lft 5962sec preferred_lft 5962sec
    inet6 fe80::bf14:21e3:4223:e5e4/64 scope link noprefixroute
    valid_lft forever preferred_lft forever
    ```

    In the above output, you can ignore item 1: called _lo_ (loopback). You can see that the IP address range of the LAN in this example is displayed in item 2: just after the word, _inet_: `192.168.1.20/24`. The `/24` at the end tells us that the first 24 bits of this address define the range of the LAN's [subnet mask](https://www.digitalocean.com/community/tutorials/understanding-ip-addresses-subnets-and-cidr-notation-for-networking). `192.168.1.20/24` then represents the full range of addresses used by the LAN in this example system. Copy whatever value represents the full range of the LAN for _your_ system. We'll need it in a future step.
3.  Intall `fail2ban`:

    ```
    sudo apt install fail2ban
    ```
4.  Initialize setup

    ```
    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
    ```
5.  Edit config file: Use a simple text editor like [vi](https://www.tutorialspoint.com/unix/unix-vi-editor.htm) or [nano](https://www.howtogeek.com/howto/42980/the-beginners-guide-to-nano-the-linux-command-line-text-editor/) to edit `/etc/fail2ban/jail.local`. For example:

    ```
    sudo nano /etc/fail2ban/jail.local
    ```

    1.  Within `/etc/fail2ban/jail.local`, search for these 3 commented out lines:

        ```
        #bantime.increment = true
        #bantime.factor = 1
        #bantime.formula = ban.Time * (1<<(ban.Count if ban.Count<20 else 20)) * banFactor
        ```

        Note, these 3 lines will be in different parts of the file, _not_ contiguous as they are displayed above.
    2.  Uncomment those 3 line by removing the `#` at the beginning of each line:

        ```
        bantime.increment = true
        bantime.factor = 1
        bantime.formula = ban.Time * (1<<(ban.Count if ban.Count<20 else 20)) * banFactor
        ```
    3.  Search for the following line

        ```
        #ignoreip = 127.0.0.1/8 ::1
        ```
    4.  Uncomment this line by removing the `#` at the begginning of the line so it looks like this:

        ```
        ignoreip = 127.0.0.1/8 ::1
        ```

        It will also be good to add the full address range of your LAN, as discovered above in step _b_, to the end of this line. This will _whitelist_ all the IP addresses of your LAN so they can't get banned. For example, to _whitelist_ all LAN addresses for the example system of step _b_ above, you would simply add a space and then `192.168.1.20/24` to the end of the `ipignore` line, like this:

        ```
        ignoreip = 127.0.0.1/8 ::1 192.168.1.20/24
        ```

        (Be sure to replace `192.168.1.20/24` here with whatever LAN address range you discovered for _your_ system in step _b_ above.)
    5.  Search for the following line:

        ```
        banaction = iptables-multiport
        ```

        Change it to:

        ```
        banaction = iptables-allports
        ```
    6.  Search for these 3 lines:

        ```
        #
        # JAILS
        #
        ```

        Just below those 3 lines, add the following lines, replacing _xr\_proxy-log-path_ with the_xr\_proxy-log-path_ you found in step _a_ above:

        ```
        [nginx-x00]

        enabled   = true
        port      = http,https
        filter    = nginx-x00
        logpath  = xr_proxy-log-path
        maxretry = 1
        findtime = 3600
        bantime  = 24h

        [nginx-404]

        enabled  = true
        port     = http,https
        filter   = nginx-404
        logpath  = xr_proxy-log-path
        maxretry = 1
        findtime = 3600
        bantime  = 1h
        ```

        After replacing _xr\_proxy-log-path_ with the value you found in step _a_ above, the `logpath =` lines will look something like this:

        ```
        logpath  = /var/lib/docker/containers/<big-hex-number>-json.log
        ```
    7. Save your edits to `/etc/fail2ban/jail.local` and exit the editor.
6. Add Filters:&#x20;
   1.  Use a simple text editor like _vi_ or _nano_ to create the file,`/etc/fail2ban/filter.d/nginx-x00.conf`. For example:

       ```
       sudo nano /etc/fail2ban/filter.d/nginx-x00.conf
       ```

       Add the following lines to the file:

       ```
       [Definition]
       failregex = ^{"log":"<HOST> .* .*\\x
       ignoreregex =
       ```

       Then save the file and exit the editor.
   2.  Use a simple text editor like _vi_ or _nano_ to create the file,`/etc/fail2ban/filter.d/nginx-404.conf`. For example:

       ```
       sudo nano /etc/fail2ban/filter.d/nginx-404.conf
       ```

       Add the following lines to the file:

       ```
       [Definition]
       failregex = {"log":"<HOST>.*(GET|POST|HEAD).*( 404 )
       ignoreregex =
       ```

       Then save the file and exit the editor.
7.  Restart `fail2ban` service:

    ```
    sudo service fail2ban restart
    ```
8.  Verify `fail2ban` is running properly:

    ```
    sudo service fail2ban status
    ```
9.  Check the logs of `fail2ban`:

    ```
    sudo tail -f /var/log/fail2ban.log
    ```

    (Ctrl-C to exit scrolling logs.)
10. Fix iptables. To complete this last step, you must wait for at least one IP address to get banned in each of the two jails we created above (`nginx-x00` and `nginx-404`). This may take a few hours, so you may want to just let `fail2ban` run overnight before coming back to this step. Then check the `fail2ban` logs to confirm there has been at least one IP banned in each of the new jails:

    ```
    sudo less /var/log/fail2ban.log
    ```

    Search with `less` for `nginx-404` and `nginx-x00` to confirm at least one IP ban in each jail. Once this has been confirmed, you can fix the system IP tables so the `fail2ban` logs will no longer print the "Already Banned" messages. Fix the IP tables by issuing these two commands:

    ```
    sudo iptables -I FORWARD -j f2b-nginx-x00
    ```

    ```
    sudo iptables -I FORWARD -j f2b-nginx-404
    ```
