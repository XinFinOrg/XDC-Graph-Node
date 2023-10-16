# About the graph-node for xdc blockchain

## Use the offical graph-node

### 1. Setup

```bash
git clone https://github.com/graphprotocol/graph-node
cd graph-node/docker
cp docker-compose.yml docker-compose-apothem.yml
cp docker-compose.yml docker-compose-xinfin.yml
```

### 2. Modify configuration

Replace the below lines

```text
      ethereum: 'mainnet:http://host.docker.internal:8545'
      GRAPH_LOG: info
```

in the file:

#### 2.1 docker-compose-apothem.yml

```text
      ethereum: "apothem:traces,archive,no_eip1898:https://earpc.apothem.network"
      ETHEREUM_REORG_THRESHOLD: 1
      GRAPH_ETHEREUM_FETCH_TXN_RECEIPTS_IN_BATCHES: true
      GRAPH_LOG: info
      GRAPH_LOG_TIME_FORMAT: "%Y-%m-%d %H:%M:%S"
```

#### 2.2 docker-compose-xinfin.yml

```text
      ethereum: "xinfin:traces,archive,no_eip1898:https://earpc.xinfin.network"
      ETHEREUM_REORG_THRESHOLD: 1
      GRAPH_ETHEREUM_FETCH_TXN_RECEIPTS_IN_BATCHES: true
      GRAPH_LOG: info
      GRAPH_LOG_TIME_FORMAT: "%Y-%m-%d %H:%M:%S"
```

### 3. Startup

```bash
# testnet
docker compose -f docker-compose-apothem.yml up

# mainnet:
docker compose -f docker-compose-xinfin.yml up
```

### 4. Test

**Notice: the xdc blockchain is not 100% fully compatible with the offical graph-node at this time.**

But my demo project https://github.com/gzliudan/erc20-subgraph can be tested with the offical graph-node on testnet now.

## Use the graph-node from xdc

The graph-node from xdc is ready for use now.

### 1. The features

- Support xdc-prefix and 0x-prefix
- Bypass the `eth_getLogs` bug of xdc blockchain
- Add flag `no_eip1898` for xdc chain
- Provide new docker image

### 2. Deploy

#### 2.1 Deploy from docker

```shell
git clone https://github.com/XinFinOrg/XDC-Graph-Node.git
cd XDC-Graph-Node
git checkout xdc-release-0.32.0
cd docker

# testnet
docker compose -f docker-compose-apothem.yml up

# mainnet
docker compose -f docker-compose-xinfin.yml up
```

#### 2.2 deploy from srouce

Here is a guide: [build from srouce step by step](./docs/deploy-from-source.md)

**Notice: please use Ubuntu 22.04, or upgrade protobuf-compiler to v3.12.4.**

### 3. Test

I wrote a subgraph project for test on testnet and mainnet: https://github.com/gzliudan/erc20-subgraph
