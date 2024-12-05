# <h1 align="center"> alloy-encode-packed </h1>
**Ethereum abi.encodePacked() in Rust**

`alloy-encode-packed` is a Rust library that provides an implementation of Ethereum's `abi.encodePacked()` function. This crate is an adaptation of the [eth-encode-packed](https://github.com/roberts-pumpurs/eth-encode-packed-rs) library, replacing the `ethers.rs` dependency with `alloy`, offering improved performance and compatibility with the latest Rust ecosystem.

The library is designed to facilitate encoding of Ethereum contract data in a packed format, which is essential for certain cryptographic operations and smart contract interactions.
