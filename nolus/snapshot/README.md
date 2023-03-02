# This is a guide for running nodes with the snapshot method, the goal is to synchronize more quickly to reach the latest block.

# First you have to stop the node
```
sudo systemctl stop nolusd
```

# Backup the state file and reset data folder
```
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
```

# Download the latest snapshot, extract the file then rename the backed up state file
```
curl -L http://nolus.jembutkucing.xyz/jembutkucing_snapshot.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```

Download new addressbook
```
wget -O $HOME/.nolus/config/addrbook.json "http://nolus.jembutkucing.xyz/addrbook.json"
```

# Restart the service and check the logs
```
sudo systemctl start nolusd && sudo journalctl -u nolusd -f
```





