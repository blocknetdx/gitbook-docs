# Installation Guide

Installing the Blocknet wallet is a simple process. Below are step-by-step instructions for how to install the wallet on each operating system (OS).

**NB:** There are two wallet variations, a redesigned interface (default) and a classic interface. To use the classic wallet, you'll need to open your `blocknet.conf` file and add `classic=1` on a new line (you may not have a `blocknet.conf` file and will need to create one). You can find the `blocknet.conf` file in your Blocknet data directory:

*   **Windows**

    ```
    C:\Users\[YourUsername]\AppData\Roaming\Blocknet\
    ```

    Or paste `%appdata%\Blocknet\` into the File Explorer path field.
*   **MacOS**

    ```
    ~/Library/Application Support/Blocknet/
    ```

    Open Finder and in the _Go_ menu select _Go to Folder..._ and enter the above path.
*   **Linux**

    ```
    ~/.blocknet/
    ```

**Redesigned Wallet (default):**

![](https://docs.blocknet.co/img/wallet-redesign/wallet-redesign.png)

**Classic Wallet:**

![](https://docs.blocknet.co/img/wallet-classic/wallet-classic.png)

## Install GUI Wallet <a href="#install-gui-wallet" id="install-gui-wallet"></a>

### **Install on** Windows

![](https://img.youtube.com/vi/r4Xs0RrbAOw/0.jpg)

1.  Download the [latest Blocknet wallet](https://github.com/blocknetdx/blocknet/releases/). There are 2 options:

    1. `blocknet-x.xx.x-win64-setup-unsigned.exe` (recommended for 64-bit)
    2. `blocknet-x.xx.x-win64.zip`

    Note: Antivirus software may be flagged

    It is normal for antivirus software to flag the wallet as potentially dangerous. This is a common issue with most wallets, including Bitcoin's. As long as the wallet was downloaded from [https://blocknet.co](https://blocknet.co/), [https://xlitewallet.com](https://xlitewallet.com/), [Blocknet's Github](https://github.com/blocknetdx/blocknet/releases) or [Blocknet's XLite Github](https://github.com/blocknetdx/xlite/releases), it can be deemed as safe and the warning can be ignored. You may need to temporarily disable antivirus download protection to complete the download. You can read more about this issue here: [https://bitcoin.org](https://bitcoin.org/en/bitcoin-core/features/requirements#possible-problems).
2. Before continuing, it is recommended to [verify your download](https://docs.blocknet.co/wallet/installation/#verifying-downloads)
3. Continue to the instructions below for the download you selected:

**Needs to be finsihed...**

### **Install on Mac OS**

1. Download the [latest Blocknet wallet](https://github.com/blocknetdx/blocknet/releases/). There are 3 options:
   * `blocknet-x.xx.x-osx-unsigned.dmg` (recommended)
   * `blocknet-x.xx.x-osx-unsigned.tar.gz`
   * `blocknet-x.xx.x-osx64.tar.gz`
2. Before continuing, it is recommended to [verify your download](broken-reference)
3. Find the downloaded file. The default location is in _Downloads_.
4. Double-click the file to begin installation.
5. Click and drag the _Blocknet-Qt_ application icon over to the _Applications_ folder and release.
6. Open _Finder_, navigate to _Applications_, and find _Blocknet.app_ in the list of applications.
7. Right-click the file and select _Open_. If using the touch pad this can be done by clicking with 2 fingers.
8. If you are prompted with a message asking if you are sure you want to open the application, select _Open_.\
   \
   **Note:** If you see a message like the one below instead of the one above, click _Cancel_ and repeat step 5 above:\
   ![Finder](https://docs.blocknet.co/img/wallet/mac-open-confirm-extra-step.png)
9. Your computer will begin verifying the application. This may take a few minutes to complete.
10. An installation prompt will appear, select _OK_.
11. Installation is now complete.

{% hint style="warning" %}
**Note: Antivirus software may be flagged**\
****It is normal for antivirus software to flag the wallet as potentially dangerous. This is a common issue with most wallets, including Bitcoin's. As long as the wallet was downloaded from [https://blocknet.co](https://blocknet.co/), [https://xlitewallet.com](https://xlitewallet.com/), [Blocknet's Github](https://github.com/blocknetdx/blocknet/releases) or [Blocknet's XLite Github](https://github.com/blocknetdx/xlite/releases), it can be deemed as safe and the warning can be ignored. You may need to temporarily disable antivirus download protection to complete the download. You can read more about this issue here: [https://bitcoin.org](https://bitcoin.org/en/bitcoin-core/features/requirements#possible-problems).
{% endhint %}

***

### **Install on** Linux

1.  Download the [latest Blocknet wallet](https://github.com/blocknetdx/blocknet/releases/). There are 2 options

    1. `blocknet-x.xx.x-x86_64-linux-gnu.tar.gz` (recommended for 64-bit)
    2. `blocknet-x.xx.x-arm-linux-gnueabihf.tar.gz` (recommended for Raspberry Pi)

    Note: Antivirus software may be flagged

    It is normal for antivirus software to flag the wallet as potentially dangerous. This is a common issue with most wallets, including Bitcoin's. As long as the wallet was downloaded from [https://blocknet.co](https://blocknet.co/), [https://xlitewallet.com](https://xlitewallet.com/), [Blocknet's Github](https://github.com/blocknetdx/blocknet/releases) or [Blocknet's XLite Github](https://github.com/blocknetdx/xlite/releases), it can be deemed as safe and the warning can be ignored. You may need to temporarily disable antivirus download protection to complete the download. You can read more about this issue here: [https://bitcoin.org](https://bitcoin.org/en/bitcoin-core/features/requirements#possible-problems).
2. You may be asked for a confirmation to download, select _Save File_ then _OK_.
3. Find the downloaded file. The default location is in _Downloads_.
4. Before continuing, it is recommended to [verify your download](broken-reference)
5. Right-click the file, select _Extract Here_.
6. Double-click the `blocknet-x.xx.x-x86_64-linux-gnu/` folder to view the contents.
7. Double-click the `blocknet-x.xx.x/` folder to view the contents.
8. Double-click the `bin/` folder to view the contents.
9. Here you will find the `blocknet-qt` executable file.
10. Move this file you where you keep your applications, such as your _Desktop_.
11. After moving this file, the files you downloaded can be deleted since the `blocknet-qt` executable file is all that is needed.
12. Double-click the `blocknet-qt` file to begin the installation process. (If it fails to open on double-click, you may need to give _executable_ permission to the file: Either `sudo chmod +x blocknet-qt` in Debian terminal, or Right-click property, give executable permission.)
13. An installation prompt will appear, select _OK_.

### Install CLI Wallet on Linux <a href="#install-cli-wallet-on-linux" id="install-cli-wallet-on-linux"></a>

See Staking from CLI on a VPS running Ubuntu Linux

***

### Verifying Downloads <a href="#verifying-downloads" id="verifying-downloads"></a>

{% hint style="warning" %}
It is important to verify the integrity of downloads before running them. Depending on how you downloaded it, it's possible the file may have been modified in transit to do something evil when run. The server hosting the download may also have been compromised.
{% endhint %}

1.  Get the sha256 hash of the release you download. These are provided on the Github release page either in a file called `sha256sums.txt` or as a plain text in the release notes. The format follows `SHA256(filename)= hash`. Here is an example of the hashes:

    ```
    SHA256(blocknet-3.13.1-arm-linux-gnueabihf-debug.tar.gz)= 77e6c3e5d1e6ef9f0d54a8f0fe3d638b1c6bd889e609c6a69bb8f82322117847
    SHA256(blocknet-3.13.1-arm-linux-gnueabihf.tar.gz)= 94705029ebf05b0aa2b0939dd0da0663e578accbf5dca8e9393456d9d40edde6
    SHA256(blocknet-3.13.1-i686-pc-linux-gnu-debug.tar.gz)= 30039c5eb3951a73d578f613d072a79610cb3983113cf816fbed485ce44bd57c
    SHA256(blocknet-3.13.1-i686-pc-linux-gnu.tar.gz)= c5c9013b5e0539a99825339f98a460281014b3dca5d970e24faa860b6fd0c0e7
    SHA256(blocknet-3.13.1-osx-unsigned.tar.gz)= 0d5be3dedc83521349b5def54c1f045f1cd35c67d8da5beb50c90beaa50ae659
    SHA256(blocknet-3.13.1-osx64.tar.gz)= 438b0b82001ca5ce0af8300061207f87421c3c9cfeab47dd4c56ebc856b357da
    SHA256(blocknet-3.13.1-win-unsigned.tar.gz)= 1f81058be74d3714f1e07f5b16562f471cd2da1fac8251b3c3d414dba5b0d271
    SHA256(blocknet-3.13.1-win32-debug.zip)= fdc15df95dbb1293d59a2a9b90bf421594b0dc27320cd09cf31dcc9073bb2a8e
    SHA256(blocknet-3.13.1-win32-setup-unsigned.exe)= c89200719d3e55f9f7eee1cf8f77a4a4c43d8c4551b896a4f0d7617a935f31e0
    SHA256(blocknet-3.13.1-win32.zip)= 60c0805f00fe4e1c1e93af2ef3e93fb0fbe3b7bcf2385f8192c1a176b4068c3f
    SHA256(blocknet-3.13.1-win64-debug.zip)= e739bf19e5d826ff9750c9ae9dfddf0bf17b9e6da2d90e094698c02171454a6f
    SHA256(blocknet-3.13.1-win64-setup-unsigned.exe)= 350d67cdb009a7b4d3101dae145caa9c69e8c7a2ca6252a4d97aedf33a5a3f9d
    SHA256(blocknet-3.13.1-win64.zip)= f1f472353f034e1151345c167a48a01d1ceafdd2b7a5b7a5cc82df9cbef6ce6d
    SHA256(blocknet-3.13.1-x86_64-linux-gnu-debug.tar.gz)= 998fa0487cc4e8fc2be9fb004cd6eb9bc0e91d690da110a5073e3f3b50bd2938
    SHA256(blocknet-3.13.1-x86_64-linux-gnu.tar.gz)= 9608a66feb4616092ddb2dbeeafef01f5c0c28b61cccf13bcd032cee3981be74
    ```
2. Take a note of the hash for the specific file you downloaded.
3.  Get the sha256 hash of the file you downloaded:\
    \
    **Windows:**

    1. Open the command prompt.
    2. Navigate to the location of the downloaded file.
    3. Enter `certUtil -hashfile filename SHA256` with `filename` replaced by the name fo the file you downloaded.&#x20;

    Example: **** `certUtil -hashfile blocknet-3.13.1-win64.zip SHA256`\
    ``\
    ``**Mac:**

    1. Open the command prompt.
    2. Navigate to the location of the downloaded file.
    3. Enter `certUtil -hashfile filename SHA256` with `filename` replaced by the name fo the file you downloaded.&#x20;

    Example: **** `certUtil -hashfile blocknet-3.13.1-win64.zip SHA256`\
    ``\
    ``**Linux:**

    1. Open the command prompt.
    2. Navigate to the location of the downloaded file.
    3. Enter `certUtil -hashfile filename SHA256` with `filename` replaced by the name fo the file you downloaded.&#x20;

    Example: `certUtil -hashfile blocknet-3.13.1-win64.zip SHA256`\
    ``
4. Compare the release hash to the hash of the download. If the hashes do not match, **DO NOT** run the file and delete the file immediately.
