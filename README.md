# Manual Installation

**Recommended Hardware: 4 Cores, 8GB RAM, 200GB of storage (NVME)**

**install dependencies, if needed**
```
sudo apt update && sudo apt upgrade -y
sudo apt install curl git wget htop tmux build-essential jq make lz4 gcc unzip -y
```
**install go, if needed**
```
cd $HOME
VER="1.19.3"
wget "https://golang.org/dl/go$VER.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$VER.linux-amd64.tar.gz"
rm "go$VER.linux-amd64.tar.gz"
[ ! -f ~/.bash_profile ] && touch ~/.bash_profile
echo "export PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.bash_profile
source $HOME/.bash_profile
[ ! -d ~/go/bin ] && mkdir -p ~/go/bin
```
**set vars**
```
echo "export WALLET="wallet"" >> $HOME/.bash_profile
echo "export MONIKER="test"" >> $HOME/.bash_profile
echo "export NOIS_CHAIN_ID="nois-1"" >> $HOME/.bash_profile
echo "export NOIS_PORT="36"" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

**download binary**
```
cd $HOME
rm -rf $HOME/noisd
git clone https://github.com/noislabs/noisd
cd noisd
git checkout v1.0.5
make install
```

**config and init app**
```
noisd config node tcp://localhost:${NOIS_PORT}657
noisd config keyring-backend os
noisd config chain-id nois-1
noisd init "test" --chain-id nois-1
```

**download genesis and addrbook**
```
wget -O $HOME/.noisd/config/genesis.json https://server-3.itrocket.net/mainnet/nois/genesis.json
wget -O $HOME/.noisd/config/addrbook.json  https://server-3.itrocket.net/mainnet/nois/addrbook.json
```

**set seeds and peers**
```
SEEDS="c8db99691545545402a1c45fa897f3cb1a05aea6@nois-mainnet-seed.itrocket.net:36656"
PEERS="22ec344512fc679e16eb358284e0d1eaa4291194@nois-mainnet-peer.itrocket.net:36656,8c0d1012b72cad9e31a80d84bd5c5e5a8c842df7@79.137.70.143:26636,431da00c2d201821ab508f69b193cce6da420119@65.108.134.47:17356,922d90c7ef1840c984fcfa387a491c8d3c4481dc@65.108.141.109:55656,2e2a668f34996d8284b7e8553a8a8698b6e0cb35@65.109.53.24:36656,e4a5fa4e5a02fa3f2fbe2cdd38f657c0270fc927@176.9.157.142:17356,00852ba0bfdf20aac74369b1a5c43e50668c9738@135.181.128.114:17356,a792606ff664a478abc2ed046b3f762a42263c5b@65.109.16.125:27656,3faff1e60b60a5ef64549c0adc0a6b1a6fc48041@149.50.102.46:17356,3dd1bb1423a3dde567d1645b999af4592d53d2d0@65.109.62.179:36656,1ff95efbb1fc681ab3302e8da70370c6e4f1462f@[2a01:4f9:6b:2e5b::17]:26656,b1e7765bf3995fba9ce10a843a735941a03e2356@38.146.3.230:17356,379c0e32463be66e5cf8d13d62eb87ddb1a702c2@142.132.152.46:47656,66834b4290c33c3d24b7f63de77feb23d056daf4@142.132.156.99:40136,0cf59ab91e4a96d6e5427d903644edd18d9421d1@142.132.248.138:26786,8c13a85248a7dcec574f4208c7ecb9b7b9481b84@51.81.49.59:17356,b8711d88e017e33753a59abd9e202744ddf3f9a5@148.251.8.186:33656,1bcddb31796d893af9aef1cf3a5c8d19cb8cca8c@162.55.245.149:2240,e409b5ae06ff0917de94f1fb636fd833ddaf9810@51.89.98.102:55726,e62849ea53f3f0c926f0ffe8bd6a2645672d875a@213.239.199.149:26656,239b5b0c66b756f8cf1dcfb92c78ef04d8bde4c8@46.4.91.49:33656,145fb4c869394d846e91cb84c6d9efe1515c0846@144.76.97.251:33656,488a9213c915556a8e0327418cd81fd69362ccb1@65.109.115.226:17356,e541e3a182bcb8d8da8cea17716d12f0b730a0a6@144.76.40.53:17356,f92b0009f979b7c04f1b71b7eab0ffdff7a321ff@51.91.105.152:17356,6ef1914f30ac7becdf2c718b65c61cd618b7021a@57.128.144.242:26656,49a52421e508e87c37b1efee2f909ce7ad176975@[2001:bc8:702:16d0::3]:26656,0371e0701ba6aaf231d147d49cdd67735d64495a@65.109.104.118:60656,68188114b583f054fd530cc9a275820e3d1c0f86@51.159.2.19:22273,f03752476d5f328b26960e20b6101a68c3c9cd6d@65.109.112.170:27656,e2bec7bc206f0491f6652e9d55d1943f6b969d70@213.190.31.82:17356,e84cbe410271d84b2968c46881522bd3e9726898@144.76.30.36:15663,9f81dbe93027b0d802319349abcc2275eef4dc40@162.55.34.91:26656,91952caf57ac1c26738f069d2e79ca9b539f641d@135.181.198.17:26656,7bd2beda636ef3077d349a0bacf6fca87c8d9b65@144.76.63.67:26806,cca26eaecd8d5250794db3b1378714130b03513c@89.233.107.72:17356,fb6eef6435d3fa3cfca9ee00c06d9cf7a18767d8@65.108.120.251:26656,171b9d4700909ec297641aa8a69d45b4149f0d1d@141.94.193.28:55726,ee7ee30cf738d64498e2448c0c27e915bc3cab0b@5.181.190.114:17656,09992768a81082f0117b771bb4fcba0cd331efa2@65.109.93.44:17356,c49c510b0e1323240f9b302c6d85fe6df186bd45@5.9.81.187:37656,8f36fd1d1b8718e54053b64717ddbbbe2a4e6d3d@154.53.44.239:26656,3a516737162cd213beed4a1ebfee7e3e29e0c3e2@94.130.138.48:30656"
sed -i -e "/^\[p2p\]/,/^\[/{s/^[[:space:]]*seeds *=.*/seeds = \"$SEEDS\"/}" \
       -e "/^\[p2p\]/,/^\[/{s/^[[:space:]]*persistent_peers *=.*/persistent_peers = \"$PEERS\"/}" $HOME/.noisd/config/config.toml
