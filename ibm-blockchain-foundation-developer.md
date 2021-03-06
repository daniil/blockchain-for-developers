# IBM Blockchain Foundation Developer

## What is Blockchain

Blockchain transactions and ledgers are different. Blockchain introduces a new kind of transaction – a multiparty transaction - that is signed by everyone involved in the transaction. Blockchain ledgers are different too; the same ledger is replicated in every organization in the network, and kept synchronized using a process called *consensus*. Moreover, these ledgers are *immutable* and *final*; once a multi-party transaction is written to the ledger, it cannot be reversed.

Blockchain introduces the idea of a *smart contract*. It describes in code what a transaction generated by the smart contract looks like. For example, a car contract might use logic to check that you're the current owner of the car, and that a purchaser has the required funds. 

### Blockchain for business

Businesses  are required to carry out **Know Your Customer (KYC)** and **Anti-Money Laundering (AML)** checks, which require businesses to know who they are dealing with. This means that business blockchains require identifiable participants and favor features such as *privacy* and *confidentiality*.

### Hyperledger Fabric

A Hyperledger Fabric network consists of three key types of components:

- **Peer node**: holds a copy of the ledger and is responsible for running smart contracts.
- **Orderer node**: part of a distributed ordering service that agrees the order that transactions are added to the ledger.
- **Certificate Authority**: responsible for issuing the certificates that identify users and organizations on the network.

In Hyperledger Fabric, a smart contract uses a *state* database containing the current value of all business objects in the ledger to simplify transaction generation. Each smart contract can run on a set of peers in each organization.

### Smart contract determinism

Whilst it may look like it, the effect of `context.putState` is not immediate. The business object identified by myAssetId will only be updated when every organization in the network agrees with the generated transaction response. This requires the consensus process to complete across the network. We need to ensure that our smart contract transactions are *deterministic*; that is, each must always generate the same transaction response for a given set of transaction inputs. 

### Fabric Environment

- **Channels** define the scope of each network, and form one method of choosing how organizations share data. Deployed smart contracts that are available to the network will show under channels. We will look at channels in a later tutorial.
- **Nodes** are the Hyperledger Fabric components that make the system work. There are three types of nodes:
  - Peers which host ledgers and execute smart contracts
  - Orderers which assert transaction order and distribute blocks to peers
  - Certificate authorities which provide the means of identifying users and organizations on the network
- **Organizations** are the members of the blockchain network. Each organization will consist of many different users and types of users.

### Identities, wallets and gateways

The resources that you can access in a Hyperledger Fabric network are determined according to your identity; that's why its called a permissioned blockchain. Your identity is typically represented by an X.509 certificate issued by your organization, and stored in your wallet. Once you have an identity and a wallet, you can create a gateway that allows you to submit transactions to a network.

A gateway represents a connection to a set of Hyperledger Fabric networks. If you want to submit a transaction, whether using VS Code or your own application, a gateway makes it easy to interact with a network: you configure a gateway, connect to it with an identity from your wallet, choose a particular network, and start submitting transactions using a smart contract that has been deployed in that network.

A gateway is configured using a connection profile, which identifies a single peer in the network as an initial connection point. 

The difference between Fabric Environments and Fabric Gateways: an environment gives an overview of all the resources available to you in a Hyperledger Fabric network; a gateway provides an access point to those resources.

### Hyperledger Fabric Transactions

Hyperledger Fabric can generate two different kinds of transactions:

- *Submitted* transactions are recorded on the blockchain ledger.  These are used when you want to update the current value of the ledger. Submitted transactions go through the full consensus process before they are recorded on the ledger. It is possible to submit read-only ledger transactions, but it's less common.

- *Evaluated* transactions are not recorded on the blockchain ledger. These transactions are typically used when you want to simply query the current value of the ledger. Evaluated transactions do not go through the consensus process; they are run on a single peer, and the result is returned to the caller. It is possible to evaluate read-write transactions, but it's less common. 