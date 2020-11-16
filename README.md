# wNear NEP21 Token contract

NEP21 is based on:
 
    https://github.com/near/near-sdk-rs/blob/ab5c01ca4c61a6414484b69302b84e5ce3113f2f/examples/fungible-token/src/lib.rs

The aim of the contract is to enable the wrapping of the native Ⓝ token into a NEP21 compatible token.
It's the equivalent of wrapping ETH into wETH via the WETH. This contract is based on the functionality 
of the WETH9 and WETH10 Solidity smart contracts.

## Minting wNear

The following methods are available for minting:
* `deposit(amount)`
* `deposit_to(recipient, amount)`

`deposit(amount)` just proxies through to `deposit_to(recipient, amount)` where recipient will be set to `env::predecessor_account_id()`.

When using `deposit_to`, the following requirements apply:
* Recipient cannot be the wNear contract - to stop people accidentally losing money
* Recipient needs to be a valid account Id
* Amount must be a positive integer

Both deposit methods will require an attached deposit that covers the storage requirements as well as the amount of `wNear` tokens being minted.