```

**set custom ports in app.toml**
```
sed -i.bak -e "s%:1317%:${NOIS_PORT}317%g;
s%:8080%:${NOIS_PORT}080%g;
s%:9090%:${NOIS_PORT}090%g;
s%:9091%:${NOIS_PORT}091%g;
s%:8545%:${NOIS_PORT}545%g;
s%:8546%:${NOIS_PORT}546%g;
s%:6065%:${NOIS_PORT}065%g" $HOME/.noisd/config/app.toml
```

**set custom ports in config.toml file**
```
sed -i.bak -e "s%:26658%:${NOIS_PORT}658%g;
s%:26657%:${NOIS_PORT}657%g;
s%:6060%:${NOIS_PORT}060%g;
s%:26656%:${NOIS_PORT}656%g;
s%^external_address = \"\"%external_address = \"$(wget -qO- eth0.me):${NOIS_PORT}656\"%;
s%:26660%:${NOIS_PORT}660%g" $HOME/.noisd/config/config.toml
```

**config pruning**
```
sed -i -e "s/^pruning *=.*/pruning = \"custom\"/" $HOME/.noisd/config/app.toml
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"100\"/" $HOME/.noisd/config/app.toml
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"50\"/" $HOME/.noisd/config/app.toml
```

**set minimum gas price, enable prometheus and disable indexing**
```
sed -i 's|minimum-gas-prices =.*|minimum-gas-prices = "0.0unois"|g' $HOME/.noisd/config/app.toml
sed -i -e "s/prometheus = false/prometheus = true/" $HOME/.noisd/config/config.toml
sed -i -e "s/^indexer *=.*/indexer = \"null\"/" $HOME/.noisd/config/config.toml
```

**create service file**
```
sudo tee /etc/systemd/system/noisd.service > /dev/null <<EOF
[Unit]
Description=Nois node
After=network-online.target
[Service]
User=$USER
WorkingDirectory=$HOME/.noisd
ExecStart=$(which noisd) start --home $HOME/.noisd
Restart=on-failure
RestartSec=5
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

