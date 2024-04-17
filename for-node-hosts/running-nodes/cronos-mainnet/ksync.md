# Syncing a Node Using KYVE's KSYNC

This sections covers how to perform a genesis-sync up to live height and how to state-sync to historical heights for Cronos Mainnet with KSYNC. In summary KSYNC is a tool developed by [KYVE](https://www.kyve.network/) which is capable of syncing blocks and state-sync snapshots from the decentralized KYVE data lake directly into Cosmos blockchain nodes. For Cronos, KYVE has validated all historical blocks and state-sync snapshots (in a 10,000 interval) in a decentralized way and permanently archived them to [Arweave](https://arweave.org/), a decentralized storage solution. KSYNC can then pull down this verified data and apply them against the Cronos app, you can find full documentation on the tool [here](https://docs.kyve.network/validators/ksync).

#### Installation

You can install KSYNC with the following command, ensure that you have go1.21 installed:

```bash
go install github.com/KYVENetwork/ksync/cmd/ksync@latest
```

To verify the installation simply run `ksync version`. To build from source visit the repository on [GitHub](https://github.com/KYVENetwork/ksync).

#### Sync Cronos from genesis

To sync Cronos from genesis up to live height install the binary used for genesis from [here](https://github.com/crypto-org-chain/cronos/releases/tag/v0.6.11).

After the installation, init the config:

```bash
./cronosd init <your-moniker> --chain-id cronosmainnet_25-1
```

Download the genesis:

```bash
wget -O ~/.cronos/config/genesis.json https://raw.githubusercontent.com/crypto-org-chain/cronos-mainnet/master/cronosmainnet_25-1/genesis.json
```

Now that Cronos is properly set up you can start the genesis sync:

```bash
ksync block-sync --binary="/path/to/cronosd" --source="cronos"
```

This will run until live height has been reached, you can check the latest height which KYVE has validated and archived [here](https://app.kyve.network/#/pools/5). Note that you can also configure Cosmovisor to already contain all upgrade binaries, then you can
also run with Cosmosvisor so you do not have to manually switch the version everytime Cronos reaches an upgrade. It is recommended to pair this with
a systemd service file, a template can be found below:

```
[Unit]
Description=KSYNC deamon supervising the ksync sync process
After=network-online.target

[Service]
User=$USER
WorkingDirectory=$HOME
ExecStart=$HOME/ksync block-sync --binary="/path/to/cosmovisor" --source=cronos -y
Restart=always
RestartSec=10s
LimitNOFILE=infinity
Environment="DAEMON_NAME=cronosd"
Environment="DAEMON_HOME=$HOME/.cronos"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=false"
Environment="DAEMON_LOG_BUFFER_SIZE=512"
Environment="UNSAFE_SKIP_BACKUP=true"

[Install]
WantedBy=multi-user.target
```

Remember to replace \$USER with your actual username.

#### Apply historical state-sync snapshots

The "normal" state-sync only supports syncing to live height, but because KYVE has validated and archived all state-sync snapshots from genesis with a
10,000 block interval historical state-sync are possible with KSYNC. Note that the archival process is still ongoing and live height has not been reached yet, you can check the current progress [here](https://app.kyve.network/#/pools/6).

Install cronos like in the genesis sync part before, but depending on the target height you want to sync to you have to use the appropiate binary version. You can find all upgrades with the respected upgrade heights [here](/for-node-hosts/running-nodes/cronos-mainnet/README.md#step-0--notes-on-huygen-network-upgrade).

To perform the state-sync execute the following command:

```bash
ksync state-sync --binary="/path/to/cronosd" --source="cronos" --target-height=$HEIGHT
```

If there is no state-sync snapshot available for your requested \$HEIGHT KSYNC will automatically propose the nearest snapshot before that height for you.

#### Sync to any historical height with height-sync

The features of historical state- and block-sync can now be combined to sync to any historical block height by using the combination of those. With that KSYNC will state-sync to the nearest snapshot before your specified target height and block-sync the remaining blocks. With that the process of checking out the state at a certain height can be greatly improved because now you don't have to sync all the way from genesis if you want to inspect the state of a historical block height.

To perform the height-sync execute the following command:

```bash
ksync height-sync --binary="/path/to/cronosd" --source="cronos" --target-height=$HEIGHT
```
