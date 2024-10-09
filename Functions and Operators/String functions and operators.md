The `||` operator performs concatenation.

The `LIKE` statement can be used for pattern matching and is documented in `like_operator`.

## String functions

#### chr()

**`chr(n)`** → varchar  
Returns the Unicode code point `n` as a single character string.

#### codepoint()

**`codepoint(string)`** → integer  
Returns the Unicode code point of the only character of `string`.

#### concat()

**`concat(string1, ..., stringN)`** → varchar  
Returns the concatenation of `string1`, `string2`, `...`, `stringN`. This function provides the same functionality as the SQL-standard concatenation operator (`||`).

#### concat\_ws()

**`concat_ws(string0, string1, ..., stringN)`** → varchar  
Returns the concatenation of `string1`, `string2`, `...`, `stringN` using `string0` as a separator. If `string0` is null, then the return value is null. Any null values provided in the arguments after the separator are skipped.

#### concat\_ws()

**`concat_ws(string0, array(varchar))`** → varchar  
Returns the concatenation of elements in the array using `string0` as a separator. If `string0` is null, then the return value is null. Any null values in the array are skipped.

#### format()

**`format(format, args...)`** → varchar  
See `format`.

#### hamming\_distance()

**`hamming_distance(string1, string2)`** → bigint  
Returns the Hamming distance of `string1` and `string2`, i.e. the number of positions at which the corresponding characters are different. Note that the two strings must have the same length.

#### length()

**`length(string)`** → bigint  
Returns the length of `string` in characters.

#### levenshtein\_distance()

**`levenshtein_distance(string1, string2)`** → bigint  
Returns the Levenshtein edit distance of `string1` and `string2`, i.e. the minimum number of single-character edits (insertions, deletions or substitutions) needed to change `string1` into `string2`.

#### lower()

**`lower(string)`** → varchar  
Converts `string` to lowercase.

#### lpad()

**`lpad(string, size, padstring)`** → varchar  
Left pads `string` to `size` characters with `padstring`. If `size` is less than the length of `string`, the result is truncated to `size` characters. `size` must not be negative and `padstring` must be non-empty.

#### ltrim()

**`ltrim(string)`** → varchar  
Removes leading whitespace from `string`.

#### luhn\_check()

**`luhn_check(string)`** → boolean  
Tests whether a `string` of digits is valid according to the [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm). This checksum function, also known as `modulo 10` or `mod 10`, is widely applied on credit card numbers and government identification numbers to distinguish valid numbers from mistyped, incorrect numbers.

Valid identification number:

select luhn\_check(‘79927398713’); — true

Invalid identification number:

select luhn\_check(‘79927398714’); — false

#### position()

**`position(substring IN string)`** → bigint

Returns the starting position of the first instance of `substring` in `string`. Positions start with `1`. If not found, `0` is returned.

Note: This SQL-standard function has special syntax and uses the `IN` keyword for the arguments. See also `strpos`.

#### replace()

**`replace(string, search)`** → varchar

Removes all instances of `search` from `string`.

**`replace(string, search, replace)`** → varchar

Replaces all instances of `search` with `replace` in `string`.

#### reverse()

**`reverse(string)`** → varchar

Returns `string` with the characters

#### rpad()

**`rpad(string, size, padstring)`** → varchar

Right pads `string` to `size` characters with `padstring`. If `size` is less than the length of `string`, the result is truncated to `size` characters. `size` must not be negative and `padstring` must be non-empty.

#### rtrim()

**`rtrim(string)`** → varchar

Removes trailing whitespace from `string`.

#### soundex()

**`soundex(char)`** → string

`soundex` returns a character string containing the phonetic representation of `char`.

It is typically used to evaluate the similarity of two expressions phonetically, that is how the string sounds when spoken:

```sql
    SELECT name
    FROM nation
    WHERE SOUNDEX(name)  = SOUNDEX('CHYNA');
```

```text
     name  |
    -------+----
     CHINA |
    (1 row)
```

#### split()

**`split(string, delimiter)`** → array(varchar)

Splits `string` on `delimiter` and returns an array.

#### split()

**`split(string, delimiter, limit)`** → array(varchar)

Splits `string` on `delimiter` and returns an array of size at most `limit`. The last element in the array always contain everything left in the `string`. `limit` must be a positive number.

#### split\_part()

**`split_part(string, delimiter, index)`** → varchar

Splits `string` on `delimiter` and returns the field `index`. Field indexes start with `1`. If the index is larger than the number of fields, then null is returned.

#### split\_to\_map()

**`split_to_map(string, entryDelimiter, keyValueDelimiter)`** → map(varchar, varchar)

Splits `string` by `entryDelimiter` and `keyValueDelimiter` and returns a map. `entryDelimiter` splits `string` into key-value pairs. `keyValueDelimiter` splits each pair into key and value.

#### split\_to\_multimap()

**`split_to_multimap(string, entryDelimiter, keyValueDelimiter)`** → map(varchar, array(varchar))

