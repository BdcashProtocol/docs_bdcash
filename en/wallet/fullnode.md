# BDECO Full Node

## Step 1: 
Set up your server hosting (VPS)

- If you have access to your own Linux Ubuntu Server running at least V16.04 with a static IP, DDOS protection and all behind a nicely configured firewall then feel free to skip this step. Otherwise, if you understood nothing in the above-mentioned paragraph then I suggest you stop now before you launch the nukes by mistake.
- If you do on the other hand have technical understanding but you do not have access to the hardware or the technical skills to manage the hardware, then VPS is for you (Virtual Private Server).
- Hit the big VULTR button below and sign up for an account (DISCLAIMER: It will ask for a credit card and it will cost you fees to run this service every month). Set up a new Ubuntu Server and obtain your SSH credentials.

## Step 2:

Install and update some needed libraries & Install bigdatacash hot wallet.

7.1. To install the libraries, please run each of the following lines INDIVIDUALLY (do not try to script them) and take care to make sure you run ALL commands.

- sudo apt-get update
- sudo apt-get upgrade
- sudo apt-get install build-essential libtool bsdmainutils autotools-dev autoconf pkg-config
- automake python3 git automake nano
- sudo apt-get install libssl-dev libgmp-dev libevent-dev libboost-all-dev
- sudo apt-get install software-properties-common
- sudo add-apt-repository ppa:bitcoin/bitcoin
- sudo apt-get update
- sudo apt-get install libdb4.8-dev libdb4.8++-dev
- sudo apt-get install libminiupnpc-dev
- sudo apt-get install libzmq3-dev

7.2. Create Swap Space (Important – otherwise, you may fail to compile):

If any of the above-mentioned commands fail, go back to Step 7 and reinstall ALL dependencies one by one.

7.3. Get the source code and compile it (This process will take some time, please be patient):

7.4. Create .bdcashprotocol directory:
- git clone https://github.com/BdcashProtocol/bdcash-protocol bdcash
- cd /root/bdcash/
- . ./autogen.sh
- ./configure CXXFLAGS=”–param ggc-min-expand=1 –param ggc-min-heapsize=32768″ — without-gui
- make
- fallocate -l 3G /swapfile
- chmod 600 /swapfile
- mkswap /swapfile
- swapon /swapfile
- echo -e “/swapfile none swap sw 0 0 ” >> /etc/fstab (Error will appear here, do not worry; If it stop here you can use CTRL + C to stop it.)
- chmod +x autogen.sh
- chmod +x share/genbuild.sh
- cd /root/bdcash/src
- .bdcashd

## Step 3:
Edit bdcashprotocol.conf file & Start the service.

8.1. Edit bdcashprotocol.conf file:

Modify the above information:
- Change YOUR_USER_NAME to a username
- Change YOUR_PASSWORD to a secure password (random is recommended)
8.3. Save and exit (CTRL + X).

8.4. Start the BdcashProtocol  server:
- nano /root/.bdcashprotocol/bdcashprotocol.conf
- cd /root/bdcash/src/
- ./bdcashd
8.5. You can use the following command to get more info
- ./bdcash-cli getinfo
8.2: Copy and paste the following into bdcashprotocol.conf:
- rpcuser=YOUR_USER_NAME
- rpcpassword=YOUR_PASSWORD
- rpcallowip=127.0.0.1
- listen=1
- server=1
- daemon=1
- maxconnections=256
- masternode=1
- logtimestamps=1