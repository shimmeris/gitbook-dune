Aggregate functions operate on a set of values to compute a single result.

Except for `count`, `count_if`, `max_by`, `min_by` and `approx_distinct`, all of these aggregate functions ignore null values and return null for no input rows or when all values are null. For example, `sum` returns null rather than zero and `avg` does not include null values in the count. The `coalesce` function can be used to convert null into zero.

## Ordering during aggregation

Some aggregate functions such as `array_agg` produce different results depending on the order of input values. This ordering can be specified by writing an `order-by-clause` within the aggregate function:

```sql
    array_agg(x ORDER BY y DESC)
    array_agg(x ORDER BY x, y, z)
```

## Filtering during aggregation

The `FILTER` keyword can be used to remove rows from aggregation processing with a condition expressed using a `WHERE` clause. This is evaluated for each row before it is used in the aggregation and is supported for all aggregate functions.

```sql
aggregate_function(...) FILTER (WHERE <condition>)
```

A common and very useful example is to use `FILTER` to remove nulls from consideration when using `array_agg`:

```sql
    SELECT array_agg(name) FILTER (WHERE name IS NOT NULL)
    FROM region;
```

As another example, imagine you want to add a condition on the count for Iris flowers, modifying the following query:

```sql
    SELECT species,
           count(*) AS count
    FROM iris
    GROUP BY species;
```

```text
species    | count
-----------+-------
setosa     |   50
virginica  |   50
versicolor |   50
```

If you just use a normal `WHERE` statement you lose information:

```sql
    SELECT species,
        count(*) AS count
    FROM iris
    WHERE petal_length_cm > 4
    GROUP BY species;
```

```text
species    | count
-----------+-------
virginica  |   50
versicolor |   34
```

Using a filter you retain all information:

```sql
    SELECT species,
           count(*) FILTER (where petal_length_cm > 4) AS count
    FROM iris
    GROUP BY species;
```

```text
species    | count
-----------+-------
virginica  |   50
setosa     |    0
versicolor |   34
```

## General aggregate functions

#### arbitrary()

**`arbitrary(x)`** → \[same as input\]

Returns an arbitrary non-null value of `x`, if one exists.

#### any\_value()

**`any_value(x)`** → \[same as input\]

Returns an arbitrary non-null value of `x`, if one exists. This is an alias for `arbitrary`.

#### array\_agg()

**`array_agg(x)`** → \[same as input\]

Returns an array created from the input `x` elements.

#### avg()

**`avg(x)`** → double

Returns the average (arithmetic mean) of all input values.

**`avg(time interval type)`** → time interval type

Returns the average interval length of all input values.

#### bool\_and()

**`bool_and(boolean)`** → boolean

Returns `TRUE` if every input value is `TRUE`, otherwise `FALSE`.

#### bool\_or()

**`bool_or(boolean)`** → boolean

Returns `TRUE` if any input value is `TRUE`, otherwise `FALSE`.

#### checksum()

**`checksum(x)`** → varbinary

Returns an order-insensitive checksum of the given values.

#### count()

**`count(*)`** → bigint

Returns the number of input rows.

**`count(x)`** → bigint

Returns the number of non-null input values.

#### count\_if()

**`count_if(x)`** → bigint

Returns the number of `TRUE` input values. This function is equivalent to `count(CASE WHEN x THEN 1 END)`.

#### every()

**`every(boolean)`** → boolean

This is an alias for `bool_and`.

#### geometric\_mean()

**`geometric_mean(x)`** → double

Returns the geometric mean of all input values.

#### listagg()

**`listagg(x, separator)`** → varchar

Returns the concatenated input values, separated by the `separator` string.

Synopsis:

```sql
    LISTAGG( expression [, separator] [ON OVERFLOW overflow_behaviour])
        WITHIN GROUP (ORDER BY sort_item, [...])
```

If `separator` is not specified, the empty string will be used as `separator`.

In its simplest form the function looks like:

```sql
    SELECT listagg(value, ',') WITHIN GROUP (ORDER BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);
```

