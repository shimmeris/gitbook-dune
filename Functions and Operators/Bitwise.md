#### bit\_count()

**`bit_count(x, bits)`** → bigint Count the number of bits set in x (treated as bits-bit signed integer) in 2’s complement representation:

```sql
SELECT bit_count(9, 64); -- 2
SELECT bit_count(9, 8); -- 2
SELECT bit_count(-7, 64); -- 62
SELECT bit_count(-7, 8); -- 6
```

#### bitwise\_and()

**`bitwise_and(x, y)`** → bigint Returns the bitwise AND of x and y in 2’s complement representation.

Bitwise AND of 19 (binary: 10011) and 25 (binary: 11001) results in 17 (binary: 10001):

```sql
SELECT bitwise_and(19,25); -- 17
```

**`bitwise_not(x)`** → bigint

Returns the bitwise NOT of x in 2’s complement representation (NOT x = -x - 1):

```sql
SELECT bitwise_not(-12); --  11
SELECT bitwise_not(19);  -- -20
SELECT bitwise_not(25);  -- -26
```

#### bitwise\_or()

**`bitwise_or(x, y)`** → bigint

Returns the bitwise OR of x and y in 2’s complement representation.

Bitwise OR of 19 (binary: 10011) and 25 (binary: 11001) results in 27 (binary: 11011):

```sql
SELECT bitwise_or(19,25); -- 27
```

#### bitwise\_xor()

**`bitwise_xor(x, y)`** → bigint

Returns the bitwise XOR of x and y in 2’s complement representation.

Bitwise XOR of 19 (binary: 10011) and 25 (binary: 11001) results in 10 (binary: 01010):

```sql
SELECT bitwise_xor(19,25); -- 10
```

#### bitwise\_left\_shift()

**`bitwise_left_shift(value, shift)`** → \[same as value\] Returns the left shifted value of value.

Shifting 1 (binary: 001) by two bits results in 4 (binary: 00100):

```sql
SELECT bitwise_left_shift(1, 2); -- 4
```

Shifting 5 (binary: 0101) by two bits results in 20 (binary: 010100):

```sql
SELECT bitwise_left_shift(5, 2); -- 20
```

Shifting a value by 0 always results in the original value:

```sql
SELECT bitwise_left_shift(20, 0); -- 20
SELECT bitwise_left_shift(42, 0); -- 42
```

Shifting 0 by a shift always results in 0:

```sql
SELECT bitwise_left_shift(0, 1); -- 0
SELECT bitwise_left_shift(0, 2); -- 0
```

#### bitwise\_right\_shift()

**`bitwise_right_shift(value, shift)`** → \[same as value\]

Returns the logical right shifted value of value.

Shifting 8 (binary: 1000) by three bits results in 1 (binary: 001):

```sql
SELECT bitwise_right_shift(8, 3); -- 1
```

Shifting 9 (binary: 1001) by one bit results in 4 (binary: 100):

```sql
SELECT bitwise_right_shift(9, 1); -- 4
```

Shifting a value by 0 always results in the original value:

```sql
SELECT bitwise_right_shift(20, 0); -- 20
SELECT bitwise_right_shift(42, 0); -- 42
```

Shifting a value by 64 or more bits results in 0:

```sql
SELECT bitwise_right_shift( 12, 64); -- 0
SELECT bitwise_right_shift(-45, 64); -- 0
```

Shifting 0 by a shift always results in 0:

```sql
SELECT bitwise_right_shift(0, 1); -- 0
SELECT bitwise_right_shift(0, 2); -- 0
```

#### bitwise\_right\_shift\_arithmetic()

**`bitwise_right_shift_arithmetic(value, shift)`** → \[same as value\]

Returns the arithmetic right shifted value of value.

Returns the same values as bitwise\_right\_shift() when shifting by less than 64 bits. Shifting by 64 or more bits results in 0 for a positive and -1 for a negative value:

```sql
SELECT bitwise_right_shift_arithmetic( 12, 64); -- 0
SELECT bitwise_right_shift_arithmetic(-45, 64); -- -1
```