# Terminology
The following terms are used to describe concepts in this specification.

|Terms|Terminology|
|-----|-----------|
| _Blockchain_ | The Dimecoin blockchain is the transaction database that is extended by nodes participating in the [mining](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#mining) and [minting](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#staker) process on the Dimecoin network. The blockchain contains [transactions](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#transaction) validated and processed by nodes on the network. Using the blockchain, anyone can add and verify a record of all of the [confirmed](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#confirmations) transactions that have taken place on the ledger up until the most recent block was found. ([DIME Blockchain, UTXO](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#blockchain)) |
| _Blockchain Transactions_ | A Dimecoin transaction consists of a version number, a lock time value, a list of inputs and a list of outputs. The primary functionality of a Dimecoin transaction is to transfer custody of dimecoin from one person to another. A transaction uses [UTXOs](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#unspent-transaction-output) as inputs and distributes their value to new outputs. UTXOs are the 'coins' in which all dimecoins are stored. ([DIME Database, Dimecoin Transactions](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#transaction)) |
| _Chain of Dust_ | In Dimecoin (DIME), a "Chain of Dust" refers to a sequence of minimum required value transactions that are created by spending small amounts of Dimes. This concept is related to "dust" in the cryptocurrency context. These are small blockchain transactions where one dust transaction leads to another. Each subsequent transaction in the chain is dependent on the previous one, creating a linked sequence. ([DIME Database, UTXO](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#unspent-transaction-output)) |
| _Decentralised identifier_ | A globally unique persistent identifier that does not require a centralized registration authority and is often generated and/or registered cryptographically. The generic format of a DID is defined in [3.1 DID Syntax](https://www.w3.org/TR/did-core/#did-syntax). A specific [DID scheme](https://www.w3.org/TR/did-core/#dfn-did-schemes) is defined in a [DID method](https://www.w3.org/TR/did-core/#dfn-did-methods) specification. Many—but not all—DID methods make use of [distributed ledger technology (DLT)](https://www.w3.org/TR/did-core/#dfn-distributed-ledger-technology) or some other form of decentralized network. ([W3C. DIDs v1.0, 2022](https://www.w3.org/TR/did-core/#dfn-did-documents))|
| _DID Controller_ | An entity that has the capability to make changes to a [DID Document](https://www.w3.org/TR/did-core/#dfn-did-documents). A [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) might have more than one DID controller. The DID controller(s) can be denoted by the optional controller property at the top level of the [DID Document](https://www.w3.org/TR/did-core/#dfn-did-documents). Note that a DID controller might be the [DID Subject](https://www.w3.org/TR/did-core/#dfn-did-subjects). ([W3C, DID V.1.0,2022](https://www.w3.org/TR/did-core/#dfn-did-controllers)) |
| _DID Document_ | A set of data describing the [DID Subject](https://www.w3.org/TR/did-core/#dfn-did-subjects), including mechanisms, such as cryptographic public keys, that the [DID Subject](https://www.w3.org/TR/did-core/#dfn-did-subjects) or a [DID delegate](https://www.w3.org/TR/did-core/#dfn-did-delegate) can use to [authenticate](https://www.w3.org/TR/did-core/#dfn-authenticated) itself and prove its association with the [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers). A DID Document might have one or more different [representations](https://www.w3.org/TR/did-core/#dfn-representations). ([W3C, DID V.1.0,2022](https://www.w3.org/TR/did-core/#dfn-did-controllers)) |
| _DID Issuer_ | An individual or entity that issued a DID. This term is specific to this document. | 
| _DID Manager_ | In this document we call DID manager to a package that includes the DID resolver and DID controller. DID Manager term is specific to nChain implementation.| 
| _DID Resolver_ | A [DID resolver](https://www.w3.org/TR/did-core/#dfn-did-resolvers) is a software and/or hardware component that performs the [DID resolution](https://www.w3.org/TR/did-core/#dfn-did-resolution) function by taking a [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) as input and producing a conforming [DID Document](https://www.w3.org/TR/did-core/#dfn-did-documents) as output. ([W3C, DID V.1.0,2022](https://www.w3.org/TR/did-core/)) |
| _DID Subject_ | The entity identified by a [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) and described by a [DID Document](https://www.w3.org/TR/did-core/#dfn-did-documents). Anything can be a DID Subject: person, group, organization, physical object, digital thing, logical thing, etc. ([W3C,DID V.1.0, 2022, Section 5.1.1](https://www.w3.org/TR/did-core/#dfn-did-documents)) |
| _Ledger_ | In this document, the ledger is distinguished from the blockchain. The Dimecoin ledger refers to information store that [keeps records (3.81)](https://www.iso.org/obp/ui/en/#iso:std:iso:22739:ed-2:v1:en:term:3.81) of [transactions (3.93](https://www.iso.org/obp/ui/en/#iso:std:iso:22739:ed-2:v1:en:term:3.93) that are intended to be final, definitive and [immutable (3.51)](https://www.iso.org/obp/ui/en/#iso:std:iso:22739:ed-2:v1:en:term:3.51). Unlike the blockchain, which is a chain of blocks verified by miners, the ledger specifically focuses on the individual transactions. ([SO22739-2024](https://www.iso.org/obp/ui/en/#iso:std:iso:22739:ed-2:v1:en)) |
| _UTXO_ | UTXO is an acronym for unspent transaction output. Every [Dimecoin transaction](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#transaction) in every [block](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#block) contains at least one [output](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#output). Outputs are then spent by inputs of later blockchain transactions and typically must be unlocked with a [digital signature](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#ecdsa-signatures) (most commonly [ECDSA](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#ecdsa-private-key) in Dimecoin). Until an output is used as an [input](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#input) in another transaction, this output is called a UTXO. ([DIME Database, UTXO](https://dimecore-docs.dimecoinnetwork.com/en/latest/docs/reference/glossary.html#unspent-transaction-output)) |
| _Verifiable data registry_ | In order to be resolvable to [DID Documents](https://www.w3.org/TR/did-core/#dfn-did-documents), [DIDs](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) are typically recorded on an underlying system or network of some kind. Regardless of the specific technology used, any such system that supports recording [DIDs](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) and returning data necessary to produce [DID Documents](https://www.w3.org/TR/did-core/#dfn-did-documents) is called a [verifiable data registry](https://www.w3.org/TR/did-core/#dfn-verifiable-data-registry). Examples include [distributed ledgers](https://www.w3.org/TR/did-core/#dfn-distributed-ledger-technology), decentralized file systems, databases of any kind, peer-to-peer networks, and other forms of trusted data storage. ([W3C, DID V.1.0,2022](https://www.w3.org/TR/vc-data-model-2.0/#dfn-verifiable-data-registries)) | 
| _Verifiers_ | In this document, a verifier refers to an entity, organization, or individual that checks the status of the DID and verifies that the signature of the subject or DID controller matches the signatures in the presentation. ([W3C, DID V.1.0,2022](https://www.w3.org/TR/vc-data-model-2.0/#dfn-verifier)) | 