and results in:

```text
    csv_value
    -----------
    'a,b,c'
```

The overflow behaviour is by default to throw an error in case that the length of the output of the function exceeds `1048576` bytes:

```sql
    SELECT listagg(value, ',' ON OVERFLOW ERROR) WITHIN GROUP (ORDER
    BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);
```

and results in:

```text
    csv_value
    -----------
    'a,c,b'
```

The overflow behaviour can also be to truncate the output:

```sql
    SELECT listagg(value, ',' ON OVERFLOW TRUNCATE) WITHIN GROUP (ORDER
    BY value) csv_value
    FROM (VALUES 'a', 'c', 'b') t(value);
```

and results in:

```text
    csv_value
    -----------
    'a,b'
```

The overflow behaviour can also be to skip the overflowed values:

```sql
    SELECT listagg(value, ',' ON OVERFLOW SKIP) WITHIN GROUP (ORDER
    BY value) csv_value
```

The current implementation of `LISTAGG` function does not support window frames.

#### max()

**`max(x)`** → \[same as input\]

Returns the maximum value of all input values.

**`max(x, n)`** → array<\[same as x\]>

Returns `n` largest values of all input values of `x`.

#### max\_by()

**`max_by(x, y)`** → \[same as x\]

Returns the value of `x` associated with the maximum value of `y` over all input values.

**`max_by(x, y, n)`** → array<\[same as x\]>

Returns `n` values of `x` associated with the `n` largest of all input values of `y` in descending order of `y`.

#### min()

**`min(x)`** → \[same as input\]

Returns the minimum value of all input values.

**`min(x, n)`** → array<\[same as x\]>

Returns `n` smallest values of all input values of `x`.

#### min\_by()

**`min_by(x, y)`** → \[same as x\]

Returns the value of `x` associated with the minimum value of `y` over all input values.

**`min_by(x, y, n)`** → array<\[same as x\]>

Returns `n` values of `x` associated with the `n` smallest of all input values of `y` in ascending order of `y`.

#### sum()

**`sum(x)`** → \[same as input\]

Returns the sum of all input values.

#### try\_sum()

**`try_sum(uint256)`** → uint256

Returns the sum of all input values, or null if an addition overflow occurred.

## Bitwise aggregate functions

#### bitwise\_and\_agg()

**`bitwise_and_agg(x)`** → bigint

Returns the bitwise AND of all input values in 2’s complement representation.

#### bitwise\_or\_agg()

**`bitwise_or_agg(x)`** → bigint

Returns the bitwise OR of all input values in 2’s complement representation.

#### bitwise\_xor\_agg()

**`bitwise_xor_agg(x)`** → bigint

Returns the bitwise XOR of all input non-NULL values in 2’s complement representation. If all records inside the group are NULL, or if the group is empty, the function returns NULL.

#### histogram()

**`histogram(x)`** → map<K,bigint>

Returns a map containing the count of the number of times each input value occurs.

#### map\_agg()

**`map_agg(key, value)`** → map<K,V>

Returns a map created from the input key/value pairs.

#### map\_union()

**`map_union(x(K, V))`** → map<K,V>

Returns the union of all the input maps. If a key is found in multiple input maps, that key’s value in the resulting map comes from an arbitrary input map.

For example, take the following histogram function that creates multiple maps from the Iris dataset:

```sql
SELECT histogram(floor(petal_length_cm)) petal_data
FROM memory.default.iris
GROUP BY species;

        petal_data
-- {4.0=6, 5.0=33, 6.0=11}
-- {4.0=37, 5.0=2, 3.0=11}
-- {1.0=50}
```

You can combine these maps using map\_union:

```sql
SELECT map_union(petal_data) petal_data_union
FROM (
       SELECT histogram(floor(petal_length_cm)) petal_data
       FROM memory.default.iris
       GROUP BY species
       );

             petal_data_union
--{4.0=6, 5.0=2, 6.0=11, 1.0=50, 3.0=11}
```

If you instead want to have the last value instead of an arbitrary value, use this snippet:

