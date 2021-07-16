## Example queries for Kusama on the following use cases. 


###Get historic transfers for a specific account

```graphql
query{
  transfers(filter:{
    or: [
      {fromId: {equalTo : "HRuaGanNmkmeQgZPWPXmkZJb944raNS5ni2vhKzhz75zVYP"}},
      {toId:{equalTo:"HRuaGanNmkmeQgZPWPXmkZJb944raNS5ni2vhKzhz75zVYP"}}
    ]
  }){
    totalCount #total transfers
    nodes{
      asset{  # type of asset
        symbol
        decimal
      }
      amount, #amout
      fromId, 
      toId,
      event{ #futher information
        id, 
        extrinsic{
          id
        }
        timestamp #when
      }
    }
  }
}
```

### Get details about accounts (including current balance)

```graphql

query{
  accounts(first: 100){ # for pagination
    nodes{
      id,
      pubKey, 
      identity, #identity info in json 
      nextNonce, 
      balanceHistory(first:1, filter:{  #get the latest balance
        assetId : {
          equalTo: "KSM_ASSET_ID"  # with particular asset
        }
      }){
        nodes{
          asset{
            symbol,
            decimal
          }
          freeAmount,
          reservedAmount,
          locked
        }
      }
    }
  }
}

```

### Get data for a graph off account balance changes over time


```graphql

query{
  account(id:"HRuaGanNmkmeQgZPWPXmkZJb944raNS5ni2vhKzhz75zVYP"){  #for particular account
      balanceHistory(filter:{
        assetId : {
          equalTo: "KSM_ASSET_ID"  #for kusama asset
        }
      }){
        nodes{
          asset{
            symbol,
            decimal
          }
          freeAmount,
          reservedAmount,
          locked
        }
      }
  }
}


```

Get historic slashes for a specific account
Get historic reward data for a specific account
Get payable staking rewards for specific Nominators
