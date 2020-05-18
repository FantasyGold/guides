# Staking with a VPS

Many users prefer using a VPS for staking purposes, it is safer than using your local machine and it is more convenient for most people as you don't need to leave your computer turned on 24/7, there are also some very cheap and stable solutions you can use.

In this tutorial we'll show how to do this using **DigitalOcean**  (please use our ref. link, it helps reduce the projects overhead) https://m.do.co/c/8148cc9b9f55 | the same principles apply to any other cloud provider you may prefer.



## Launching instance



Let's begin, we log into our dashboard where we create a new Droplet.

<img src="dig1.png" width="800">

Choose a server type, our linux wallet runs on Ubuntu 18.04, You can select any plan you want, we went with a basic $5 VPS and you can choose any location for the VPS.. 









#### SSH Keys

It is recommended to use ssh-key to login instead of passwords, its far more secure and convenient.

Creating ssh-keys is out of the scope of this tutorial, but here are some good references on how to do this:

https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2

https://docs.joyent.com/public-cloud/getting-started/ssh-keys/generating-an-ssh-key-manually/manually-generating-your-ssh-key-in-windows < *this one is for Windows users.*



After we've created our SSH key, we click on "New SSH Key"

<img src="ssh.png" width="800">



Here we can paste our SSH-key, enter a name for it and click on add ssh key.

## Logging in to your VPS



Once we have our credentials ready, we log in and see the following screen:

<img src="root.png" width="800">



### Initial Server Setup with Ubuntu 18.04

Word of caution before moving forward, basic security and VPS hardening is out of scope for this tutorial. You are responsible for your own security methods here are a few guides to help you get started.

https://www.lifewire.com/harden-ubuntu-server-security-4178243

https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04

https://www.digitalocean.com/community/tutorials/an-introduction-to-securing-your-linux-vps 


​

### Downloading the FantasyGold wallet

AFTER we have our server nice and secure need to download the FantasyGold linux wallet, here's how:

``` wget https://github.com/FantasyGold/FantasyGold-Core/releases/download/2.0.0/FantasyGoldCore-v2.0.0-Linux64.tar.gz ```

Copy and Paste the above command into your terminal this will start the download.

Once its done we need to untar the file.

``` tar -xvzf FantasyGoldCore-v2.0.0-Linux64.tar.gz ```

The wallet will be located in the bin file, you can move fantasygoldd and fantasygold-cli files to any location you like or leave them

``` cd bin ```

now move the fantasygoldd and fantasygold-cli files to /usr/local/bin/ 

``` mv fantasygoldd fantasygold-cli /usr/local/bin ```

you can check by typing

`ls /usr/local/bin/`

### Launching FantasyGold daemon

 `./fantasygoldd -daemon`  -> This launches the fantasygold daemon and the blockchain begins to synchronize right after launching. It can take some minutes before it's fully synced.

### Encrypting wallet

We can encrypt the wallet at any time, it's better to do it before we go any further.

To do this, type the following on the command line:

`./fantasygold-cli encryptwallet yourpassword`

Replace `yourpassword` with a long and secure password and make sure you write it down and keep it safe, if you lose this password you have lost ALL your coins!   

This will encrypt the wallet which in turn closes the daemon, you'll see the following message:

`wallet encrypted; FantasyGold server stopping, restart to run with encrypted wallet. The keypool has been flushed and a new HD seed was generated (if you are using HD). You need to make a new backup.`

You will need to restart the wallet after a minute `./fantasygoldd -daemon`

`./fantasygold-cli getaccountaddress ""` -> Right after launching the daemon, you can obtain your wallet address by typing this.

You can send FantasyGold coins to the address we just obtained from the daemon, please remember that those transactions require at least 500+ confirmations before they become mature enough for staking.



### Staking

Now that we've waited until we have at least 501 confirmations on our received transaction, we are elligible for staking, however, if our wallet is encrypted (which we did for security reasons) we won't be able to stake, let's open our wallet for staking using the command line!.

`./fantasygold-cli walletpassphrase password 999999999 true`

The above command will unlock the walet **for staking only** for 31.6 Years! that should be enough for now. Please note, this will not unlock your backup, only the wallet that's running right now.

Now that we've unlocked our wallet, we need to wait until we have more than 501 confirmations to be elligible for staking, if we already do, it's a matter of time which will vary depending on the network weight vs your wallet's weight.

#### Checking Balance

To check your balance, type `./fantasygold-cli getwalletinfo` this will show general information, including your available balance and balance in staking

#### Check transactions

To check your transactions (incoming and outgoing) type `./fantasygold-cli listtransactions`

#### Check staking info

To check FantasyGold's staking information, type `./fantasygold-cli getstakinginfo`



### Staking tips

Staking really depends on network weight vs your wallet’s weight which is based on the amount of coins you have, higher weight increases your chances of staking a block.

If you have a large amount of coins, it’s a good idea to split those up in separate transactions, for instance, if you have 10.000 FGC, it’s better to send 10 transactions of 1000 FGC each to your wallet, each one generates a UTXO input which will take part in staking. This optimizes the staking process and works much better than just one large 10.000 FGC input.

If you want to split your coins into different addresses inside your VPS wallet, type the following to obtain new addresses inside your wallet: `./fantasygold-cli getnewaddress`
Each time you type this, you’ll get a new address, FGC can generate any amount of addresses you want, but please keep in mind, if you do go over 100 new address, you might want to make a new backup of your wallet.




### Wallet Backup

Backing up your wallet from a Linux VPS is different from a desktop but not too complicated, there's several ways to do this, and here are some steps which should work on all major desktop OS.

You can use Filezilla or WinSCP, both are easy to use and secure using SFTP. 

https://filezilla-project.org

https://winscp.net

Installing is just like any other app.

Afer inputting the IP address of your VPS you'll need to go into the advanced settings add the path to your ssh key 

<img src="key.png" width="800">


###
After logging in go to the /root/ folder of your VPS, this is where your wallet runs and has the wallet stored in /root/.fantasygold we can go ahead and enter the folder 
and find the wallet.dat, right click and select download. This will download the wallet.dat file to our computer, we've successfully backed up our FantasyGold wallet!.


