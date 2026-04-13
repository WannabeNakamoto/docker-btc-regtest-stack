# Introduction
I share my docker stack for developing Bitcoin stuff. This is a quick and dirty stack, things could be done in a better way, but this way is convienent for me. I hope it could be useful for other plebs. Coments and PRs are very welcome. Please don't use it on mainnet, there are better solutions for this. I create this stuff during the awesome [Bitshala's](https://www.bitshala.org/) cohort  [Learning Bitcoin from the Command Line](https://github.com/BlockchainCommons/Learning-Bitcoin-from-the-Command-Line). Please, checkout [Bitshala](https://www.bitshala.org/) site, this folks are making really great things for bitcoin plebs.


# Docker stack

These are the docker stack containers:
* bitcoind: oficial bitcoin core node
* fulcrum: a c++ electrum server implementation
* mempool.space (web, api, db)

# Explanation

The key component is the [my_entry_point.sh](my_entry_point.sh) script. This bash scripts start a bitcoind node, also creates some wallets, mine some blocks and finally creates some TX and sleeps for long time. No data is persistent, every time that you stop & start the docker stack a new shinny bitcoin devel environment is ready for build new crazy stuff.

# Usage

Clone this repo:
```
git clone https://github.com/lazysatoshi/docker-btc-regtest-stack
```

Start the docker stack:

```
cd docker-btc-regtest-stack
docker compose up
```

Wait some minutes, after downloading container images and bulding the stack. Then, you should connect to your [mempool.space](http://localhost:1080) bitcoin regtest explorer at localhost port 1080 and enjoy it!



Command executions outside of docker:
#  Usage:
#    docker compose up -d
#    docker compose -f bitcoin-env.yaml exec bitcoind bitcoin-cli -regtest -rpcuser=admin -rpcpassword=admin createwallet "dev"
#    docker compose -f bitcoin-env.yaml exec bitcoind bitcoin-cli -rpcwallet="dev" -regtest -rpcuser=admin -rpcpassword=admin getnewaddress
#    docker compose -f bitcoin-env.yaml exec bitcoind bitcoin-cli -regtest -rpcuser=admin -rpcpassword=admin generatetoaddress 101 <address>
# ------------- Check balance for specific address:
#    docker compose -f bitcoin-env.yaml exec bitcoind bitcoin-cli -regtest -rpcuser=admin -rpcpassword=admin scantxoutset start '["addr(<ADDRESS>)"]'
# If running on Windows machine, use \" \" because it has parsing issue: Error parsing JSON: [addr(<ADDR>)]
# docker compose -f bitcoin-env.yaml exec bitcoind bitcoin-cli -regtest -rpcuser=admin -rpcpassword=admin scantxoutset start '[\"addr(<ADDRESS>)\"]'

But there are helper scripts for powershell that can be used for command executions easily [Windows development infra.]




Commands examples:
.\mineblock.ps1 -Address bcrt1qure2064txdms6sdna3p60amq00knqqt6xwmpkx -Blocks 12 [mines 12 blocks to specified address]
.\generateaddress.ps1 -Wallet Miner [Generates new address for wallet called miner. default value is also miner because it is created while container starts.]