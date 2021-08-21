# Install

```shell
git clone https://github.com/Flora-Network/fd-cli.git
```
```shell
cd fd-cli
```
```shell
python3 -m venv venv
```
```shell
source venv/bin/activate
```
```shell
pip install -e . --extra-index-url https://pypi.chia.net/simple/
```


# NFT 7/8 reward recovery

```shell

# Set env var to blockchain path.
export FD_CLI_BC_DB_PATH=$HOME/.olive/mainnet/db/blockchain_v1_mainnet.sqlite

# Set env var to wallet path.
# This must be the wallet that is associated with mnemonic from which NFT plot was created. (Usually your hot wallet)
# Replace <fingerprint> with your wallet fingerprint found at below path or by using "chia wallet show"
export FD_CLI_WT_DB_PATH=$HOME/.olive/mainnet/wallet/db/blockchain_wallet_v1_mainnet_<fingerprint>.sqlite

# Set env var to launcher id of NFT plot. Replace the below ID with output of "Launcher ID:" 
# Launcher ID: can be obtained using "chia plotnft show"
# Execute above command in Chia, as those values are the original NFT contract details, which do not exist in the forks
export LAUNCHER_HASH=8084f1233bce0d15da8558bf122e94a0315962ec46fbdfa36ef767d95dd062da

# Set env var to pool_contract_address. 
# Pool contract address: can be obtained using "chia plotnft show"
# Execute above command in Chia, as those values are the original NFT contract details, which do not exist in the forks
export POOL_CONTRACT_ADDRESS=xch169dp3cgcr6mhcqr8m4fpcpy5qqhh3pycf4lp66cladtmv6xxgmzq2ah9y8

fd-cli nft-recover \
  -l "$LAUNCHER_HASH" \
  -p "$POOL_CONTRACT_ADDRESS" \
  -nh 127.0.0.1 \
  -np 7559 \
  -ct $HOME/.olive/mainnet/config/ssl/full_node/private_full_node.crt \
  -ck $HOME/.olive/mainnet/config/ssl/full_node/private_full_node.key
  
# All coins that were mined +7 days ago WITH NFT PLOT should be spendable soon via wallet.
```
