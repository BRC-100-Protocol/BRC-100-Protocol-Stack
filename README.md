# BRC-100: An Extensible Decentralized Computing Protocol based on Ordinals Theory



**Date:** Sept. 2 2023

**Creator:** Mikael.btc

**Email:** [mikael@brc100.org](mailto:mikael@brc100.org)

**Twitter:** https://twitter.com/MikaelBTC



# Introduction

This document is intended to manage BRC-100 protocol and its extension and improvement protocols.

As we all know, Ordinals Theory, BRC-20 and other protocols based on Bitcoin have brought a lot of imagination to the development of Bitcoin ecosystem through "on-chain declaration, off-chain resolve" mechanism. And a large number of Bitcoin NFTs and tokens have been issued, but the development of decentralized applications such as DeFi is still lagging behind. This document attempts to explore a protocol that supports decentralized computing: BRC-100, and how the protocol can be extended and improved, to create a possibility for decentralized applications based on the Bitcoin network.

https://docs.ordinals.com/

https://domo-2.gitbook.io/brc-20-experiment/

The BRC-100 protocol is an extensible decentralized computing protocol based on Ordinals Theory. BRC-100 proposes a modularity method of protocols and applications: inheritance and nesting, which provides a theoretical basis for the extension of BRC-100 protocol and applications. BRC-100 protocol essentially describes a token with computing capabilities and state. The behavior of the token is an extension of BRC-20 protocol. The computing capabilities and state transition can be extended by BRC-100 extension protocol. All BRC-100 extension protocols are compatible with each other, that is, tokens that implement BRC-100 and its extension protocols can be used in all applications. At the same time, BRC-100 protocol and its extension protocols can be updated and upgraded through improvement protocols. BRC-100 protocol and all its extension and improvement protocols are called BRC-100 protocol stack.

You can find the details of BRC-100 here: https://github.com/BRC-100-Protocol/BRC-100-Protocol-Stack/blob/main/BRC-100.md.

The BRC-100 protocol is based on two models: UTXO model and state machine model, which greatly extends the computing capabilities of Bitcoin. The operation of token satisfies the UTXO model, and the computation conforms to the state machine model. And BRC-100 provides new operations: burn2/burn3 and mint2/mint3, so that token can be safely converted between UTXO model and state machine model.

BRC-100 introduces many concepts, please read the explanation below firstly.

| Term                           | Description                                                  |
| ------------------------------ | ------------------------------------------------------------ |
| BRC-100 Protocol               | An extensible decentralized computing protocol based on Ordinals Theory |
| BRC-100 Protocol Stack         | The general name for BRC-100 and its extension and improvement protocols |
| Protocol                       | A standard that describes the attributes, operations, and computing operations of the application |
| Inheritance                    | The extension protocol will inherit the properties, operations and computing operations of the parent protocol |
| BRC-100 Extension Protocols    | The protocols that directly or indirectly inherit from BRC-100 protocol |
| BRC-100 Improvement Protocols  | The protocols used to improve BRC-100 and its extension protocols |
| Governance of BRC-100 Protocol | Proposal, review, addition, modification, and deletion of BRC-100 and its extension and improvement protocols |
| Computing Operation            | The computing capability of the protocol, expressed by cop attribute |
| Application                    | An instance created after the protocol is deployed to Bitcoin network through inscriptions |
| Token                          | Application is essentially a token with computing capabilities and state |
| Nesting/Child Application      | Multiple applications can be created under one application, to complete multiple independent computing logics |
| BRC-101 Protocol               | A governance protocol that defines how to govern an application that implements BRC-100 or its extension protocol |
| Governance of Application      | The process of updating application attributes, creating child applications, and stoping application |

The BRC-100 protocol stack is open, and developers are welcome to participate in building protocols, developing applications, and jointly building the Bitcoin ecosystem. You can join the BRC-100 Developers Community: https://t.me/BRC100Developers.

Also, if you like BRC-100, you can donate to: **bc1pdkyv4vp507vrvj4x3h4pmlj2jrz235vmex9cz7flkg8mvra2jmzq50ay7c**.



## Design Principles

The BRC-100 protocol is designed based on three principles: security, extension, and consistency. The BRC-100 extension and improvement protocols must also conform to these three principles.

### 1. Security

Security is the foundation of all decentralized applications. Protocol design needs to consider two aspects: user asset security and protocol/application security, including:

• No centralized custody of user assets

• Users can fully control their own assets

• Application cannot censor users

• Computing logic of applications is open and transparent

• Application supports decentralized governance

### 2. Extension

The protocol should have great extension, and can support the logic of currently known decentralized applications and possible future innovations. BRC-100 protocol achieves extension and modularity through the support for inheritance and nesting. Protocol can inherit from BRC-100 or its extension protocol to extend protocol’s computing capabilities. Applications deployed based on BRC-100 and its extension protocol can create child application to utilize the computing capabilities of the child application, to implement the modularity of building application.

### 3. Consistency

