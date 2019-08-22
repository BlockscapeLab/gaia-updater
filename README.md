# ansible-gaia-upgrade

### upgrade with new genesisfile, steps that should be executed automatically 
```
cd
cd go/src/github.com/cosmos/gaia/
git fetch --tags
git checkout .
git checkout v1.0.0-rc3                       #variable?
git clean -fd
git clean -fx
sudo systemctl stop gaiad
ps -ax | grep gaia                            #check gaiad killed?
go version                                    #check minimal version
echo $GOPATH                                  #check envs
echo $GOBIN
make go-mod-cache                             #or set env to?: GO111MODULE=on
make install
gaiad version                                 #variable to check version?
cd
df -h                                         #check disk space
cp -r .gaiad/data/ .gaiad/data_backup         #backup blockchain data
gaiad unsafe-reset-all
df -h                                       #check disk space if old database is clean/removed
cd .gaiad/config/
vim config.toml                               #check configs peers, pri_ids
ls                                            #check dir
rm genesis.json
wget https://raw.githubusercontent.com/cosmos/testnets/master/gaia-13k/genesis.json #variable?
sha256sum genesis.json                        #variable?
sudo systemctl start gaiad                    #ensure set ulimit in systemd service file
```
