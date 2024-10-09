Tron blockchain adopted a custom type of addresses. It is similar to [Base58](https://docs.dune.com/query-engine/Functions-and-operators/base58) encoding format, with some modifications.

Under basic tron address encoding format an address can be encoded as:

```
base58encode ( concat ( <constant-prefix>, <address>, <checksum> ) )
```

#### from\_tron\_address()

**`from_tron_address(varchar)`** → `varbinary`

Converts a Tron address string to the corresponding `VARBINARY` hex address.

```sql
SELECT 
    from_tron_address('THHRK1bA7YRPZBcLnTP1SZy9ipUpsRwpo6')
-- results in VARBINARY 0x503aa4ad108bd3a89ba0310e23b49fb654cd6986
```

#### to\_tron\_address()

**`to_tron_address(varbinary)`** → `varchar`

Encodes a `VARBINARY` hex address to the corresponding Tron address.

```sql
SELECT 
    to_tron_address(0x503aa4ad108bd3a89ba0310e23b49fb654cd6986)
-- results 'THHRK1bA7YRPZBcLnTP1SZy9ipUpsRwpo6'
```

- [Functions](https://docs.dune.com/query-engine/Functions-and-operators/tronaddress/#functions)
- [from\_tron\_address()](https://docs.dune.com/query-engine/Functions-and-operators/tronaddress/#from-tron-address)
- [to\_tron\_address()](https://docs.dune.com/query-engine/Functions-and-operators/tronaddress/#to-tron-address)