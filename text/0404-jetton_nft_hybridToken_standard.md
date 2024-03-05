- **TEP**: [0](https://github.com/ton-blockchain/TEPs/pull/0) _(don't change)_
- **title**: Jetton NFT Hybrid Token Standard
- **status**: Draft
- **type**: Contract Interface
- **authors**: [Howard Peng](https://github.com/howardpen9)
- **created**: Mar 1, 2024
- **replaces**: -
- **replaced by**: -

# Summary

Hybrid Token is a standard that with a combination of fungible and non-fungible properties. It is designed to be used in the Jetton NFT ecosystem.

# Motivation

For the further community and project development, it is necessary to have a standard for the Jetton NFT Hybrid Token. This standard will help to create a more unified and efficient ecosystem for the Jetton and NFT communities and also related trading protocols for higher potential trading volume.

# Guide

The point of TEP-404 token standard is majoring focus on Jetton Token, but implement the interface that enable to interact with NFTs as well. The deployer should decide what is the "buffer(閥值)" when the NFT enable being minted when the balannce transfer of Jetton token is more than certain amount.

For example, in our example, we set the users enable to mint the 10 jetton tokens whenever they want. In the meanwhile, since the Jetton Token minted is more than the buffer value, then the new NFT will be minted as well.

On the flip side, when the user transfer NFT will make the Jetton Token balance decrease by transfering the new jetton token to others.

![Example1](https://ibb.co/5MzHTFn)
![Example2](https://ibb.co/J5B2mxH)
![Example3](https://ibb.co/XSqqSF4)

# Specification

- We add the new idea for the `series_id`, `nft_item_record`, and `nft_item_address_to_id` to implement the JettonDefaultWallet contract.
- And let the `item_index` implement at Jetton Master contract. Which make us enable to send the message to initailize the NFT item at Jetton Root contract.
- From modulality perspective, we can see that the `JettonRoot` contract is the main contract to interact with the JettonDefaultWallet contract and NFT Item contract.
- Also need the calling for `SyncTheIndex` at JettonRoot contract to sync the index of the current item_id for the NFT items.

Docs and specs are in [https://github.com/howardpen9/trc404](https://github.com/howardpen9/trc404) repo.

## Jetton NFT Hybrid Token Standard

### Get-methods

- Same as Jetton Standard(TEP-74) and NFT Standard(TEP-62).
- At JettonRoot contract, we can call the `get_next_nft_item_index` to get the next item index for the NFT item.

# TL-B schema

```
## ReportTotalSupply
TLB: `report_total_supply#ef42ff93 query_id:uint64 item_index:uint32 = ReportTotalSupply`
Signature: `ReportTotalSupply{query_id:uint64,item_index:uint32}`


## NftBurnRequest_and_Mint
TLB: `nft_burn_request_and_mint#5e74af97 query_id:uint64 item_index:uint32 original_sender:address new_owner:address = NftBurnRequest_and_Mint`
Signature: `NftBurnRequest_and_Mint{query_id:uint64,item_index:uint32,original_sender:address,new_owner:address}`


## NftCollectionInitialize
TLB: `nft_collection_initialize#4ccea562 query_id:uint64 royalty_params:RoyaltyParams{numerator:int257,denominator:int257,destination:address} collection_content:^cell = NftCollectionInitialize`
Signature: `NftCollectionInitialize{query_id:uint64,royalty_params:RoyaltyParams{numerator:int257,denominator:int257,destination:address},collection_content:^cell}`


## JettonInitialize
TLB: `jetton_initialize#bf1fd470 royalty_params:RoyaltyParams{numerator:int257,denominator:int257,destination:address} = JettonInitialize`
Signature: `JettonInitialize{royalty_params:RoyaltyParams{numerator:int257,denominator:int257,destination:address}}`

```

# Drawbacks

There is no way to get actual wallet balance onchain, because when the message with balance will arrive, wallet balance may be not actual.

# Rationale and alternatives

Distributed architecture "One wallet - one contract" well described in the [NFT standard](https://github.com/ton-blockchain/TEPs/blob/master/text/0062-nft-standard.md#rationale-and-alternatives) in paragraph "Rationale".

# Prior art

1. [TEP-74](https://github.com/ton-blockchain/TEPs/blob/master/text/0074-jettons-standard.md)
2. [TEP-62](https://github.com/ton-blockchain/TEPs/blob/master/text/0062-nft-standard.md#tl-b-schema)

# Unresolved questions

(WIP)

# Future possibilities

- Set up with FunC version of Code
- Optimize the functions

# Changelog

Mar 1, 2024: Initial version submitted

```

```