The protocol must meet the consistency requirements, and any indexer can compute a completely consistent state based on the inscriptions on Bitcoin and the computing logic of the protocol. The BRC-100 protocol consists of three parts: attribute, operation and computing operation. The operation represents token operation, which is based on the UTXO model and cannot be extended, which ensures the compatibility and consistency of tokens for all extension protocols. The computing operation part is expressed using a state machine model, which requires the BRC-100 extension protocols to have the rigorous and unambiguous description of the computing logic to ensure the consistency of indexer.



## Concepts



This chapter will define and explain some concepts in the BRC-100 protocol to help developers to understand better.

### 1. Protocol and Application

In the BRC-100 protocol stack, the protocol is a standard that describes the attributes, operations, and computing operations of the application. The application is an instance created after the protocol is deployed to the Bitcoin network through inscriptions. The application is essentially a token with computing capabilities and state. The computing capabilities of an application are described very detail in the protocol. Without adding child applications, the application cannot have computing capabilities not described in the protocol. The added child applications can also only have the computing capabilities of the protocol, otherwise the public indexer cannot verify the state of the application, resulting in state inconsistency of user and application.

### 2. Protocol Inheritance

The BRC-100 protocol introduces the concept of inheritance. The protocols that directly or indirectly inherit from BRC-100 are called BRC-100 extension protocols. BRC-100 extension protocols must inherit from only one protocol. The extension protocol will inherit the properties, operations and computing operations of the parent protocol, and can only extend the properties and computing operations. All tokens/applications that implement BRC-100 and its extension protocols are compatible with each other, which means that a token/application can be used in any other application/token or child application/token.

### 3. Application Nesting

Applications deployed based on BRC-100 and its extension protocols can be nested, that is, another application can be created under one application, which is called child application. The ticker of the child application starts with "parent application ticker:", and multiple applications can be created under one application, to complete multiple independent computing logics. For example, in the classic AMM DEX scenario, multiple LP child applications/tokens need to be created in one DEX application.

### 4. State of Application and Address

Besides the UTXO model, the BRC-100 protocol also introduces the state machine model to extend the computing capabilities of the protocol. Applications, child applications and addresses can all have states. For example, an application can hold tokens, and the address can have a balance in the application. The conversion of UTXO and state is completed through the operators: burn2/burn3 and mint2/mint3. The computing operation(cop) is used to represent specific computing logic, that is, the transition logic of application and address state. For example, address A burn 10 token1 to the application through the burn3 inscription. At this time, the application owns this UTXO and 10 token1. The application can allocate these 10 token1 by changing the internal state of any address or application by its computing logic. Then the address or application who has token1 in the application can mint it through the mint3 operator.

### 5. Protocol Parameters

When defining BRC-100 and its extension protocols, two parameters need to be defined: extends and openAsChild. The first one represents which protocol is inherited from, and the other represents whether all users can deploy the protocol as a child application. These two parameters are designed when defining the protocol and do not need to be set when deploying the application. For example, AMM DEX's LP Protocol, extends: BRC-100, openAsChild: true.

### 6. Privileges

The BRC-100 protocol introduces two kinds of roles: owner and admin. The address with the application deployment inscription is called owner. The owner can follow the UTXO transfer of the deployment inscription. The owner of all child applications is the owner of the parent application. The admin is managed by the owner, and the admin cannot manage the admin. The privileges of the owner and the admin are strictly limited. They cannot censor users and can only do:  govern applications that have not started DAO, complete the computing operation of mint2/burn2. Admin can be an address or an application or a child application. An application and its child applications are each other's admin by default, no additional settings are required, but child applications are not admins of each other. The inscriptions of burn2/burn3 need to be sent to the owner of the application in order to be processed correctly.

The part of token needed to be mint by "mint2" can only be allocated by the application/child application logic, and the application/child application need to be the admin of the token, also "burn2" operator has similar logic. The inscriptions of burn2/burn3 need to be sent to the owner of the application in order to be processed correctly according to the logic of the computing operation.

### 7. Decentralized Governance of Application

The BRC-100 protocol stack introduces a governance protocol: BRC-101, which can govern applications that implement BRC-100 or its extension protocol standard. And after the application starts DAO, governance needs to be completed through decentralized voting. The governance of application includes: update the attributes of application and child applications, create child applications, and stop application. Application governance is on-chain governance. After the voting on-chain is passed, the application should be notified through the computing operation: egov, then the application will automatically execute governance after the time lock.

### 8. Deploy Application/Token

In the BRC-100 protocol, there are two ways to deploy application: one is to deploy directly using the deploy operator, and the other is to deploy through the governance protocol: BRC-101. The first one is used to deploy parent applications and child applications configured not to require governance, and the other is used to deploy child applications that require governance.

### 9. Mint Token

BRC-100 protocol provides three mint operators: mint, mint2, and mint3, which are used to mint token in different scenarios. When deploying applications, you need to set the number of tokens that can mint by public (using operator: "mint"). The remaining tokens will use operator: "mint" to mint.

