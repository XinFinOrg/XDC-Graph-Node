# Graph node for xdc blockchain

## 1. deploy from docker

### 1.1 testnet


```shell
git clone https://github.com/XinFinOrg/XDC-Graph-Node.git
cd XDC-Graph-Node
git checkout xdc-release-0.32.0
cd docker
docker compose -f docker-compose-apothem.yml up
```

### 1.2 mainnet

```shell
git clone https://github.com/XinFinOrg/XDC-Graph-Node.git
cd XDC-Graph-Node
git checkout xdc-release-0.32.0
cd docker
docker compose -f docker-compose-xinfin.yml up
```

## 2) deploy from srouce

[build from srouce step by step](./docs/deploy-from-source.md)

Notice: please use Ubuntu 22.04, or upgrade protobuf-compiler to v3.12.4.

## 3) Query

Subgraph example: https://github.com/gzliudan/bad-token-subgraph  
Query URL: http://\<IP\>:8000/subgraphs/name/gzliudan/bad-token-subgraph-apothem  
Query command:

```graphql
{
  erc20Contracts(first: 5) {
    id
    name
    symbol
    decimals
    totalSupply {
      value
      valueExact
    }
  }
  blackLists(first: 5) {
    id
    members {
      account {
        id
      }
    }
  }
  accounts(first: 5) {
    id
    isErc20
    blackLists {
      id
    }
    Erc20balances {
      id
      value
      valueExact
    }
  }
}
```

This subgraph example is deployed on subgraph hosted service: https://thegraph.com/hosted-service/subgraph/gzliudan/bad-token-mumbai also.
