pbtx_npm autonomous testing
===========================

The following tests do not require a blockchain with PBTX
contract. They use the private and public keys in EOSIO text notation,
which is only used for conveninence. The PBTX protocol itself does not
depend on textual representation of the keys. "cleos" utility is part
of EOSIO software suite.

Key and signature primitives:
```
###################
# k1 key
cleos create key --to-console 
Private key: 5KgBKkXDZf6u4RrRwQARZMTNNU7E5bnKm5ELrxnqXGWVQ1DtRE7
Public key: EOS7hBPNA4ZhMJ32kFW7uSQCKuBsYFWSivfr6kGirJTLhysCKLU8Z

# pbtx.PublicKey object
./bin/pbtxdata eos2pbtxkey EOS7hBPNA4ZhMJ32kFW7uSQCKuBsYFWSivfr6kGirJTLhysCKLU8Z

12220003716875cd7ebcb45ae275f0f638f5c94132eb18a892bed1153ad72cce302afab6

# pbtx.PublicKey to EOS key conversion
./bin/pbtxdata pbtxkey2eos 12220003716875cd7ebcb45ae275f0f638f5c94132eb18a892bed1153ad72cce302afab6

PUB_K1_7hBPNA4ZhMJ32kFW7uSQCKuBsYFWSivfr6kGirJTLhysB4wYis

# sign data
./bin/pbtxdata mksig --data=0102030405060708090a0b0c0d0e0f --privkey=5KgBKkXDZf6u4RrRwQARZMTNNU7E5bnKm5ELrxnqXGWVQ1DtRE7

00207fe441d2d1215f57f87256843877d07d0d5a34a9b61d3985bc934867441c93813fb37264303895ca2614105d4296f27518dfa601f3536c62a859af27b1de75de

# verify the signatute
./bin/pbtxdata checksig --data=0102030405060708090a0b0c0d0e0f --key=12220003716875cd7ebcb45ae275f0f638f5c94132eb18a892bed1153ad72cce302afab6 --sig=00207fe441d2d1215f57f87256843877d07d0d5a34a9b61d3985bc934867441c93813fb37264303895ca2614105d4296f27518dfa601f3536c62a859af27b1de75de

Matched


###################
# r1 key
cleos create key --to-console --r1
Private key: PVT_R1_2B17RwGod27jJFMmDZdfYSKTjLsjiUvbEFLDTtDiK5rs8SBrh4
Public key: PUB_R1_4ucLsQSE3KXMqDDt1kUQodBKwLrwE8arGvWvitdxSv9n8ej2y7

# pbtx.PublicKey object
./bin/pbtxdata eos2pbtxkey PUB_R1_4ucLsQSE3KXMqDDt1kUQodBKwLrwE8arGvWvitdxSv9n8ej2y7

12220102028b54b9667baef61bf38c666140b92ea7e529d933cb57cc09ab60abc4c55330

# pbtx.PublicKey to EOS key conversion
./bin/pbtxdata pbtxkey2eos 12220102028b54b9667baef61bf38c666140b92ea7e529d933cb57cc09ab60abc4c55330

PUB_R1_4ucLsQSE3KXMqDDt1kUQodBKwLrwE8arGvWvitdxSv9n8ej2y7

# sign data
./bin/pbtxdata mksig --data=0102030405060708090a0b0c0d0e0f --privkey=PVT_R1_2B17RwGod27jJFMmDZdfYSKTjLsjiUvbEFLDTtDiK5rs8SBrh4

0120527fda9a6ab5bfa339d2d9a837b3e2f587e5b09d77cb2ef8df779d63f2a7d2075455c4fd330460e1303a06cfb70089c7613b2602dc81f59815a17b2770c47030

# verify the signatute
./bin/pbtxdata checksig --data=0102030405060708090a0b0c0d0e0f --key=12220102028b54b9667baef61bf38c666140b92ea7e529d933cb57cc09ab60abc4c55330 --sig=0120527fda9a6ab5bfa339d2d9a837b3e2f587e5b09d77cb2ef8df779d63f2a7d2075455c4fd330460e1303a06cfb70089c7613b2602dc81f59815a17b2770c47030

Matched
```


