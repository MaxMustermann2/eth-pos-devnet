# Devnet with ETH PoS

## Start

```bash
docker compose up -d
```

## Validator public key, signature and data root

Sent using private key `0x47c99abed3324a2707c28affff1267e45918ec8c3f20b8aa892e8b065d2942dd` and mnemonic `margin tank lunch prison top episode peanut approve dish seat nominee illness`. The private key affects the execution address calculation, which is made using CREATE2, while the mnemonic affects the validator BLS12-381 public key.

```bash
# https://github.com/MaxMustermann2/staking-deposit-cli
export PYTHONPATH=.
./deposit.sh --non_interactive existing-mnemonic --num_validators=1 --validator_start_index=0 --chain=custom --execution_address=0x468c15d616B52FCEf0B932BF89D42157984BE2A5
```

Then, include the contents of the file into the integration script

```bash
cat $(ls -t validator_keys/deposit_data* | head -1) | jq
```

We will use the values `pubkey`, `signature` and `deposit_message_root`.

```json
[
  {
    "pubkey": "98db81971df910a5d46314d21320f897060d76fdf137d22f0eb91a8693a4767d2a22730a3aaa955f07d13ad604f968e9",
    "withdrawal_credentials": "010000000000000000000000468c15d616b52fcef0b932bf89d42157984be2a5",
    "amount": 32000000000,
    "signature": "a20d736d6807720cb2a2f48526eb3df83162b387b806bdf7d0d08bb31d3d4e4daaf4a11120dc194b188035e9e5c9bdbf00c3be3ca68adec9c4fb2fb59d936337b750ae08a9e7add56fb82526792876066456010a64c5629b7f1f564f9923ff8e",
    "deposit_message_root": "2304faca7c177b307c224757df6e8a955026c613c86045ea569ba5547f8d104c",
    "deposit_data_root": "e6260302845906138ebe075e9977e6086f02fc1c5142590bebdf54579c806bd3",
    "fork_version": "20000089",
    "network_name": "custom",
    "deposit_cli_version": "2.7.0"
  }
]
```
