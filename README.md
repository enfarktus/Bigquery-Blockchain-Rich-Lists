# Bigquery-Blockchain-Rich-Lists
Creating rich address lists of several coins with bigquery.

Rich address lists can be easily created with bigquery:

1- ******* BİTCOİN *******
**************************

WITH double_entry_book AS (
   -- debits
   SELECT array_to_string(inputs.addresses, ",") AS address, inputs.type, -inputs.value AS value
   FROM `bigquery-public-data.crypto_bitcoin.inputs` AS inputs
   UNION ALL
   -- credits
   SELECT array_to_string(outputs.addresses, ",") AS address, outputs.type, outputs.value AS value
   FROM `bigquery-public-data.crypto_bitcoin.outputs` AS outputs
)
SELECT address, type, sum(value) AS balance
FROM double_entry_book
GROUP BY address, type
ORDER BY balance DESC
LIMIT 1000000

******************************

2- ******* DOGE *******
**************************

WITH double_entry_book AS (
   -- debits
   SELECT array_to_string(inputs.addresses, ",") AS address, inputs.type, -inputs.value AS value
   FROM `bigquery-public-data.crypto_dogecoin.inputs` AS inputs
   UNION ALL
   -- credits
   SELECT array_to_string(outputs.addresses, ",") AS address, outputs.type, outputs.value AS value
   FROM `bigquery-public-data.crypto_dogecoin.outputs` AS outputs
)
SELECT address, type, sum(value) AS balance
FROM double_entry_book
GROUP BY address, type
ORDER BY balance DESC
LIMIT 1000000

*******************************

3- ******* BİTCOİN CASH *******
*******************************

WITH double_entry_book AS (
   -- debits
   SELECT array_to_string(inputs.addresses, ",") AS address, inputs.type, -inputs.value AS value
   FROM `bigquery-public-data.crypto_bitcoin_cash.inputs` AS inputs
   UNION ALL
   -- credits
   SELECT array_to_string(outputs.addresses, ",") AS address, outputs.type, outputs.value AS value
   FROM `bigquery-public-data.crypto_bitcoin_cash.outputs` AS outputs
)
SELECT address, type, sum(value) AS balance
FROM double_entry_book
GROUP BY address, type
ORDER BY balance DESC
LIMIT 1000000
***********************************

4- ******* LİTECOİN *******
*******************************

WITH double_entry_book AS (
   -- debits
   SELECT array_to_string(inputs.addresses, ",") AS address, inputs.type, -inputs.value AS value
   FROM `bigquery-public-data.crypto_litecoin.inputs` AS inputs
   UNION ALL
   -- credits
   SELECT array_to_string(outputs.addresses, ",") AS address, outputs.type, outputs.value AS value
   FROM `bigquery-public-data.crypto_litecoin.outputs` AS outputs
)
SELECT address, type, sum(value) AS balance
FROM double_entry_book
GROUP BY address, type
ORDER BY balance DESC
LIMIT 1000000
*************************************

5- ******* SOLANA *******
*******************************

SELECT
  pubkey,
  CAST(lamports AS numeric ) / 1E09 AS SOL
FROM
  `bigquery-public-data.crypto_solana_mainnet_us.Accounts`
ORDER BY
  lamports DESC
LIMIT
  1000000;
*************************

6- ******* ETHEREUM *******
*******************************
SELECT `address`, `eth_balance`
FROM `bigquery-public-data.crypto_ethereum.balances`
WHERE `eth_balance` != 0
ORDER BY `eth_balance` DESC
LIMIT 30000


donation:
0xe47BBeAc8F268d7126082D5574B6f027f95AF5FB 
3FerqQF5DVY1tPCEV7nXENoqxuVHGLjRh3