```sql
map_concat(map_filter(m.chain_stats, (k, v) -> NOT contains(map_keys(n.chain_stats), k)), n.chain_stats)
```

#### multimap\_agg()

**`multimap_agg(key, value)`** → map<K,array(V)>

Returns a multimap created from the input key / value pairs. Each key can be associated with multiple values.

## Approximate aggregate functions

#### approx\_distinct()

**`approx_distinct(x)`** → bigint

Returns the approximate number of distinct input values. This function provides an approximation of `count(DISTINCT x)`. Zero is returned if all input values are null.

This function should produce a standard error of 2.3%, which is the standard deviation of the (approximately normal) error distribution over all possible sets. It does not guarantee an upper bound on the error for any specific input set.

**`approx_distinct(x, e)`** → bigint

Returns the approximate number of distinct input values. This function provides an approximation of `count(DISTINCT x)`. Zero is returned if all input values are null.

This function should produce a standard error of no more than `e`, which is the standard deviation of the (approximately normal) error distribution over all possible sets. It does not guarantee an upper bound on the error for any specific input set. The current implementation of this function requires that `e` be in the range of 0.0040625 to 0.26000.

#### approx\_most\_frequent()

**`approx_most_frequent(x, k)`** → map<\[same as x\], bigint>

Computes the top frequent values up to `buckets` elements approximately. Approximate estimation of the function enables us to pick up the frequent values with less memory. Larger `capacity` improves the accuracy of underlying algorithm with sacrificing the memory capacity. The returned value is a map containing the top elements with corresponding estimated frequency.

The error of the function depends on the permutation of the values and its cardinality. We can set the capacity same as the cardinality of the underlying data to achieve the least error.

`buckets` and `capacity` must be `bigint`. `value` can be numeric or string type.

