- [Overview](https://docs.dune.com/query-engine/overview)

##### Functionality

- [Executions](https://docs.dune.com/query-engine/query-executions)
- [Query Views](https://docs.dune.com/query-engine/query-a-query)
- [Materialized Views](https://docs.dune.com/query-engine/materialized-views)

##### DuneSQL

- [Writing Efficient Queries](https://docs.dune.com/query-engine/writing-efficient-queries)
- [Datatypes](https://docs.dune.com/query-engine/datatypes)
- [Reserved keywords](https://docs.dune.com/query-engine/reserved-keywords)

##### Functions and Operators

- [Overview](https://docs.dune.com/query-engine/Functions-and-operators/index)
- [Aggregate functions](https://docs.dune.com/query-engine/Functions-and-operators/aggregate)
- [Array functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/array)
- [Base58 functions](https://docs.dune.com/query-engine/Functions-and-operators/base58)
- [Binary](https://docs.dune.com/query-engine/Functions-and-operators/binary)
- [Bitwise](https://docs.dune.com/query-engine/Functions-and-operators/bitwise)
- [Chain utility functions](https://docs.dune.com/query-engine/Functions-and-operators/chain-utility-functions)
- [Comparisons](https://docs.dune.com/query-engine/Functions-and-operators/comparison)
- [Conditional expressions](https://docs.dune.com/query-engine/Functions-and-operators/conditional)
- [Conversions](https://docs.dune.com/query-engine/Functions-and-operators/conversion)
- [Date and time functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/datetime)
- [Decimal functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/decimal)
- [EVM Decoding Functions](https://docs.dune.com/query-engine/Functions-and-operators/evm-decoding-functions)
- [HyperLogLog functions](https://docs.dune.com/query-engine/Functions-and-operators/hyperloglog)
- [JSON functions](https://docs.dune.com/query-engine/Functions-and-operators/json)
- [Lambda expressions](https://docs.dune.com/query-engine/Functions-and-operators/lambda)
- [LiveFetch functions](https://docs.dune.com/query-engine/Functions-and-operators/live-fetch)
- [Logical operators](https://docs.dune.com/query-engine/Functions-and-operators/logical)
- [Map functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/map)
- [Mathematical functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/math)
- [Machine learning functions](https://docs.dune.com/query-engine/Functions-and-operators/ml)
- [Quantile digest functions](https://docs.dune.com/query-engine/Functions-and-operators/qdigest)
- [Regular expression functions](https://docs.dune.com/query-engine/Functions-and-operators/regexp)
- [Set Digest functions](https://docs.dune.com/query-engine/Functions-and-operators/setdigest)
- [SS58 functions](https://docs.dune.com/query-engine/Functions-and-operators/ss58)
- [Tron address functions](https://docs.dune.com/query-engine/Functions-and-operators/tronaddress)
- [String functions and operators](https://docs.dune.com/query-engine/Functions-and-operators/string)
- [System information](https://docs.dune.com/query-engine/Functions-and-operators/system)
- [T-Digest functions](https://docs.dune.com/query-engine/Functions-and-operators/tdigest)
- [Teradata functions](https://docs.dune.com/query-engine/Functions-and-operators/teradata)
- [URL functions](https://docs.dune.com/query-engine/Functions-and-operators/url)
- [UUID functions](https://docs.dune.com/query-engine/Functions-and-operators/uuid)
- [Varbinary functions (DuneSQL)](https://docs.dune.com/query-engine/Functions-and-operators/varbinary)
- [Varchar utility functions](https://docs.dune.com/query-engine/Functions-and-operators/varchar-utility-functions)
- [Window functions](https://docs.dune.com/query-engine/Functions-and-operators/window)

Functions and Operators

DuneSQL supports a wide range of built-in functions and operators.

This chapter describes the built-in SQL functions and operators supported by Trino. They allow you to implement complex functionality and behavior of the SQL executed by Trino operating on the underlying data sources.

Using `SHOW FUNCTIONS` in the query editor returns a list of all available functions, including custom functions, with all supported arguments and a short description.

### 

[​](https://docs.dune.com/query-engine/Functions-and-operators/index/#dunesql-added-functions)

DuneSQL Added Functions:

- [Varbinary datatypes for EVM data](https://docs.dune.com/query-engine/Functions-and-operators/varbinary)
- [Base58 for Bitcoin&Solana data](https://docs.dune.com/query-engine/Functions-and-operators/base58)
- [ss58 for Substrate data](https://docs.dune.com/query-engine/Functions-and-operators/ss58)
- [Tron Address Functions](https://docs.dune.com/query-engine/Functions-and-operators/tronaddress)
- [Chain Utility Functions](https://docs.dune.com/query-engine/Functions-and-operators/chain-utility-functions)
- [Varchar Utility Functions](https://docs.dune.com/query-engine/Functions-and-operators/varchar-utility-functions)
- [LiveFetch Functions](https://docs.dune.com/query-engine/Functions-and-operators/live-fetch)

### 

[​](https://docs.dune.com/query-engine/Functions-and-operators/index/#trino-base-functions)

Trino Base Functions:

- [Aggregate](https://docs.dune.com/query-engine/Functions-and-operators/aggregate)
- [Array](https://docs.dune.com/query-engine/Functions-and-operators/array)
- [Binary](https://docs.dune.com/query-engine/Functions-and-operators/binary)
- [Bitwise](https://docs.dune.com/query-engine/Functions-and-operators/bitwise)
- [Comparison](https://docs.dune.com/query-engine/Functions-and-operators/comparison)
- [Conditional](https://docs.dune.com/query-engine/Functions-and-operators/conditional)
- [Conversion](https://docs.dune.com/query-engine/Functions-and-operators/conversion)
- [Date and time](https://docs.dune.com/query-engine/Functions-and-operators/datetime)
- [Decimal](https://docs.dune.com/query-engine/Functions-and-operators/decimal)
- [HyperLogLog](https://docs.dune.com/query-engine/Functions-and-operators/hyperloglog)
- [JSON](https://docs.dune.com/query-engine/Functions-and-operators/json)
- [Lambda](https://docs.dune.com/query-engine/Functions-and-operators/lambda)
- [Logical](https://docs.dune.com/query-engine/Functions-and-operators/logical)
- [Map](https://docs.dune.com/query-engine/Functions-and-operators/map)
- [Math](https://docs.dune.com/query-engine/Functions-and-operators/math)
- [Quantile digest](https://docs.dune.com/query-engine/Functions-and-operators/qdigest)
- [Regular expression](https://docs.dune.com/query-engine/Functions-and-operators/regexp)
- [Set Digest](https://docs.dune.com/query-engine/Functions-and-operators/setdigest)
- [String](https://docs.dune.com/query-engine/Functions-and-operators/string)
- [System](https://docs.dune.com/query-engine/Functions-and-operators/system)
- [Teradata](https://docs.dune.com/query-engine/Functions-and-operators/teradata)
- [T-Digest](https://docs.dune.com/query-engine/Functions-and-operators/tdigest)
- [URL](https://docs.dune.com/query-engine/Functions-and-operators/url)
- [UUID](https://docs.dune.com/query-engine/Functions-and-operators/uuid)
- [Window](https://docs.dune.com/query-engine/Functions-and-operators/window)

Was this page helpful?

[Raise issue](https://github.com/duneanalytics/dune-docs/issues/new?title=Issue%20on%20docs&body=Path:%20/query-engine/Functions-and-operators/index)

[Reserved keywords](https://docs.dune.com/query-engine/reserved-keywords)[Aggregate functions](https://docs.dune.com/query-engine/Functions-and-operators/aggregate)

On this page

- [DuneSQL Added Functions:](https://docs.dune.com/query-engine/Functions-and-operators/index/#dunesql-added-functions)
- [Trino Base Functions:](https://docs.dune.com/query-engine/Functions-and-operators/index/#trino-base-functions)