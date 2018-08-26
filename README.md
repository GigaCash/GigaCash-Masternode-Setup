# GigaCash Masternode Setup Guide

> Follow the steps below to setup and install your GigaCash masternode<br><br>

## 1. Wallet setup
* 1.1 Download the [latest wallet](https://github.com/GigaCash/GigaCash/releases) for your operating system.<br>
* 1.2 Launch the wallet and allow it to synchronize with the other nodes.<br />
* 1.3 Click on `debug console` found in `tools`
![Imgur](https://i.gyazo.com/2b22c2a6f2f050f84357989ee67bb88a.png)
* 1.4 Type `masternode genkey` and copy the generated key into a text file for future use, then close the console.<br />
* 1.5 Go to `receiving addresses` found in `file` - create a new masternode wallet address and call it `mn1`. <br />
![Imgur](https://i.gyazo.com/8a4ef87618bcb7c8e61f8cebb5c22dad.png)
Copy the address by right-clicking and selecting "Copy Address"<br>
* 1.6 Send EXACTLY 10,000 coins to `mn1` wallet by pasting the copied address.<br>
Note that this has to be sent in **ONE transaction**. <br />
* 1.7 Go back to `debug console` and type `masternode outputs`. <br />
* 1.8 Copy the transaction id and output id and save it to the text file for future use.

## 2. Get a VPS ( masternode server )
We recommend renting a DigitalOcean VPS as they are fast and easy to setup.

* 2.1 Create an account:<br>
![Create account](https://i.gyazo.com/5615c4d87bcc1df2c4de7446f8bd671b.png)<br>
* 2.2 Deploy a new server
* 2.3 Choose a location close to you to have a fast connection
* 2.4 Choose Ubuntu 16.04  x64 as operating system and take the 5$ server size. This is sufficient.<br>
![Server size](https://i.gyazo.com/4c26198fe7b80283917f24afd5b70d49.png)<br>
* 2.5 Move to step 7 and give your masternode VPS a name.<br>
![Masternode name](https://i.gyazo.com/f57ea7b2bd7e7acf555d1ce412a91e7e.png)<br>
* 2.6 Click "Create"<br>
The server is now being created you may need to wait a few minutes.
* 2.7 Go you your email
In your email you will receive the access details for your vps you will need the IP, USERNAME & PASSWORD

## 3. Configure your masternode

### 3.1 Install PuTTY - [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
* Once you open the program you will see the following:<br>
![Imgur](https://i.imgur.com/X1k9vXi.png)<br>
* Fill the Host name field with the IP address you previously received in the email and click "Open".<br>
* You will now see a popup asking you if you trust this host, you will need to choose Yes.
![Imgur](https://i.imgur.com/Y2iEDj8.png)<br>
* Now you will be asked to enter your username which was provided in the email usually this is "root".
* Next you will be asked to enter your password which was provided in the email copy it and right click in the putty terminal and hit ENTER.
* You are now logged into your server:
![Imgur](https://i.gyazo.com/fafb3a79f1e174a049973964255746a9.png)<br>
### 3.2 General Setup
Update your system to the latest version to make sure you are secure.
* Type: `sudo apt-get update`  ENTER
* Wait until this has finished
* Type: `sudo apt-get upgrade` ENTER
* Type "y" if the system asks you, so you can update the system.

> Now we will use the easy setup Masternode Script<br>

* Type: `cd ~`  ENTER
* Type: `wget https://raw.githubusercontent.com/GigaCash/GigaCash-Masternode-Setup/master/setupmn.sh` ENTER
* Type: `bash setupmn.sh` ENTER
* You will now be asked to type or copy your masternode private key after making sure it is correct press ENTER.
* Your masternode is now setup on your VPS now all you need to do is setup your desktop wallet

## 4. Masternode Configure Desktop wallet

4.1 Go to `open masternode configuration file` in the wallet - found on the 'tools' menu if asked what program to use to open it choose notepad <br />
   Here you will see the format and an example( these three lines are comments so they have no effect ) <br />
The format is like this:

```
# Masternode config file
# Format: alias IP:port masternodeprivkey collateral_output_txid collateral_output_index
# Example: mn1 127.0.0.2:5078 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0
```

4.2. Add your own node details under it. <br />
4.3. Put the masternode wallet name, i.e - `MN01` <br />
4.4 Put the server IP address followed by the port :5078 <br />
4.5 Put the private key generated in step 1.4 <br />
4.6 Put the transaction hash and output id from step 1.7 <br />
Example below

```
mn1 128.893.2.0:5078 A3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8bC dgcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a667 0
```

4.7 Once complete, save the file <br />

The file will look like this:
```
# Masternode config file
# Format: alias IP:port masternodeprivkey collateral_output_txid collateral_output_index
# Example: mn1 127.0.0.2:5078 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0
mn1 128.893.2.0:5078 A3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8bC dgcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a667 0
```
4.8 Restart the wallet<br>
4.9 Go to your wallet and go to the masternode page.<br>
4.10 Go to tools > debug console<br>
4.11 Type <startmasternode "alias" "0" "mn1"> where mn1 is the name of your masternode<br>


To verify that the masternode is running on the vps:
* Type: `cd ~`  ENTER
* Type: `Gigacash-cli masternode status`  ENTER
* If you get this output you are done:<br>
![Imgur](https://i.imgur.com/tWVgO2O.png)

<br>

>Congratulations, you have now setup your masternode<br>

If you are needing any help or have a question you can join our Discord and we will help you.
<br>
<br>
>Based on Zoldur's MN scripts