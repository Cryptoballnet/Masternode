![Example-Logo](https://avatars.githubusercontent.com/u/80650691?v=4)

# cryba Masternode Setup Guide
***
## Required
1) **cryba collateral value at current block** ([consult the collateral table](../../README.md#rewards-breakdown))
2) **Local Wallet https://github.com/Cryptoballnet/cryba/releases**
3) **VPS with UBUNTU 18.04** (it is possible to work on other versions but it is not tested)
4) **Putty https://www.putty.org/**
5) **Text editor on your local pc to save data for copy/paste**
***

***On your Local Wallet***
* Create an address with a label MN1 and send exactly the collateral amount to it ([consult the collateral table](../../README.md#rewards-breakdown)). Wait to complete 6 confirmations on “ Payment to yourself “ created.

* Open the Debug Console ( Tools – Debug Console ) and type ***createmasternodekey***.
You will then receive your private key, save it in a txt to use it later.
  ```
  Example:
          createmasternodekey
          7R1f1rNnB67BnosqGSZA2gk7U3SAR72QmMiZBL5qXcDu5cWtRpU
		 
* Still at Debug Console type ***getmasternodeoutputs*** and save txhash and outputidx on a txt
  ```
  Example:
          "txhash" : "12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa",
		         "outputidx" : 0

***On Putty***

* Once logged in your vps, *copy/paste* each line one by one with *Enter*

```
wget -q https://raw.githubusercontent.com/Cryptoballnet/Masternode/master/contrib/masternodesetup/masternodesetup.sh
```

```
bash masternodesetup.sh
```

* Let this run, and when it ask you to install dependencies, if you're not sure press ***y*** and then enter

* It will take some time and then will ask to compile the Daemon, press ***y*** and then enter 

* Last thing script will ask you is to provide Masternode Genkey. Copy the one you got previously (createmasternodekey) and press enter.

Remember to do `cryba-cli getblockcount` to check if VPS catching blocks till it synced with chain, if not follow this procedure:

* Go to your wallet-qt and check peers list (tools - peers list) and select one ip from the list. With that ip do the follow command at VPS `cryba-cli addnode "ip" onetry`

      Example:
		  cryba-cli addnode 144.91.111.155 onetry
    
* Check now if VPS already downloading blocks with the command `cryba-cli getblockcount`, and if yes give it time now to catch last block number 

Do not close your terminal/ command prompt window at this point.

***Go back to your Local Wallet***

* Open the Masternode Configuration file (tools – open masternode configuration file) and add a new line (without #) using this template (bold needs to be changed) in the final save it and close the editor

**ALIAS VPS_IP**:22489 **masternodeprivkey TXhash Output**

		Example:
		MN1 125.67.32.10:22489 7R1f1rNnB67BnosqGSZA2gk7U3SAR72QmMiZBL5qXcDu5cWtRpU 12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa 0

* Close and Re-open Local Wallet, and at Masternode Tab you will find your MN with status MISSING

***(For the next steps you need to have already 16 confirmation on “Payment to yourself “ created in first step)***

* Go to Debug Console type the following: ***startmasternode alias 0 (mymnalias)***

		Example:
		startmasternode alias 0 MN1
***

***Go back to Putty***

```
cryba-cli getmasternodestatus
```

You need to get **"status" : 4** 

## Congratulations your cryba node it's running
