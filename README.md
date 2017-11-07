# Masternode-Setup-Guide

Step 1:	You will need a Kore wallet on your local machine with atleast 500.1 Kore in your wallet.

Step 2:	You will need a Linux based VPS. We recommend Ubuntu 16 or later. Any VPS provider will do, but you can use a VPS service like Digital Ocean to quickly spin up a VPS in minutes. Make sure you acquire your root username and password.

Step 3:	Open up an SSH connection to your VPS. If you have never used SSH before, we suggest YouTube for some how to tutorials. At this point, you should be logged into SSH connected to your VPS ready to enter commands.

Step 4:	At the root command line run these:


  sudo apt-get
  
  sudo apt-get upgrade -y
  
  sudo apt-get install nano
  
  sudo apt-get install git
  
  nano test.sh
  
now you're inside a temp text file

Copy all text below and then paste it into the test.sh (text inside the *s)

Say Yes when asked if you want to paste

press Ctl o -- not zero the letter o

press Enter

press Ctl x

press Enter

  chmod +x test.sh
  
  ./test.sh


  ************************************************************************
  If you have a VPS with 4GB of RAM or less use this code
  ************************************************************************
  fallocate -l 4G /swapfile
  chmod 600 /swapfile
  mkswap /swapfile
  swapon /swapfile
  clear
  #Install Dependencies
  echo Dependencies installing ...
  apt-get install software-properties-common -y
  echo|apt-add-repository ppa:bitcoin/bitcoin
  apt-get update && apt-­get upgrade ­y
  apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev libcurl4-nss-dev bsdmainutils libboost-all-dev libdb4.8-dev libdb4.8++-dev libminiupnpc-dev libzmq3-dev protobuf-compiler libqrencode-dev libsqlite3-dev libprotobuf-dev libasound2-dev uuid-dev libuuid1 libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools liblog4cplus-dev libavdevice-dev libsndio-dev libjack-dev libavformat-dev libopencore-amrnb-dev libopencore-amrwb-dev libswscale-dev libopus-dev libavcodec-dev libspeexdsp-dev libspeex-dev libsdl-dev libsdl2-dev libgsm1-dev -y
  git clone https://github.com/Kore-Core/kore.git 
  cd kore
  echo Dependencies Finished installing. 
  echo Configuring Kore 
  echo clearing cache 
  sync; echo 3 > /proc/sys/vm/drop_caches 
  echo cache cleared 
  ./autogen.sh 
  ./configure 
  make install 
  echo Kore Configured 
  ************************************************************************ 
  If you have a VPS with more than 4GB of RAM use this code 
  ************************************************************************ 
  #Install Dependencies 
  echo Dependencies installing ... 
  apt-get install software-properties-common -y 
  echo|apt-add-repository ppa:bitcoin/bitcoin 
  apt-get update && apt-­get upgrade ­y 
  apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev libcurl4-nss-dev bsdmainutils libboost-all-dev libdb4.8-dev libdb4.8++-dev libminiupnpc-dev libzmq3-dev protobuf-compiler libqrencode-dev libsqlite3-dev libprotobuf-dev libasound2-dev uuid-dev libuuid1 libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools liblog4cplus-dev libavdevice-dev libsndio-dev libjack-dev libavformat-dev libopencore-amrnb-dev libopencore-amrwb-dev libswscale-dev libopus-dev libavcodec-dev libspeexdsp-dev libspeex-dev libsdl-dev libsdl2-dev libgsm1-dev -y 
  git clone https://github.com/Kore-Core/kore.git 
  cd kore
  echo Dependencies Finished installing. 
  echo Configuring Kore 
  echo clearing cache 
  sync; echo 3 > /proc/sys/vm/drop_caches 
  echo cache cleared 
  ./autogen.sh 
  ./configure 
  make install 
  echo Kore Configured 
  ************************************************************************* 
Step: 4a	Start the kore daemon and save your masternode key and your onion address

At the root command line run these:
kored --daemon
kore-cli masternode genkey (save your masternode key that generates here)
kore-cli stop
cat ~/.kore/onion/hostname (save your onion address that displays here)


Now edit the conf file:

At the command line enter this:
nano ~/.kore/kore.conf 

In the screen that pops up copy and paste the test below between the ***s

*************************************************************
server=1

daemon=1 rpcuser=huckuserone
rpcpassword=anythingyouwant
rpcport=9932
rpcallowip=127.0.0.1
listen=1
staking=0
masternode=1
masternodeprivkey=***put your MN private key here***
masternodeaddr=***put your onion address here***
txindex=1
addrindex=1
addnode=uei3hz5jstv7tfo6.onion
addnode=fzmjhi7xbapufts6.onion
addnode=p6sfbaw762mcqyxg.onion
addnode=b5gacg24h6licg5m.onion
addnode=skrivht2uj3yjluv.onion
addnode=yylyof6avhsmb327.onion
************************************************************

To exit back enter these commands:

- press Ctl o -- not zero the letter o
- press Enter
- press Ctl x

Now at the root command line:

- kored -reindex

wait a few moments and run

- kore-cli getinfo

Make sure you have connections and blocks are updating...
Step 5	Your VPS is now ready... we are moving on to the local wallet on your local machine. This next work is NOT on your VPS

Create a new incoming address to receive coins
Step 6	Now send 500 kore coins (+ network fee) coins to yourself by sending them to the address you just created in step 5
Step 7	Go to the transactions tab and select your transaction you just created in step 6. Right click and select copy raw transaction info.
Step 8	Go to the transactions tab and select your transaction you just created in step 6. Right click and select copy raw transaction info.
Step 9	Go to Help >> Debug Window .... then select the Console tab

In the console tab, enter...

decoderawtransaction ***paste your transaction id here *** without the ***s
Press enter

Find your vout transaction of 500 coins and then look for the value of "n" right next to it. It should be a number between 0 and 9

Remember the value of n
Step 10	Now edit your masternode.conf located inside your local /.kore/ folder

add the following line at the bottom of the doc:

***masternodename*** ***%hostname%:10743*** ***masternode key*** ***500 kore tx id without the -000*** ***"n" value***

Do not keep the ***s, they are only to express entity separation in the example...

save and exit

This is an example below:

JediMasternode dfaslkuaha.onion:10743 dasadsfoifuhewq89kjdfspo adfsp98o32hodfsakjudfasuidfs 0
Step 11	Restart your Kore wallet

Go to settings >> options >> select the wallet tab >> Check the Show Masternodes Tab >> Click Ok 

On the left of the wallet, select the Masternodes tab... you will see your Masternode in the list under My Masternodes tab

Select your masternode you just created and click on "Start alias" follow the prompts... Congratulations, you now have a Masternode...
Step 12	Let's go check to make sure your Masternode is running as expected... Log back into your VPS...

Enter this command:

kore-cli masternode status

You should see this:

"status": "Masternode successfully started"

If it is not running, you will see this:

"status": "Node just started, not yet activated... If you see this, then give it more time. My first masternode took about 16 hours to start...
Thank you...	The Kore community is the core of the Kore Projects... We cannot do any of this without you and we are grateful to have you amongst us as a community member...
