# Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.

First of all you have to start one masternode using <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-18.04-MN.sh">vida-18.04-MN.sh</a> OR <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-20.04-MN.sh">vida-20.04-MN.sh</a> script that is your MainNode.

# Guide of use VIDA MN for MainNode:

##### For Ubuntu 18.04
```
wget -q https://raw.githubusercontent.com/Vidachain/VIDA-MultiMN/main/vida-18.04-MN.sh
sudo chmod +x vida-18.04-MN.sh
./vida-18.04-MN.sh
```

##### For Ubuntu 20.04
```
wget -q https://raw.githubusercontent.com/Vidachain/VIDA-MultiMN/main/vida-20.04-MN.sh
sudo chmod +x vida-20.04-MN.sh
./vida-20.04-MN.sh
```

***

# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/Vidachain/VIDA-MultiMN/main/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/Vidachain/VIDA-MultiMN/main/profiles/vida.mn
multimn profadd vida.mn vida
```
Now the vida profile is saved and the downloaded file can be removed if you want: `rm -rf vida.dmn`

Stop the vida Service:
```
vida-cli stop
systemctl stop vida
```
Now create 3 extra instances with bootstrap (Ex. You want to make 3 Masternode):
```
multimn install vida --bootstrap
multimn install vida --bootstrap
multimn install vida --bootstrap
```
You can check every MN like this:
```
vida-cli-1 getinfo
vida-cli-2 getinfo
vida-cli-3 getinfo
vida-cli-all getinfo
```
There's also a `vida-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall vida 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall vida all`


You can get priv key of all MN with:

`multimn list vida --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN0 IP:20406 MN_PrivKey Tx_Hash Output_Index
MN01 IP:20406 MN_PrivKey Tx_Hash Output_Index
MN02 IP:20406 MN_PrivKey Tx_Hash Output_Index
MN03 IP:20406 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN0 is your main_node MN which you create with <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-18.04-MN.sh">vida-18.04-MN.sh</a> OR <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-20.04-MN.sh">vida-20.04-MN.sh</a> script.

MN01, MN02, MN03 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN0
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
```

Now StartMasternode in VPS with Service:

`systemctl start vida` (Start your MN which is create with main_node <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-18.04-MN.sh">vida-18.04-MN.sh</a> OR <a href="https://github.com/Vidachain/VIDA-MultiMN/blob/main/vida-20.04-MN.sh">vida-20.04-MN.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   vida-1.service
systemctl start   vida-2.service
systemctl start   vida-3.service
```

That's all now your MN start.
