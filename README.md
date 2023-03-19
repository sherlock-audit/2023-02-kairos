
# Kairos Loan contest details

- Join [Sherlock Discord](https://discord.gg/MABEWyASkp)
- Submit findings using the issue page in your private contest repo (label issues as med or high)
- [Read for more details](https://docs.sherlock.xyz/audits/watsons)

# Resources

- [kairos book](https://doc.kairos.loan): in depth description of the protocol mechanisms and goals. It contains protocol specifications, it is a necessary read.

# On-chain context

Kairos is meant to interact with ERC721s as NFT collaterals and ERC20s as fungible lent funds. Kairos is permissionless when it comes to which ERC721s and which ERC20s can be used in the protocol, considering it is the responsibility of the lenders and borrowers not to interact with non-compliant implementations of those standards, and does not guarantee to function correctly if used with those non-compliant implementations.  

The owner/administrator/governance of kairos is the account that has the power to upgrade the protocol and call the `onlyOnwer` methods and is considered trusted.

```list
DEPLOYMENT: any EVM
ERC20: any
ERC721: any
ERC777: none
FEE-ON-TRANSFER: none
REBASING TOKENS: none
ADMIN: owner() - Trusted
EXTERNAL-ADMINS: none
```

### Q: Are there any additional protocol roles? If yes, please explain in detail:
1) The roles
2) The actions those roles can take 
3) Outcomes that are expected from those roles 
4) Specific actions/outcomes NOT intended to be possible for those roles

A: There is no extra access-control role other than the admin. Actors interacting with kairos are described in the [book](https://doc.kairos.loan).

___
### Q: Is the code/contract expected to comply with any EIPs? Are there specific assumptions around adhering to those EIPs that Watsons should be aware of?
A: The Kairos contract is an ERC721. The Kairos NFTs represent lending positions in the protocol and give access to claiming interests and shares of liquidation proceeds. Lending is done through signing EIP712 messages. The typed data signed has the format of [`Offer` structs](kairos-contracts/src/DataStructure/Objects.sol).

___

### Q: Please list any known issues/acceptable risks that should not result in a valid finding.
A: Borrowers can effectively lock lenders funds by spaming the minting of supply positions on ERC20s where the governance has not set a `minOfferCost` or an `offerBorrowAmountLowerBound` at sufficient values.

____
### Q: Please provide links to previous audits (if any).
A: This is the first audit.

___

### Q: Are there any off-chain mechanisms or off-chain procedures for the protocol (keeper bots, input validation expectations, etc)? 
A: Loan offer signatures are kept in an offchain API. This API being offline or corrupted should only disturb the ability of one to take a new loan due to the inability to find those signatures.
_____

### Q: In case of external protocol integrations, are the risks of an external protocol pausing or executing an emergency withdrawal acceptable? If not, Watsons will submit issues related to these situations that can harm your protocol's functionality. 
A: Kairos does not integrate another protocol.


# Audit scope


[kairos-contracts @ b2fd98d62cf0f25ee1db2bd551cd7b4606a5a988](https://github.com/kairos-loan/kairos-contracts/tree/b2fd98d62cf0f25ee1db2bd551cd7b4606a5a988)
- [kairos-contracts/src/AdminFacet.sol](kairos-contracts/src/AdminFacet.sol)
- [kairos-contracts/src/AuctionFacet.sol](kairos-contracts/src/AuctionFacet.sol)
- [kairos-contracts/src/BorrowFacet.sol](kairos-contracts/src/BorrowFacet.sol)
- [kairos-contracts/src/BorrowLogic/BorrowCheckers.sol](kairos-contracts/src/BorrowLogic/BorrowCheckers.sol)
- [kairos-contracts/src/BorrowLogic/BorrowHandlers.sol](kairos-contracts/src/BorrowLogic/BorrowHandlers.sol)
- [kairos-contracts/src/ClaimFacet.sol](kairos-contracts/src/ClaimFacet.sol)
- [kairos-contracts/src/DataStructure/Errors.sol](kairos-contracts/src/DataStructure/Errors.sol)
- [kairos-contracts/src/DataStructure/Global.sol](kairos-contracts/src/DataStructure/Global.sol)
- [kairos-contracts/src/DataStructure/Objects.sol](kairos-contracts/src/DataStructure/Objects.sol)
- [kairos-contracts/src/DataStructure/Storage.sol](kairos-contracts/src/DataStructure/Storage.sol)
- [kairos-contracts/src/Initializer.sol](kairos-contracts/src/Initializer.sol)
- [kairos-contracts/src/ProtocolFacet.sol](kairos-contracts/src/ProtocolFacet.sol)
- [kairos-contracts/src/RepayFacet.sol](kairos-contracts/src/RepayFacet.sol)
- [kairos-contracts/src/Signature.sol](kairos-contracts/src/Signature.sol)
- [kairos-contracts/src/SupplyPositionFacet.sol](kairos-contracts/src/SupplyPositionFacet.sol)
- [kairos-contracts/src/utils/RayMath.sol](kairos-contracts/src/utils/RayMath.sol)
- [kairos-contracts/src/utils/Erc20CheckedTransfer.sol](kairos-contracts/src/utils/Erc20CheckedTransfer.sol)
- [kairos-contracts/src/utils/NFTokenUtils.sol](kairos-contracts/src/utils/NFTokenUtils.sol)
- [kairos-contracts/src/SupplyPositionLogic/SafeMint.sol](kairos-contracts/src/SupplyPositionLogic/SafeMint.sol)



# About Kairos Loan

Kairos loan is an NFT-as-collateral lending protocol. It manages deals between lenders and borrowers in a P2P fashion.  
Thank you for laying eyes on our code, please reach out to tobou.eth 🦅  CTO kairos-loan#4370 on the sherlock discord for any question.