Splits `string` by `entryDelimiter` and `keyValueDelimiter` and returns a map containing an array of values for each unique key. `entryDelimiter` splits `string` into key-value pairs. `keyValueDelimiter` splits each pair into key and value. The values for each key will be in the same order as they appeared in `string`.

#### strpos()

**`strpos(string, substring)`** → bigint

Returns the starting position of the first instance of `substring` in `string`. Positions start with `1`. If not found, `0` is returned.

**`strpos(string, substring, instance)`** → bigint

Returns the position of the N-th `instance` of `substring` in `string`. When `instance` is a negative number the search will start from the end of `string`. Positions start with `1`. If not found, `0` is returned.

#### starts\_with()

**`starts_with(string, substring)`** → boolean

Tests whether `substring` is a prefix of `string`.

#### substring()

**`substr(string, start)`** → varchar

This is an alias for `substring`.

**`substring(string, start)`** → varchar

Returns the rest of `string` from the starting position `start`. Positions start with `1`. A negative starting position is interpreted as being relative to the end of the string.

**`substr(string, start, length)`** → varchar

This is an alias for `substring`.

**`substring(string, start, length)`** → varchar

Returns a substring from `string` of length `length` from the starting position `start`. Positions start with `1`. A negative starting position is interpreted as being relative to the end of the string.

#### translate()

**`translate(source, from, to)`** → varchar

Returns the `source` string translated by replacing characters found in the

**`translate(source, from, to)`** → varchar

Returns the `source` string translated by replacing characters found in the `from` string with the corresponding characters in the `to` string. If the `from` string contains duplicates, only the first is used. If the `source` character does not exist in the `from` string, the `source` character will be copied without translation. If the index of the matching character in the `from` string is beyond the length of the `to` string, the `source` character will be omitted from the resulting string.

Here are some examples illustrating the translate function:

```sql
    SELECT translate('abcd', '', ''); -- 'abcd'
    SELECT translate('abcd', 'a', 'z'); -- 'zbcd'
    SELECT translate('abcda', 'a', 'z'); -- 'zbcdz'
    SELECT translate('Palhoça', 'ç','c'); -- 'Palhoca'
    SELECT translate('abcd', 'b', U&'\+01F600'); -- a😀cd
    SELECT translate('abcd', 'a', ''); -- 'bcd'
    SELECT translate('abcd', 'a', 'zy'); -- 'zbcd'
    SELECT translate('abcd', 'ac', 'z'); -- 'zbd'
    SELECT translate('abcd', 'aac', 'zq'); -- 'zbd'
```

#### trim()

**`trim(string)`** → varchar

Removes leading and trailing whitespace from `string`.

**`trim( \[ \[ specification \] \[ string \] FROM \] source )`** → varchar

Removes any leading and/or trailing characters as specified up to and including `string` from `source`:

```sql
    SELECT trim('!' FROM '!foo!'); -- 'foo'
    SELECT trim(LEADING FROM '  abcd');  -- 'abcd'
    SELECT trim(BOTH ' FROM '$var); -- 'var'
    SELECT trim(TRAILING 'ER' FROM upper('worker')); -- 'WORK'
```

#### upper()

**`upper(string)`** → varchar

Converts `string` to uppercase.

#### word\_stem()

**`word_stem(word)`** → varchar

Returns the stem of `word` in the English language.

**`word_stem(word, lang)`** → varchar

Returns the stem of `word` in the `lang` language.

## Unicode functions

#### keccak()

**`keccak(varbinary)`** → varbinary

Returns the Keccak-256 hash of `varbinary`.

```sql
    SELECT keccak(to_utf8('Transfer(address,address,uint256)')) --0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
```

#### normalize()

**`normalize(string)`** → varchar

Transforms `string` with NFC normalization form.

**`normalize(string, form)`** → varchar

Transforms `string` with the specified normalization form. `form` must be one of the following keywords:

| Form | Description |
| --- | --- |
| `NFD` | Canonical Decomposition |
| `NFC` | Canonical Decomposition, followed by Canonical Composition |
| `NFKD` | Compatibility Decomposition |
| `NFKC` | Compatibility Decomposition, followed by Canonical Composition |

#### to\_utf8()

**`to_utf8(string)`** → varbinary

Encodes `string` into a UTF-8 varbinary representation.

```sql
    SELECT to_utf8('Hello, world!'); -- 0x48656C6C6F2C20776F726C6421
    Select keccak(to_utf8('Transfer(address,address,uint256)')) --0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef 
```

#### from\_utf8()

**`from_utf8(binary)`** → varchar

Decodes a UTF-8 encoded string from `binary`. Invalid UTF-8 sequences are replaced with the Unicode replacement character `U+FFFD`.

**`from_utf8(binary, replace)`** → varchar

Decodes a UTF-8 encoded string from `binary`. Invalid UTF-8 sequences are replaced with `replace`. The replacement string `replace` must either be a single character or empty (in which case invalid characters are removed).