### Binary operators

The `||` operator performs concatenation.

### Binary functions

#### concat()

**`concat(binary1, ..., binaryN)`** → varbinary

Returns the concatenation of binary1, binary2, …, binaryN. This function provides the same functionality as the SQL-standard concatenation operator (||).

#### length()

**`length(binary)`** → bigint

Returns the length of binary in bytes.

#### lpad()

**`lpad(binary, size, padbinary)`** → varbinary

Left pads binary to size bytes with padbinary. If size is less than the length of binary, the result is truncated to size characters. size must not be negative and padbinary must be non-empty.

#### rpad()

**`rpad(binary, size, padbinary)`** → varbinary

Right pads binary to size bytes with padbinary. If size is less than the length of binary, the result is truncated to size characters. size must not be negative and padbinary must be non-empty.

#### substr()

**`substr(binary, start)`** → varbinary

Returns the rest of binary from the starting position start, measured in bytes. Positions start with 1. A negative starting position is interpreted as being relative to the end of the string.

**`substr(binary, start, length)`** → varbinary

Returns a substring from binary of length length from the starting position start, measured in bytes. Positions start with 1. A negative starting position is interpreted as being relative to the end of the string.

#### reverse()

**`reverse(binary)`** → varbinary

Returns binary with the bytes in reverse order.

### Base64 encoding functions

#### from\_base64()

**`from_base64(string)`** → varbinary

Decodes binary data from the base64 encoded string.

#### to\_base64()

**`to_base64(binary)`** → varchar

Encodes binary into a base64 string representation.

#### from\_base64url()

**`from_base64url(string)`** → varbinary

Decodes binary data from the base64 encoded string using the URL safe alphabet.

#### to\_base64url()

**`to_base64url(binary)`** → varchar

Encodes binary into a base64 string representation using the URL safe alphabet.

#### from\_base32()

**`from_base32(string)`** → varbinary

Decodes binary data from the base32 encoded string.

#### to\_base32()

**`to_base32(binary)`** → varchar

Encodes binary into a base32 string representation.

### Hex encoding functions

#### from\_hex()

**`from_hex(string)`** → varbinary

Decodes binary data from the hex encoded string.

#### to\_hex()

**`to_hex(binary)`** → varchar

Encodes binary into a hex string representation.

### Integer encoding functions

#### from\_big\_endian\_32()

**`from_big_endian_32(binary)`** → integer

Decodes the 32-bit two’s complement big-endian binary. The input must be exactly 4 bytes.

#### to\_big\_endian\_32()

**`to_big_endian_32(integer)`** → varbinary

Encodes integer into a 32-bit two’s complement big-endian format.

#### from\_big\_endian\_64()

**`from_big_endian_64(binary)`** → bigint

Decodes the 64-bit two’s complement big-endian binary. The input must be exactly 8 bytes.

#### to\_big\_endian\_64()

**`to_big_endian_64(bigint)`** → varbinary

Encodes bigint into a 64-bit two’s complement big-endian format.

### Floating-point encoding functions

#### from\_ieee754\_32()

**`from_ieee754_32(binary)`** → real

Decodes the 32-bit big-endian binary in IEEE 754 single-precision floating-point format. The input must be exactly 4 bytes.

#### to\_ieee754\_32()

**`to_ieee754_32(real)`** → varbinary

Encodes real into a 32-bit big-endian binary according to IEEE 754 single-precision floating-point format.

#### from\_ieee754\_64()

**`from_ieee754_64(binary)`** → double

Decodes the 64-bit big-endian binary in IEEE 754 double-precision floating-point format. The input must be exactly 8 bytes.

#### to\_ieee754\_64()

**`to_ieee754_64(double)`** → varbinary

Encodes double into a 64-bit big-endian binary according to IEEE 754 double-precision floating-point format.

### Hashing functions

#### crc32()

**`crc32(binary)`** → bigint

Computes the CRC-32 of binary. For general purpose hashing, use xxhash64(), as it is much faster and produces a better quality hash.

#### md5()

**`md5(binary)`** → varbinary

Computes the MD5 hash of binary.

#### sha1()

**`sha1(binary)`** → varbinary

Computes the SHA1 hash of binary.

#### sha256()

**`sha256(binary)`** → varbinary

Computes the SHA256 hash of binary.

#### sha512()

**`sha512(binary)`** → varbinary

Computes the SHA512 hash of binary.

#### spooky\_hash\_v2\_32()

**`spooky_hash_v2_32(binary)`** → varbinary

Computes the 32-bit SpookyHashV2 hash of binary.

#### spooky\_hash\_v2\_64()

**`spooky_hash_v2_64(binary)`** → varbinary

Computes the 64-bit SpookyHashV2 hash of binary.

#### xxhash64()

**`xxhash64(binary)`** → varbinary

Computes the 64-bit xxHash hash of binary.

### HMAC functions

#### hmac\_md5()

**`hmac_md5(binary, key)`** → varbinary

Computes HMAC with MD5 of binary with the given key.

#### hmac\_sha1()

**`hmac_sha1(binary, key)`** → varbinary

Computes HMAC with SHA1 of binary with the given key.

#### hmac\_sha256()

**`hmac_sha256(binary, key)`** → varbinary

Computes HMAC with SHA256 of binary with the given key.

#### hmac\_sha512()

**`hmac_sha512(binary, key)`** → varbinary

Computes HMAC with SHA512 of binary with the given key.