• mint: Mint from Public, public mint, anyone can mint tokens to users, but the total number mint by "mint" operator cannot exceed the settings of the max and mma attributes of the application. After mint the circulation supply of token will be increased.

• mint2: Mint from Whitelist, the application records the number of users or applications that can mint, anyone can mint2 tokens to users or applications under the application rules. After mint2 the circulation supply of token will also be increased.

• mint3: Mint from State, mint3 the balance of users or applications in other applications, anyone can mint3 tokens to users or applications under the application rules. After mint3 the circulation supply of token will not be increased.

### 10. Burn Token

The burn is a newly introduced operation by the BRC-100 protocol. The user can inscribe the inscription of the burn operation and then transfer the inscription to the owner of the application, which is similar to the semantics of the transfer operation. Then the inscribed token will be burned or transferred to the balance of the application. Similar to the definition of mint operation, there are three burn operators: burn, burn2, and burn3, which correspond logically to mint, mint2, and mint3 respectively. No extra configuration is required, all applications/tokens support these three burn operators.

• burn: Burn to Public, everyone can use the operator to burn token. After the token is burned, the circulation supply will be reduced, and the burned token cannot be minted again.

• burn2: Burn to Whitelist, according to the application's preset rules, after burn2 token to application, the user's balance will be reduced, the state of the application will also be updated accordingly, the circulation supply will be reduced. In practice, the logic such as remove liquidity in AMM DEX can be realized by burn2.

• burn3: Burn to State, burn3 will reduce the user’s token balance and increase the balance of "to" application. In practice, it can be used with mint3 to complete swap token, add liquidity and other logic in AMM DEX.

### 11. Trading Tax and Deflation

The BRC-100 protocol introduces a new token trading mechanism: trading tax and deflation. Applications can set the trading tax percentage, tax receiver and trading black hole percentage. These settings only take effect when trading in decentralized exchanges based on AMA. Normal transfer, mint and burn operations will not trigger trading tax and deflation.

### 12. Computing Operation

The computing operation is the extended computing behavior of the BRC-100 protocol. It is expressed by cop attribute and is the smallest unit of the protocol computing capability. When used with the op operator: burn2/burn3/mint2/mint3, it can be understood as a state transition function, which defines how the state of the application and user can be updated under the corresponding op operator.



# Governance of BRC-100 Protocol

First of all, BRC-100 is an open protocol that provides a framework for future protocol to extend to facilitate the development of Bitcoin ecosystem. Then, the development of the BRC-100 protocol requires the joint efforts of more developers. In the future, the BRC-100 protocol will complete governance in a more transparent and decentralized manner, to complete the processes such as proposal, review, addition, modification, and deletion of BRC-100 protocol and its extension and improvement protocols. The governance details are being formulated.

The current editor of the BRC-100 protocol is: Mikael.btc. If you want to become a new editor or have other suggestions, you can send an email to: [mikael@brc100.org](mailto:mikael@brc100.org), or you can contact Mikael.btc on Twitter: https://twitter.com/MikaelBTC.



# BRC-100 Extension Protocols

This chapter defines the BRC-100 extension protocols, including various DeFi and other protocols in the future.

## 1. BRC-101

BRC-101 is a governance protocol that defines how to govern an application that implements BRC-100 or its extension protocol and will be released soon.



# BRC-100 Improvement Protocols

This chapter defines the BRC-100 improvement protocols, which is used to improve the BRC-100 and its extension protocols, such as adding new computing operators, adding new attributes to the BRC-100 protocol, etc.



# BRC-100 Protocol Indexer

The indexer of BRC-100 protocol is an index implemented based on BRC-100 protocol and its extension and improvement protocols. In order to ensure security, we hope that more indexers can support the BRC-100 protocol stack. In the future, there will be a set of indexer behavior specifications to guide the behavior of the indexer. And the results of the indexer can be verified to ensure the consistency of user and application state, to ensure the security of user assets.

Considering the complexity and subsequent extension of the BRC-100 protocol, we are exploring a way to implement the minimal index. The demander can deploy his own minimal index to get the state of all the assets of BRC-100 protocol stack without realizing the complex computing logic of all the extension protocols. Also, the minimal index does not need to be updated or upgraded frequently.



# Developers

Developers are important role of the BRC-100 protocol. The purpose of the design of the BRC-100 protocol is to have more developers to develop decentralized applications based on the Bitcoin network. If a developer wants to develop a decentralized application based on BRC-100 protocol stack, he should first design the relevant protocol to extend BRC-100 or its extension protocol, make the protocol public and obtain indexer support, and then develop the application following the new protocol.

Welcome developers to develop decentralized applications based on the BRC-100 protocol stack. The development of the Bitcoin network is driven by you. If you have any questions, you can ask in the BRC-100 Developers Community: https://t.me/BRC100Developers.



# Donate

Of course, if you feel that the BRC-100 protocol has inspired or helped you, or you have seen and recognized our efforts to develop Bitcoin ecosystem, you can donate to: **bc1pdkyv4vp507vrvj4x3h4pmlj2jrz235vmex9cz7flkg8mvra2jmzq50ay7c**.
