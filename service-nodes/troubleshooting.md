# Troubleshooting

* Ensure you have the latest wallet and that it's fully synced.
* Ensure the SNode Wallet is open and synced before using the `servicenoderegister` from the Collateral Wallet.
* Ensure that you have at least 5000 BLOCK per Service Node in your designated `[NODE_ADDRESS]`.
* Ensure that your 5000 BLOCK accidentally didn’t send to a change address (if creating inputs manually).
* Ensure all your inputs have at least 2 confirmations before registering.
* Ensure you didn't include the `[` or `]` when typing commands and replacing the variables. Example:
  * Correct: `getnewaddress snode1`
  * Incorrect: `getnewaddress [snode1]`
* If you manually setup your Service Node (this guide shows the automatic procedure):
  * Ensure your `servicenode.conf` information is correct to your settings.&#x20;
  * Ensure that the `servicenode.conf` matches on both the Collateral and Service Node Wallets.
  * Ensure your configuration file is `servicenode.conf` and **NOT** `servicenode.conf.txt`.