**reset and download snapshot**
```
noisd tendermint unsafe-reset-all --home $HOME/.noisd
if curl -s --head curl https://server-3.itrocket.net/mainnet/nois/nois_2024-08-19_18581960_snap.tar.lz4 | head -n 1 | grep "200" > /dev/null; then
  curl https://server-3.itrocket.net/mainnet/nois/nois_2024-08-19_18581960_snap.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.noisd
    else
  echo "no snapshot founded"
fi
```

**enable and start service**
```
sudo systemctl daemon-reload
sudo systemctl enable noisd
sudo systemctl restart noisd && sudo journalctl -u noisd -f
Automatic Installation
pruning: custom: 100/0/10 | indexer: null

source <(curl -s https://itrocket.net/api/mainnet/nois/autoinstall/)
```
**Create wallet**
```
noisd keys add $WALLET
```

# to restore exexuting wallet, use the following command
noisd keys add $WALLET --recover

# save wallet and validator address
WALLET_ADDRESS=$(noisd keys show $WALLET -a)
VALOPER_ADDRESS=$(noisd keys show $WALLET --bech val -a)
echo "export WALLET_ADDRESS="$WALLET_ADDRESS >> $HOME/.bash_profile
echo "export VALOPER_ADDRESS="$VALOPER_ADDRESS >> $HOME/.bash_profile
source $HOME/.bash_profile

# check sync status, once your node is fully synced, the output from above will print "false"
noisd status 2>&1 | jq 

# before creating a validator, you need to fund your wallet and check balance
noisd query bank balances $WALLET_ADDRESS 
Create validator
Moniker
Identity
Details
I love blockchain ❤️
Amount, unois
1000000
Commission rate
0.1
Commission max rate
0.2
Commission max change rate
0.01
Website
noisd tx staking create-validator \
--amount 1000000unois \
--from $WALLET \
--commission-rate 0.1 \
--commission-max-rate 0.2 \
--commission-max-change-rate 0.01 \
--min-self-delegation 1 \
--pubkey $(noisd tendermint show-validator) \
--moniker "test" \
--identity "" \
--website "" \
--details "I love blockchain ❤️" \
--chain-id nois-1 \
--gas auto --gas-adjustment 1.5 \
-y
Monitoring
If you want to have set up a monitoring and alert system use our cosmos nodes monitoring guide with tenderduty

Security
To protect you keys please don`t share your privkey, mnemonic and follow basic security rules

Set up ssh keys for authentication
You can use this guide to configure ssh authentication and disable password authentication on your server

Firewall security
Set the default to allow outgoing connections, deny all incoming, allow ssh and node p2p port

sudo ufw default allow outgoing 
sudo ufw default deny incoming 
sudo ufw allow ssh/tcp 
sudo ufw allow ${NOIS_PORT}656/tcp
sudo ufw enable
Delete node
sudo systemctl stop noisd
sudo systemctl disable noisd
sudo rm -rf /etc/systemd/system/noisd.service
sudo rm $(which noisd)
sudo rm -rf $HOME/.noisd
sed -i "/NOIS_/d" $HOME/.bash_profile
