```sql
SELECT
sp.call_inner_instructions[1].data
,from_base58(sp.call_inner_instructions[1].data) as first_step
,bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8) as second_step
,bytearray_reverse(bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8)) as third_step
,bytearray_to_bigint(bytearray_reverse(bytearray_substring(from_base58(sp.call_inner_instructions[1].data), 2, 8))) as decoded_amount
FROM whirlpool_solana.whirlpool_call_swap sp
WHERE sp.account_whirlpool = '7qbRF6YsyGuLUVs6Y1q64bdVrfe4ZcUUz1JRdoVNUJnm'
AND call_tx_id = '44kmeC1edSfp21K5kKNVViJvLHG8XQqqu3KbHsrYcYZGmopWwBgP48c9u1DRBMGtQcbvyxd2TT8syY7ZvwpHqkhF'
and call_block_slot = 187701147
```