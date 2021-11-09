# Manual installation

## Desktop Wallet Setup

- Make sure you have a ful node in your vps here's [how to get](en/wallet/fullnode.md)
- Have your QT wallet installed on your [windows pc](https://github.com/BdcashProtocol/bdcash-protocol/releases/latest)

### Requirements
-  More than 5000 BDCASH
- One computer with BigDataCash wallet installed. Make sure the wallet contains the Masternode Collateral of at least 5000 BDCASH.
- One VPS.
- A decent amount of technical knowledge. i.e. Knowing what a VPS is and using basic Linux shell commands.
-  Patience – enough to follow these instructions properly before asking questions!

###  Step 1:
Setup your BDCASH wallet – this will keep your coins safe. Install bigdatacash-qt wallet on Windows or Linux from the official github.

1.1. Load your bdcash-qt wallet and sync.

1.2. Set a password for bdcash-qt. (Wallet will shut down)

1.3. Find yourwallet.dat file: e.g. c://Usersusername/AppData/Roaming/bdcash (windows file path)

1.4. Backup your private keys and wallet.dat file! (Very important! You may lose your coins if you don’t backup!)

1.5. Exit the wallet application and then re-open it. Let it synchronize.

### Step 2:
Accessing the debug console in the QT-wallet

2.1. Open the Debug Console.

2.2. Click Tools on the top file menu.

2.3. Open Debug console.

2.4. Click Console on the top Tab Bar.

### Step 3: 
Obtaining your masternode genkey & address

3.1. In the debug console command box (bottom of the window) enter the following:

3.2. You should see something very similar to this. It’s your MN_GENKEY (save into a text file in Notepad or Gedit/Nano/etc.

3.3. Enter the following to create a masternode address (ENTER): (Replace with your MASTERNODE_ALIAS_NAME.)

3.4. You should see something very similar to this (save into a text file in Notepad or Gedit/Nano/etc):

- createmasternodekey
- createmasternodekey
- 5K……………………………………….98iX <- you keygetnewaddress mn1
- getnewaddress mn1
- 8M4Dr………………………………………..sTCusH

### Step 4:
Wallet set up for masternode

4.1. Open your bdcash-qt Wallet

4.2. Click Send Tab

4.3. Send 5000 BDCASH to the address [MASTERNODE_ALIAS_NAME]

4.3. Wait for ALL confirmations to complete (See the Transactions tab in wallet for more details).

4.4. Open Debug console once more (see step 3 instructions on accessing this).

4.5. Enter the following to get outputs( ENTER):

4.6. You should see something very similar to this (save into a text file in Notepad or Gedit/Nano/etc):

- They are your TX_ID and TX_INDEX, {“TX_ID”:“TX_INDEX”}

4.7. Open the options menu in your wallet and enable the masternode tab. This will allow you to see you Masternodes easily via the Graphical User Interface (GUI) of the wallet. You can also use this once you have completed all steps to start nodes.
- getmasternodeoutputs
- { “30a988b50……………………………….d4c25a4de91f898”:“0” }

### Step 5:
Edit “masternode.conf” file

5.1. Find your masternode.conf file For example – In windows, it would be located in the following directory: c://UsersusernameAppDataRoaming/bdcash

5.2. Open masternode.conf with Notepad, You should see something very similar to this.

5.3. Format your masternode information?

**Please note – the Masternode Config file should have only one line of text. All other lines should be commented out with # at the beginning of each line.**

5.4. Paste masternode information [step5.3] into masternode.conf on new line.

5.5. Save and close masternode.conf
-  Masternode config file
-  Format: alias IP:port masternodeprivkey collateral_output_txid collateral_output_index
-  Example:
- mn1 ip_you_vps:36264 5K……………………………………….98iX 30a988b50……………………………….d4c25a4de91f898 0

### Step 6: 
Start your masternode!

9.1. Restart local wallet and Open the Debug Console.

9.2. Enter the following to start your Masternode(MASTERNODE_ALIAS_NAME from step3.3):

9.3. You should see something very similar to this:

9.4. You can use the following commands on the VPS to see the status of Masternode:
- startmasternode alias 0 mn1
- “alias” : “MASTERNODE_ALIAS_NAME”,
- “result” : “successful”
- ./bdcash-cli getmasternodestatus
9.5. Keep your VPS and PUSHI services running

