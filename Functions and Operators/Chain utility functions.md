Dune SQL offers a series of functions designed to ease some common tasks when working with blockchain data.

These functions are helpful to generate links to the explorer of a chain, to specific addresses, or to specific transactions. Most of the time you’ll want to use `get_href()` in combination with one of the other functions to generate a clickable link to a specific address or transaction.

```sql
Select
    get_href(get_chain_explorer_address('ethereum', to), cast(to as varchar))
FROM ethereum.transactions
limit 100
```

This sql code will generate a clickable link pointing to the explorer of the Ethereum chain for each address in the `to` column. The displayed link will be the address itself.

You can find all the functions in action on this dashboard: [Chain Utility Functions](https://dune.com/dune/chain-utility-functions)

#### get\_href()

**`get_href(varchar, varchar)`** → varchar

This function converts a link and associated text into a clickable hyperlink. The first argument is the link, and the second argument is the text to be displayed.

```sql
SELECT 
    get_href('https://dune.com', 'Dune')
```

#### get\_chain\_explorer\_address()

**`get_chain_explorer_address(varchar, varchar)`** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given address (also provided as a varchar).

```sql
SELECT 
    get_chain_explorer_address('ethereum', cast(to as varchar)) 
FROM ethereum.transactions 
limit 100
```

#### get\_chain\_explorer\_address()

**`get_chain_explorer_address(varchar, varbinary)`** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given address (provided as a varbinary).

```sql
SELECT 
    get_chain_explorer_address('ethereum', to) 
FROM ethereum.transactions 
limit 100
```

#### get\_chain\_explorer\_tx\_hash()

**`get_chain_explorer_tx_hash(varchar, varchar)`** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given transaction hash (also provided as a varchar).

```sql
SELECT 
    get_chain_explorer_tx_hash('ethereum', cast(hash as varchar)) 
FROM ethereum.transactions 
limit 100
```

#### get\_chain\_explorer\_tx\_hash()

**`get_chain_explorer_tx_hash(varchar, varbinary)`** → varchar

This function generates a URL for the explorer of a specified chain (provided as a varchar) for a given transaction hash (provided as a varbinary).

```sql
SELECT 
    get_chain_explorer_tx_hash('ethereum', hash) 
FROM ethereum.transactions 
limit 100
```

#### get\_chain\_explorer()

**`get_chain_explorer(varchar)`** → varchar

This function returns the URL of the explorer for a specified chain (provided as a varchar).

```sql
SELECT 
    get_chain_explorer('ethereum')
```

#### get\_balancer\_link()

**`get_balancer_link(varchar, varchar)`** → varchar

This function returns a link to access a specific pool on the Balancer app. The first argument is the chain, and the second argument is the pool Id (provided as varchar).

```sql
SELECT 
    get_balancer_link(blockchain, cast(pool_id as varchar))
FROM balancer.trades
limit 100
```

#### get\_balancer\_link()

**`get_balancer_link(varchar, varbinary)`** → varchar

This function returns a link to access a specific pool on the Balancer app. The first argument is the chain, and the second argument is the pool Id (provided as varbinary).

```sql
SELECT 
    get_balancer_link(blockchain, pool_id)
FROM balancer.trades
limit 100
```

#### all\_evm\_chains()

**`all_evm_chains()`** → array(varchar)

This function returns an array listing all the EVM chains available on Dune.

#### all\_op\_chains()

**`all_op_chains()`** → array(varchar)

This function returns an array listing all the Optimism chains available on Dune.