![alt text](https://downloadwallet.infinitericks.com/images/logo.png)  
# InfiniteRicks

Proof Type: PoS (Proof-of-Stake)<br>
Coin name: InfiniteRicks<br>
Coin abbreviation: RICK<br>
Address letter:	1<br>
Min stake age: 12 Hours<br>
Block time: 2 min<br>
APR:  307% a year<br>
RPC port:	31648<br>
P2P port:	31647<br>
Supply: unlimited


Official Website <br>
https://infinitericks.com

Blockexplorer <br>
https://explorer.infinitericks.com

## How to compile and use the Linux Deamon
Tested and working on Ubtunu 14 - 16.04 and 18.04 Version.<br>
Versions 20.04 and later do not currently compile due to changes in OpenSSL 1.1
and the Boost C++ library in that version.

### Swapfile

You can check if your server has a swap file already with the ```swapon``` command.  If your system has less than 1.5GB of memory, you'll want at least a 2GB swap area.  Add a new swapfile with:
```
sudo fallocate -l 2G /swapfile
sudo chown root:root /swapfile
sudo chmod 0600 /swapfile
sudo bash -c "echo 'vm.swappiness = 10' >> /etc/sysctl.conf"
sudo mkswap /swapfile
sudo swapon /swapfile
```
If fallocate doesn’t work, you can instead use:
```
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1024288
```
Initialize the swapfile to mount automatically on boot:
```
sudo echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

### Install all required dependencies

```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get -y install nano ntp unzip git build-essential libssl-dev
sudo apt-get -y installlibdb-dev libdb++-dev libboost-all-dev libqrencode-dev aptitude
sudo aptitude -y install miniupnpc libminiupnpc-dev
```
ubuntu 18.04
```
sudo apt-get install libssl1.0-dev
sudo apt-get install libqt4-dev
```

If you get an error mentioning lock files, you probably have a desktop or background package update tool running that prevents other apt changes from happening.  You can use the ```lsof``` utility to figure out what program holds the lock and then pause it from running.

Pull the source code from github, or download it yourself:
```
git clone https://github.com/coinsdevcode/InfiniteRicks.git
```

### Compiling the software

Now you compile the included leveldb:
```
chmod +x InfiniteRicks
cd InfiniteRicks/src/leveldb
chmod +x build_detect_platform
make clean
make libleveldb.a libmemenv.a
```
Return to the source directory, and compile the daemon:
```
cd ..
make -f makefile.unix RELEASE=1
```
To compile qt (wallet with GUI) for Ubuntu 16.04 or 18.04 LTS use:
```
sudo apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools
sudo apt-get install libboost-system-dev
sudo apt-get install libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev
```
Return to the source directory, and compile the qt:
```
cd ..
qmake RELEASE=1
make STATIC=1
```
Strip the file to make it smaller, then relocate it:
```
strip InfiniteRicksd
sudo cp InfiniteRicksd /usr/bin
```
Now run the daemon:
```
InfiniteRicksd
```
It should return an error, telling you to set up config file in a directory. 

## Create a config file

Now we’ll set up the config file. Note that this is case sensitive.<br>
Linux
```
nano ~/.InfiniteRicks/InfiniteRicks.conf
```
Winodws
```
C:\Users\YourUserName\AppData\Roaming\InfiniteRicks
```
Add the following, save and exit:
```
stake=1
listen=1
daemon=1
server=1
rpcuser=(username)
rpcpassword=(strong password)
addnode=38.242.236.173
addnode=104.28.196.77
addnode=104.28.196.78
addnode=104.28.228.77
addnode=104.28.228.78
addnode=107.9.8.127
addnode=109.163.219.176
addnode=146.168.22.107
addnode=178.40.242.170
addnode=181.214.94.9
addnode=185.65.200.244
addnode=195.3.222.58
addnode=202.169.105.168
addnode=207.180.217.38
addnode=31.41.102.56
addnode=45.225.237.172
addnode=47.97.162.229
addnode=5.189.155.73
addnode=62.163.210.67
addnode=62.214.252.131
addnode=62.214.252.20
addnode=75.119.137.26
addnode=77.38.144.211
addnode=82.64.109.25
addnode=85.209.89.98
addnode=87.76.34.19
addnode=87.76.35.164
addnode=88.116.84.178
addnode=89.27.88.218
addnode=91.239.42.41
addnode=93.176.148.124
addnode=94.140.233.79
addnode=95.24.150.255
addnode=95.24.153.161
```
Run compoundd once more and if you did everything correctly, your daemon is now online! 
## Command summary
Type:
```
help
```
for a full list of commands available.

