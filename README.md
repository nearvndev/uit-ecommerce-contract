# UIT Payment Smart contract

Application Design: [Ecommerce Payment user flow](https://drive.google.com/file/d/1ilBGG7hfkx7r6KzQy_6cEiHJqQlcSf6w/view?usp=sharing)

Prerequires
- NodeJS
- Near CLI
- Rust/Rustup and Wasm

Actions

1. Create new account in testnet
```
export CONTRACT_ID=uit-payment-contract.vbidev.testnet
export ACCOUNT_ID=vbidev.testnet
near create $CONTRACT_ID --masterAccount $ACCOUNT_ID --initialBalance 5
```

2. Build contract
```
cargo test & build.sh
```

3. Deploy and init contract
```
near deploy --wasmFile out/contract.wasm --accountId $CONTRACT_ID--initFunction new '{"owner_id": "$ACCOUNT_ID"}'
```

4. Pay order
```
near call $CONTRACT_ID pay_order '{"order_id": "order_1", "order_amount": "1000000000000000000000000"}' --accountId $ACCOUNT_ID --deposit 1
```

5. Get order

```
near view $CONTRACT_ID get_order '{"order_id": "order_1"}'
```

Ex response:
```
{
  order_id: 'order_1',
  payer_id: 'vbidev.testnet',
  amount: 1e+24,
  received_amount: 2e+24,
  is_completed: true,
  is_refund: false,
  created_at: 1661439327890786600
}
```