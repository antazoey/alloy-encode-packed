# <h1 align="center"> alloy-encode-packed </h1>
**Ethereum abi.encodePacked() in Rust**

`alloy-encode-packed` is a Rust library that provides an implementation of Ethereum's `abi.encodePacked()` function. This crate is an adaptation of the [eth-encode-packed](https://github.com/roberts-pumpurs/eth-encode-packed-rs) library, replacing the `ethers.rs` dependency with `alloy`, offering improved performance and compatibility with the latest Rust ecosystem.

The library is designed to facilitate encoding of Ethereum contract data in a packed format, which is essential for certain cryptographic operations and smart contract interactions.

## Example usage


### packing an uint24
```rust
let input = vec![
    // this is supposed to be uint24 variable in solidity
    SolidityDataType::NumberWithShift(U256::from(4001), TakeLastXBytes(24))
];
let (bytes, hash) = abi::encode_packed(&input);
let hash = format!("0x{:}", hash);
let expected = "0x000fa1";
assert_eq!(hash, expected);
```

### Packing a lot of data

Solidity
```solidity
    function packer(
        uint24 uint24_data,
        uint256 tokenId,
        string calldata ipfsURI,
        address sample,
        uint256 id
    ) public pure returns (bytes memory ){
        bytes memory res = abi.encodePacked(uint24_data, tokenId, ipfsURI, sample, id);
        return res;
    }
```

Rust
```rust
let address = hex::decode("d8b934580fcE35a11B58C6D73aDeE468a2833fa8").unwrap();
let address: [u8; 20] = address.try_into().unwrap();
let input = vec![
    SolidityDataType::NumberWithShift(U256::from(3838), TakeLastXBytes(24)),
    SolidityDataType::Number(U256::from(4001)),
    SolidityDataType::String("this-is-a-sample-string"),
    SolidityDataType::Address(Address::from(address)),
    SolidityDataType::Number(U256::from(1)),
];
let (_bytes, hash) = abi::encode_packed(&input);
let hash = format!("0x{:}", hash);
let expected = "0x000efe0000000000000000000000000000000000000000000000000000000000000fa1746869732d69732d612d73616d706c652d737472696e67d8b934580fce35a11b58c6d73adee468a2833fa80000000000000000000000000000000000000000000000000000000000000001";
assert_eq!(hash, expected);
```