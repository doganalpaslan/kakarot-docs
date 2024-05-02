---
sidebar_position: 3
---

# Differences between Kakarot and Ethereum

Although Kakarot is Ethereum-compatible and aims to support the latest features
of Ethereum (e.g.
[Cancun new opcodes](https://blog.ethereum.org/2024/01/10/goerli-dencun-announcement)),
it still has some edge case behaviors. They are listed below:

| Item                   | Ethereum                                                     | Kakarot                                                                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BLOCKHASH              | Get the hash of one of the 256 most recent complete blocks   | The last 10 blocks are not available, and 0 is returned instead                                                                                                                                                |
| BLOBBASEFEE            | Get the current data-blob base-fee                           | Return 0 as there are no blobs on Kakarot                                                                                                                                                                      |
| BLOBHASH               | Get blob versioned hashes at index                           | Return 0 as there are no blobs on Kakarot                                                                                                                                                                      |
| Block hash computation | keccak256(RLP.encode(Block Header))                          | [pedersen(Starknet Block Header)](https://docs.starknet.io/documentation/architecture_and_concepts/Network_Architecture/header/)                                                                               |
| State root computation | Root of state keccak-MPT                                     | [poseidon(root of contract pedersen-MPT, root of contract class pedersen-MPT)](https://docs.starknet.io/documentation/architecture_and_concepts/Network_Architecture/starknet-state/)                          |
| Transaction receipt    | Transaction receipt is available once a transaction is mined | Transaction receipt is available once a transaction is processed and guaranteed to be mined. This means that blockhash field of the receipt is optional and will be non-null only once the transaction is mined. |
| RIP-7212 Support   | Kakarot Supports native P256 verification. | P256 is a wildly used curve and it is and supported in many modern devices such as Apple’s Secure Enclave, Webauthn, Android Keychain which can be used in many use cases. |