```
# Actor A: k1 key
cleos create key --to-console 
Private key: 5JUR8gUQi5w6w7oiZQpLBXPDpTabGHPDUdewWppQfpRa2KKBzan
Public key: EOS84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3qzhJSZ

./bin/pbtxdata perm '{"actor":"1", "threshold":1, "keys":[{"key":"EOS84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3qzhJSZ", "weight":1}]}'

09010000000000000010011a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d1001

# Actor B: r1 key
cleos create key --to-console --r1
Private key: PVT_R1_25sjSKMuHA8cXtA8HfH6w6cREfbS9mMEosXphDaV5fkEJkJ9GG
Public key: PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ

./bin/pbtxdata perm '{"actor":"2", "threshold":1, "keys":[{"key":"PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ", "weight":1}]}'

09020000000000000010011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab8961001

# Actor A signature

./bin/pbtxdata sign --data=0102030405060708090a0b0c0d0e0f --privkey=5JUR8gUQi5w6w7oiZQpLBXPDpTabGHPDUdewWppQfpRa2KKBzan

1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac685

# Actor B signature

./bin/pbtxdata sign --data=0102030405060708090a0b0c0d0e0f --privkey=PVT_R1_25sjSKMuHA8cXtA8HfH6w6cREfbS9mMEosXphDaV5fkEJkJ9GG

1242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e



# Validate the A's signature against A permission

./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09010000000000000010011a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d1001 --verbose --auth=1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac685

Signature #0 matched key: PUB_K1_84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3tA4T9S

# The A's signature does not match B permission

./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09010000000000000010011a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d1001 --verbose --auth=1242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e

Could not find a matching signature for actor 1

# Validate the B's signature against B permission

./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09020000000000000010011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab8961001 --verbose --auth=1242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e

Signature #0 matched key: PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ


######  multi-signature ######

# Actor C: 2 out of 3 signatures

cleos create key --to-console --r1
Private key: PVT_R1_aW8f8WeJXcpTdQMyLas74LnyxpzNZnktMxUE4MDTFURUZAwfc
Public key: PUB_R1_5keu2XapiPfFnZVBWkKyoTrsiyAHwnQux4Tbva4odyjqpvfLYJ


./bin/pbtxdata perm '{"actor":"3", "threshold":2, "keys":[{"key":"EOS84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3qzhJSZ", "weight":1},{"key":"PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ", "weight":1},{"key":"PUB_R1_5keu2XapiPfFnZVBWkKyoTrsiyAHwnQux4Tbva4odyjqpvfLYJ", "weight":1}]}'

09030000000000000010021a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d10011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab89610011a280a241222010271e79e42adaee0001bbafbd2366d84b1972fff3bbe9082bfe3ccd7517e5b87811001

# only key 1 signature

./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09030000000000000010021a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d10011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab89610011a280a241222010271e79e42adaee0001bbafbd2366d84b1972fff3bbe9082bfe3ccd7517e5b87811001 --verbose --auth=1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac685

Signature #0 matched key: PUB_K1_84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3tA4T9S
Insufficient signatures for actor 3


./bin/pbtxdata sign --data=0102030405060708090a0b0c0d0e0f --privkey=PVT_R1_25sjSKMuHA8cXtA8HfH6w6cREfbS9mMEosXphDaV5fkEJkJ9GG --privkey=5JUR8gUQi5w6w7oiZQpLBXPDpTabGHPDUdewWppQfpRa2KKBzan 


1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac6851242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e


./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09030000000000000010021a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d10011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab89610011a280a241222010271e79e42adaee0001bbafbd2366d84b1972fff3bbe9082bfe3ccd7517e5b87811001 --verbose --auth=1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac6851242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e

Signature #0 matched key: PUB_K1_84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3tA4T9S
Signature #1 matched key: PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ


./bin/pbtxdata sign --data=0102030405060708090a0b0c0d0e0f --privkey=PVT_R1_25sjSKMuHA8cXtA8HfH6w6cREfbS9mMEosXphDaV5fkEJkJ9GG --privkey=5JUR8gUQi5w6w7oiZQpLBXPDpTabGHPDUdewWppQfpRa2KKBzan 

1242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac685


./bin/pbtxdata validate --data=0102030405060708090a0b0c0d0e0f --perm=09030000000000000010021a280a2412220003a1a62f15551e5a4989abec133b404caa6a40d783b8f47e26be95f4dc48ecfc0d10011a280a24122201020b849e7b995aec840911fc25a7769c54a4e8d9e5adfd37bf0c81c79c037ab89610011a280a241222010271e79e42adaee0001bbafbd2366d84b1972fff3bbe9082bfe3ccd7517e5b87811001 --verbose --auth=1242011f199de8aa1b52583d257cbeafdb312baaaa6b381590cef4cd2d217298121986103dd709c1dcfb145e9d13cb11d894ed01cea9207d02e1162fe91f4b6e0e31656e1242002033c03b5d9be355cdabae1ebb50a1867d12529075ff9c8ba9478e4ed3e44e99545b8835a2b04ad3638002f0eed2051ff1b9c45564ed6a7e600f6c8da51c2ac685

Signature #0 matched key: PUB_R1_4yZZpHMmtR8FUUwGHT2YRPtkjgC4e9tDENT72pkWW4FwDt5UAQ
Signature #1 matched key: PUB_K1_84Re7rHTn1QNBkPekp9gbAvR5dPipsxdjfnjEjsavHM3tA4T9S

