## System information

Functions providing information about the Trino cluster system environment. More information is available by querying the various schemas and tables exposed by the `/connector/system`.

## Function

**`version()`** -> varchar

Returns the Trino version used on the cluster. Equivalent to the value of the `node_version` column in the `system.runtime.nodes` table.

- [System information](https://docs.dune.com/query-engine/Functions-and-operators/system/#system-information)
- [Function](https://docs.dune.com/query-engine/Functions-and-operators/system/#function)