The function uses the stream summary data structure proposed in the paper [Efficient Computation of Frequent and Top-k Elements in Data Streams](https://www.cse.ust.hk/~raywong/comp5331/References/EfficientComputationOfFrequentAndTop-kElementsInDataStreams.pdf) by A. Metwalley, D. Agrawl and A. Abbadi.

#### approx\_percentile()

**`approx_percentile(x, percentage)`** → \[same as x\]

Returns the approximate percentile for all input values of `x` at the given `percentage`. The value of `percentage` must be between zero and one and must be constant for all input rows.

**`approx_percentile(x, percentages)`** → array<\[same as x\]>

Returns the approximate percentile for all input values of `x` at each of the specified percentages. Each element of the `percentages` array must be between zero and one, and the array must be constant for all input rows.

**`approx_percentile(x, w, percentage)`** → \[same as x\]

Returns the approximate weighed percentile for all input values of `x` using the per-item weight `w` at the percentage `percentage`. Weights must be greater or equal to 1. Integer-value weights can be thought of as a replication count for the value `x` in the percentile set. The value of `percentage` must be between zero and one and must be constant for all input rows.

**`approx_percentile(x, w, percentages)`** → array<\[same as x\]>

Returns the approximate weighed percentile for all input values of `x` using the per-item weight `w` at each of the given percentages specified in the array. Weights must be greater or equal to 1. Integer-value weights can be thought of as a replication count for the value `x` in the percentile set. Each element of the `percentages` array must be between zero and one, and the array must be constant for all input rows.

#### approx\_set()

**`approx_set(x)`** → HyperLogLog

See `hyperloglog`.

#### merge()

**`merge(x)`** → HyperLogLog

See `hyperloglog`.

**`merge(qdigest(T))`** → qdigest(T)

See `qdigest`.

**`merge(tdigest)`** → tdigest

See `tdigest`.

#### numeric\_histogram()

**`numeric_histogram(buckets, value)`** → map<double, double>

Computes an approximate histogram with up to `buckets` number of buckets for all `value`s. This function is equivalent to the variant of `numeric_histogram` that takes a `weight`, with a per-item weight of `1`.

**`numeric_histogram(buckets, value, weight)`** → map<double, double>

Computes an approximate histogram with up to `buckets` number of buckets for all `value`s with a per-item weight of `weight`. The algorithm is based loosely on:

```text
Yael Ben-Haim and Elad Tom-Tov, "A streaming parallel decision tree algorithm", J. Machine Learning Research 11 (2010), pp. 849--872.
```

`buckets` must be a `bigint`. `value` and `weight` must be numeric.

#### qdigest\_agg()

**`qdigest_agg(x)`** → qdigest

See [Quantile digest functions](https://docs.dune.com/query-engine/Functions-and-operators/qdigest).

#### qdigest\_agg()

**`qdigest_agg(x, w)`** → qdigest

See [Quantile digest functions](https://docs.dune.com/query-engine/Functions-and-operators/qdigest).

#### tdigest\_agg()

**`tdigest_agg(x)`** → tdigest

See [T-Digest functions](https://docs.dune.com/query-engine/Functions-and-operators/tdigest).

#### tdigest\_agg()

**`tdigest_agg(x, w)`** → tdigest

See [T-Digest functions](https://docs.dune.com/query-engine/Functions-and-operators/tdigest).

## Statistical aggregate functions

#### corr()

**`corr(x, y)`** → double

Returns correlation coefficient of input values.

#### covar\_pop()

**`covar_pop(y, x)`** → double

Returns the population covariance of input values.

#### covar\_samp()

**`covar_samp(y, x)`** → double

Returns the sample covariance of input values.

#### kurtosis()

**`kurtosis(x)`** → double

Returns the excess kurtosis of all input values. Unbiased estimate using the following expression:

```text
kurtosis(x) = n(n+1)/((n-1)(n-2)(n-3))sum[(x_i-mean)^4]/stddev(x)^4-3(n-1)^2/((n-2)(n-3))
```

#### regr\_intercept()

**`regr_intercept(y, x)`** → double

Returns linear regression intercept of input values. `y` is the dependent value and `x` is the independent value.

#### regr\_slope()

**`regr_slope(y, x)`** → double

Returns linear regression slope of input values. `y` is the dependent value and `x` is the independent value.

#### skewness()

**`skewness(x)`** → double

Returns the skewness of all input values. Returns the Fisher’s moment coefficient of [skewness](https://en.wikipedia.org/wiki/Skewness) of all input values.

#### stddev()

**`stddev(x)`** → double

Returns the standard deviation of all input values.

#### stddev\_pop()

**`stddev_pop(x)`** → double

Returns the population standard deviation of all input values.

#### stddev\_samp()

**`stddev_samp(x)`** → double

Returns the sample standard deviation of all input values.

#### variance()

**`variance(x)`** → double

Returns the variance of all input values.

#### var\_pop()

**`var_pop(x)`** → double

Returns the population variance of all input values.

#### var\_samp()

**`var_samp(x)`** → double

Returns the sample variance of all input values.

## Lambda aggregate functions

#### reduce\_agg()

**`reduce_agg(inputValue T, initialState S, inputFunction(S, T, S), combineFunction(S, S, S))`** → S

Reduces all input values into a single value. `inputFunction` will be invoked for each non-null input value. In addition to taking the input value, `inputFunction` takes the current state, initially `initialState`, and returns the new state. `combineFunction` will be invoked to combine two states into a new state. The final state is returned:

```sql
    SELECT id, reduce_agg(value, 0, (a, b) -> a + b, (a, b) -> a + b)
    FROM (
        VALUES
            (1, 3),
            (1, 4),
            (1, 5),
            (2, 6),
            (2, 7)
    ) AS t(id, value)
    GROUP BY id;
    -- (1, 12)
    -- (2, 13)
```

```sql
    SELECT id, reduce_agg(value, 1, (a, b) -> a * b, (a, b) -> a * b)
    FROM (
        VALUES
            (1, 3),
            (1, 4),
            (1, 5),
            (2, 6),
            (2, 7)
    ) AS t(id, value)
    GROUP BY id;
    -- (1, 60)
    -- (2, 42)
```

The state type must be a boolean, integer, floating-point, or date/time/interval.