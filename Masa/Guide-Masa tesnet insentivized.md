Official documentation:
(https://github.com/masa-finance/masa-node-v1.0)



Minimal hardware requirements

CPU: 1 core
Memory: 2 GB RAM
Disk: 20 GB


Option 1 (automatic)

You can setup your Masanode in few minutes by using automated script below. It will prompt you to input your node name!







```
wget -O masa.sh https://raw.githubusercontent.com/kj89/testnet_manuals/main/masa/masa.sh && chmod +x masa.sh && ./masa.sh
``` 







Option 2 (manual)


[You can follow (manual guide) if you better prefer setting up node manually](Link)
Usefull commands

Check masa node logs
*You have to see blocks comming*



```
journalctl -u masad -f | grep "new block"
``` 









Get masa node key
!Please make sure you backup your node key somewhere safe. Its the only way to restore your node!



```
cat $HOME/masa-node-v1.0/data/geth/nodekey
``` 




Get masa enode id




```
geth attach ipc:$HOME/masa-node-v1.0/data/geth.ipc --exec web3.admin.nodeInfo.enode | sed 's/^.//;s/.$//'
``` 




Restart service





```
systemctl restart masad.service
``` 



Check eth node status
To check eth node synchronization status first of all you have to open geth




```
geth attach ipc:$HOME/masa-node-v1.0/data/geth.ipc
``` 


 


After that you can use commands below inside geth (eth.syncing should = false and net.peerCount have to be > than 0)


> node data directory with configs and keys
admin.datadir
check if node is connected
net.listening
show synchronization status
eth.syncing
node status (difficulty should be equal to current block height)
admin.nodeInfo
show synchronization percentage
eth.syncing.currentBlock * 100 / eth.syncing.highestBlock
list of all connected peers (short list)
admin.peers.forEach(function(value){console.log(value.network.remoteAddress+"\t"+value.name)})
list of all connected peers (long list)
admin.peers
show connected peer count
net.peerCount


*Press CTRL+D to exit*

Restore node key

To restore masa node key just insert it into $HOME/masa-node-v1.0/data/geth/nodekey and restart service afterwards
Replace <YOUR_NODE_KEY> with your node key and run command below





```
echo <YOUR_NODE_KEY> > $HOME/masa-node-v1.0/data/geth/nodekey
systemctl restart masad.service
``` 
