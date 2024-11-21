# DID:DIME Method Specification: A UTXO Based Model

November 21 2024 - Unofficial Draft v.0.1

**Authors**

- Douglas Hopping

**Contributors**

- NA

**Reviewers**

- NA
- NA

**Feedback**

- Issues: <https://github.com/dime-coin/dimedid-method/issues>

## Contents

- [ABSTRACT](https://github.com/dime-coin/dimedid-method/blob/main/README.md#1-abstract)
- [INTRODUCTION](https://github.com/dime-coin/dimedid-method/blob/main/README.md#2-introduction)
  - [Purpose](https://github.com/dime-coin/dimedid-method/blob/main/README.md#21-purpose)
  - [Intended Audience](https://github.com/dime-coin/dimedid-method/blob/main/README.md#22-intended-audience)
  - [Scope](https://github.com/dime-coin/dimedid-method/blob/main/README.md#23-scope)
  - [Compliance](https://github.com/dime-coin/dimedid-method/blob/main/README.md#24-compliance)
  - [Terminology](https://github.com/dime-coin/dimedid-method/blob/main/README.md#25-terminology)
- [SPECIFICATION OVERVIEW](https://github.com/dime-coin/dimedid-method/blob/main/README.md#3-specification-overview)
  - [Prerequisites](https://github.com/dime-coin/dimedid-method/blob/main/README.md#31-prerequisites)
  - [UTXO DID Method](https://github.com/dime-coin/dimedid-method/blob/main/README.md#32-utxo-did-method)
    - [The DID](https://github.com/dime-coin/dimedid-method/blob/main/README.md#33-did-controller-and-did-resolver)
    - [DID Document](https://github.com/dime-coin/dimedid-method/blob/main/README.md#322-the-did-document)
    - [DID Document Data Model](https://github.com/dime-coin/dimedid-method/blob/main/README.md#3221-the-did-document-data-model)
  - [DID Controller and DID Resolver](https://github.com/dime-coin/dimedid-method/blob/main/README.md#33-did-controller-and-did-resolver)
    - [DID Controller](https://github.com/dime-coin/dimedid-method/blob/main/README.md#331-did-controller)
    - [DID Resolver](https://github.com/dime-coin/dimedid-method/blob/main/README.md#332-did-resolver)
  - [DID CRUD Operations](https://github.com/dime-coin/dimedid-method/blob/main/README.md#34-did-operations)
    - [Create](https://github.com/dime-coin/dimedid-method/blob/main/README.md#341-create)
    - [Resolve](https://github.com/dime-coin/dimedid-method/blob/main/README.md#342-resolve)
    - [Update](https://github.com/dime-coin/dimedid-method/blob/main/README.md#343-update)
    - [Destroy](https://github.com/dime-coin/dimedid-method/blob/main/README.md#344-destroy)
    - [DID Document Data Modal](https://github.com/dime-coin/dimedid-method/blob/main/README.md#3221-the-did-document-data-model)
- [GOVERNANCE MODEL USING DID DIME METHOD](https://github.com/dime-coin/dimedid-method/blob/main/README.md#4-governance-model-using-did-dime-method)
- [LOW LATENCY DID RESOLUTION](https://github.com/dime-coin/dimedid-method/blob/main/README.md#4-governance-model-using-did-dime-method)
  - [Timing and Latency in DID Resolution Processes](https://github.com/dime-coin/dimedid-method/blob/main/README.md#timing-and-latency-in-did-resolution-processes)
  - [User-Controlled Security through Miner Block Validation](https://github.com/dime-coin/dimedid-method/blob/main/README.md#user-controlled-security-through-miner-block-validation)
- [DATA REGISTER ANALYSIS](https://github.com/dime-coin/dimedid-method/blob/main/README.md#6-data-register-analysis)
  - [Distributed Ledger Technology](https://github.com/dime-coin/dimedid-method/blob/main/README.md#61-distributed-ledger-technology)
  - [Why use Dimecoin? Ledger Comparison Analysis](https://github.com/dime-coin/dimedid-method/blob/main/README.md#62-why-not-others-ledger-comparison-analysis)
- [PRIVACY CONSIDERATIONS](https://github.com/dime-coin/dimedid-method/blob/main/README.md#7-privacy-considerations)
- [UTXO DID METHOD NORMATIVE REFERENCE](https://github.com/dime-coin/dimedid-method/blob/main/README.md#8-utxo-did-method-normative-reference)
  - [DID Syntax](https://github.com/dime-coin/dimedid-method/blob/main/README.md#81-did-syntax)
  - [Verifiable Data Registry](https://github.com/dime-coin/dimedid-method/blob/main/README.md#82-verifiable-data-registry)
    - [DID Issuance Transaction](https://github.com/dime-coin/dimedid-method/blob/main/README.md#821-did-issuance-transaction)
    - [DID Document Transaction](https://github.com/dime-coin/dimedid-method/blob/main/README.md#822-did-document-transaction)
    - [DID Destroy Transaction](https://github.com/dime-coin/dimedid-method/blob/main/README.md#823-did-destroy-transaction)
    - [DID Funding Transaction](https://github.com/dime-coin/dimedid-method/blob/main/README.md#824-did-funding-transaction)
    - [Example of DID Transaction Chain](https://github.com/dime-coin/dimedid-method/blob/main/README.md#825-example-of-did-transaction-chain)
  - [DID Operations](https://github.com/dime-coin/dimedid-method/blob/main/README.md#83-did-operations)
    - [DID Creation](https://github.com/dime-coin/dimedid-method/blob/main/README.md#831-did-creation)
    - [DID Document Update](https://github.com/dime-coin/dimedid-method/blob/main/README.md#832-did-document-updates)
    - [DID Deactivation](https://github.com/dime-coin/dimedid-method/blob/main/README.md#833-did-deactivation)
    - [DID Resolution](https://github.com/dime-coin/dimedid-method/blob/main/README.md#834-did-resolution)
- [REFERENCES AND CREDITS](https://github.com/dime-coin/dimedid-method/blob/main/README.md#834-did-resolution)

---

# DID:DIME Method Specification: UTXO Model

## 1. Abstract

This document outlines a method for the issuance, updates, key rotation, and destruction of Decentralized Identifiers (DIDs) using Dimecoin's public, UTXO-based blockchain as a data registry. The did:dime method specification aims to conform to the requirements specified in the DID specification currently published by the W3C Credentials Community Group. For more information about DIDs and DID method specifications, please see the [DID PRIMER](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/did-primer.md).

### 1.1 Status of This Document

This document is a draft of a potential specification. It has no official standing of any kind and does not represent the support or consensus of any standards organization.

### 1.1.2 Conformance

As well as sections marked as non-normative, all authoring guidelines, diagrams, examples, and notes in this specification are non-normative. Everything else in this specification is normative.

The key words MAY, MUST, and SHOULD in this document are to be interpreted as described in [BCP 14](https://datatracker.ietf.org/doc/html/bcp14) [RFC2119](https://www.rfc-editor.org/rfc/rfc2119) [RFC8174](https://www.rfc-editor.org/rfc/rfc8174) when, and only when, they appear in all capitals, as shown here.

---

## 2. Introduction

### 2.1 Purpose

This document aims to define a DID method for the issuance and management of Decentralized Identifiers (DIDs), designed in compliance with W3C specifications. The key distinction of this method is its enhanced mechanism for updating the status and destruction of DID Documents, implementable on any UTXO-based blockchain serving as the data ledger. Numerous UTXO-based blockchains are currently utilized in the industry, including Bitcoin, Litecoin, Cardano, Bitcoin Cash, Zcash, among others. This DID method is applicable across all UTXO-based blockchains, ensuring suitability for deployment across these networks. Our objective is to achieve interoperability and consistency, regardless of the specific underlying UTXO architecture.
- Immutable and Timestamped Records: Blockchain's double-spend protection ensures that transaction chains are immutable, unique, and timestamped sequences of events. This feature is utilized to record DID issuance, status updates, key rotations, and destructions. UTXO-based blockchains support parallel transaction validation, enhancing scalability.
- Leveraging Existing Digital Signatures: The digital signatures inherent in blockchain transactions are leveraged for the DID authorization system. This supports a hierarchical public key infrastructure, establishing governance and hierarchical authorization over DID issuance when governance or control over DIDs on a public blockchain is required.
- Programmable Multi-Party Authorization: The programmable nature of blockchain transactions allows for easy implementation of multi-party authorization schemes. For example, enabling either a DID Controller or a DID Subject to destroy a DID using a 1-of-2 multi-signature scheme within a transaction locking script.

### 2.2 Intended audience

This specification is intended for software implementers that want to adopt this method for the creation and verification of Decentralized Identifiers. The implementation of this method was chosen to be on the Dimecoin Blockchain due to its low transaction fees, high throughput, and near instant transaction verification. But it is understood that it can be implemented in any UTXO-based blockchain. These specifications assume a basic understanding of programming and blockchain technology.

### 2.3 Scope

The specifications include:
- Use of the Dimecoin Blockchain as a Data Registry: Leveraging Dimecoin's public ledger to store and manage Decentralized Identifiers (DIDs) and their associated documents.
- Linking Public Keys to Blockchain Transactions: Providing detailed methods for associating a public key with a specific blockchain transaction (Tx) on the Dimecoin network.
- Transaction Structure and Signature Framework: Describing the anatomy of transactions and the composition of signature structures. This includes the use of multi-signatures for the issuance of DIDs and the creation of DID Documents. The signatures involve coordination between the DID Subject and the DID Controller through a component service known as a DID Manager, operated by an authorized entity. DID issuance can be initiated by any entity or wallet connected to the DID Manager. Additionally, the specifications explain how to link a blockchain transaction to a status check performed by the DID Manager.

This design enables the verification of DID status to be conducted independently from the DID issuer and the DID Manager, enhancing user privacy. Since the DID issuer and the DID Manager are not aware of the verification checks being performed, users can confirm the status of their DIDs without disclosing their actions to these entities. This increases privacy during the verification process. Furthermore, this method is universally applicable across different UTXO-based blockchain networks, including Dimecoin, making it a versatile and flexible solution for decentralized identity management.

### 2.4 Compliance

Our implementation of the DID method can appropriately handle and enforce the issuance, status check destruction, and verification status of the DID and DID Document in accordance with the specifications presented by the [W3C](https://www.w3.org/TR/did-core/#sotd), and the [DIF](https://decentralized-id.com/) .

### 2.5 Terminology

Please review terminology [here](https://github.com/dime-coin/dimedid-method/blob/main/Terminology.md).

---

## 3. Specification Overview

_THIS SECTION IS NOT NORMATIVE_

### 3.1 Prerequisites

Based on the [W3C specifications](https://www.w3.org/TR/did-core/) a Decentralized Identifier (DID) must adhere to the following core principles:  
- Persistent Identifier (URN): The DID should act as a permanent and unique Uniform Resource Name
- Cryptographic Verifiability: It must be possible to verify the DID through cryptographic means.
- Decentralization: The system should operate without the need for a central registration authority.
- Simplicity and Cost-Effectiveness: Creating a DID should be easy and economical.
- Resolution to a DID Document: The DID must always be able to resolve to, or be associated with, a corresponding DID Document.
- Variable Administration: The DID Subject is not necessarily the manager of their own DID; this can vary depending on the specific use case.

Similarly, the DID Document must fulfill the following criteria:  
- Public Availability: The DID Document should be accessible to the public.
- Mandatory Contents: The DID Document must include:
  - One or more keys for authenticating the DID Subject
  - One or more services associated with the DID Subject.
  - Additional metadata such as digital signatures, timestamps, and other cryptographic proofs.

### 3.2 UTXO DID Method

In this section we present an overview of the DID method. Our proposal introduces a new Decentralized Identifier (DID) method that links a UTXO and the DID with the public key of the subject and manages the DID status and destruction through transaction spending checks. We use the DIME Blockchain as the verifiable data registry.

The UTXO DID method uses the following method name: **dime**

#### 3.2.1 The DID

The issuance of a DID using this method is performed by publishing a blockchain transaction: **Tx0**. This transaction has a single input and a single output. The transaction ID (**TxID**) becomes the DID for the subject. The **TxID** can be easily calculated by either controller or subject and, because of the properties of blockchain it would never be repeated. Both the controller and the subject can easily compute the TxID, and due to the inherent properties of the blockchain, this identifier is guaranteed to be unique and non-repetitive. Moreover, the **TxID** is easily recognizable by independent third-party platforms, such as blockchain explorers, which enhances transparency and verification.

_1. Representation of a DID as per W3C specification_

```bash
DID:example:123456789abcdefghi
```

Where fields are broken down as follows:

| Scheme | DID Method | DID Method - Specific Identifier |
|----------|--------------|-----------------------------|
| DID:     | example:     | 123456789abcdefghi          |

_2. Representation of a DID using UTXO method_

```bash
did:dime:21f2dae26817752b8f92c51a49a898e287ad133a4e7ed64b4909f7b62f0bbb6e
```

Where fields are broken down as follows:

| Scheme | DID Method | DID Method- Specific Identifier |
|----------|--------------|-----------------------------|
| DID:     | Blockchian     | TXID                      |
| did:     | dime:     | 21f2dae26817752b8f92c51a49a898e287ad133a4e7ed64b4909f7b62f0bbb6e|

#### 3.2.2 The DID Document

The DID Document is published via a subsequent transaction **Tx1** that spends the output of **Tx0**. The relationship between the DID, the DID document, and the blockchain transactions is given in Figure 1.  The transaction **Tx1** contains a single input and a single output. The output contains the locking script, the DID Document and the funds covering the mining fee of the next transaction. **Tx1** spending the output of **Tx0** allows an external observer to conclude that there is a link between both blockchain transactions. The status of **Tx1** output indicates the latest status of the DID Document.

![Figure 1_DID UTXO Status](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDUtxoStatus.jpg?raw=true)

> _Figure 1: DID UTXO Status_

##### 3.2.2.1 The DID Document Data Model

Our current implementation uses [W3C DID Document Data Model](https://www.w3.org/TR/did-core/#data-model) and is referenced in the DID Document. Below is a representative example of a DID Document data model.

```json
"@context": "https://www.w3.org/ns/did/v1", 
  "id": "did:dime:5909468ac49f960e191faba2dd7da60bd1775ccf59e90b8390c971d04741b710",
  "controller": "did:dime:b6333300b727ae4d355ffe2fee06ebe9ed5565cb1321e02637fa971bd523272e",
  "verificationMethod": 
         [ { 
             "id": "did:dime:5909468ac49f960e191faba2dd7da60bd1775ccf59e90b8390c971d04741b710#subject-key",
             "type": "JsonWebKey2020", 
             "controller": "did:dime:5909468ac49f960e191faba2dd7da60bd1775ccf59e90b8390c971d04741b710",
             "publicKeyJwk": 
              { 
                  "kty": "EC", 
                  "x": "xJxFTwL183Hmz19WnLAgBa1wpljMuaYk_rBnAKlol-g", 
                  "y": "585wM9i1dGHr6qgL5NG5N2EAxel3Son9HpkGpl-hY-I", 
                  "crv": "secp256k1" 
              } } ]
  "authentication": [ "did:dime:5909468ac49f960e191faba2dd7da60bd1775ccf59e90b8390c971d04741b710#subject-key" ] 
```

### 3.3 DID Controller and DID Resolver

#### 3.3.1 DID Controller

As described in W3C, the DID Controller is an entity that has the capability to make changes to a DID document. A DID Controller is not a central registration authority, subjects can be identified by multiple DIDs issued by different DID Controllers. Initially the DID Controller is required to create an identity for itself. The process describe here is the same required for an external Subject DID Creation: the DID controller requires an issuance transaction **Tx0’***, locked to its own public key PKC0 and the “subject” public key PKCD. In this case, the subject is the controller itself. The transaction ID of **Tx0’**, **TxID0’** becomes the DID of the Controller. To generate the subsequent transaction that will contain the Controllers DID Document, the controller will sign the transaction using two public keys: PKCD and PKC0, both of which belong to the Controller. **Tx1’** input spends the output of **Tx0’**.

When requested by the subject, the DID Controller issues a new DID by creating and broadcasting two blockchain transactions: an Issuance and DID Document transaction. The issuance transaction, Tx0 is created by the DID Controller and provisioned (funded) by controller. UTXO of **Tx0** should provide enough funds to cover the mining fee for the next transaction.  The transaction ID of **Tx0**, **TxID0** becomes the DID of the Subject. The DID Document is contained in the subsequent transaction **Tx1**, linked to the issuance transaction Tx0 by spending its output. **Tx1** has a single output; that contains a payload with the DID Document and the minimal required funding to cover the mining fee pf the next transaction.

#### 3.3.2. DID Resolver

Per the W3C specifications, a DID Controller is an entity with the authority to modify a DID Document. Importantly, a DID Controller is not a central registration authority; subjects can possess multiple DIDs issued by different DID Controllers. Initially, the DID Controller needs to establish its own identity, following the same procedure as creating a DID for an external subject.

To achieve this, the DID Controller creates an issuance transaction denoted as **Tx0'**. This transaction is locked to the Controller's own public key **PKC0** and the "subject" public key **PKCD** -- in this case, the subject is the Controller itself. The transaction ID of **Tx0'**, referred to as **TxID0'**, becomes the DID of the Controller. To generate the subsequent transaction containing the Controller's DID Document, the Controller signs the transaction using both public keys **PKCD** and **PKC0**, which both belong to the Controller. The input of this transaction, **Tx1'**, spends the output of **Tx0'**.

When a subject requests a new DID, the DID Controller issues it by creating and broadcasting two blockchain transactions: an issuance transaction and a DID Document transaction. The issuance transaction, **Tx0**, is created and funded by the DID Controller. The unspent transaction output (UTXO) of **Tx0** must have sufficient funds to cover the mining fee for the subsequent transaction. The transaction ID of **Tx0**, designated as **TxID0**, becomes the DID of the subject.

The DID Document is included in the next transaction, **Tx1**, which is linked to the issuance transaction by spending its output. **Tx1** has a single output that contains the payload with the DID Document and includes the minimal required funding to cover the mining fee for any following transaction.

- The **versionId** of the DID Document corresponds to the txID of the transaction that contains it.
- The **versionTime** of the DID Document is the timestamp of the block that includes the transaction containing the DID Document.

The verifier utilizes the method-specific part of the DID identifier to search the ledger for the relevant transaction. By finding this transaction and its linked transactions that contain the DID Document, the verifier can perform status checks on their outputs.

To request the status of a DID, the verifier can use a DID resolver. Verifiers have the option to build and operate their own independent DID resolver, create their own implementation following this specification, or use a service provided by a third party that runs an implementation of the UTXO DID method.

![Figure 2_DID Creation](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDUTXO2.jpg?raw=true)

> _Figure 2: DID Creation_

### 3.4 DID Operations

In this section, we will cover CRUD specifications to Create, Read, Update, and Destroy a DID. We included implementation examples as references. Please note that some specifications are optional and serve only to illustrate potential implementations.

### 3.4.1 Create

In previous sections, we have explained how the DID and DID document are related through two transactions, and how the Controller issues a DID to itself. This section explains in detail the process of a DID Controller creating a DID and a DID Document for Subject, including the digital signatures and the transaction specification required. It also explains the use of signatures in blockchain transactions to bind the Subject and the Controller public keys to the DID and the DID Document.

Recall that the DID Controller possesses two keys:
- PKCD. Which serves as the Controller’s master key. It is only used to establish the Controllers DID.
- PKC0. Which is used to create/sign DIDs for DID subjects.
The Subject has a single key.
- PKS0. This key is always in possession of the subject.

**A: TxID0: Issuance Transaction.**

When a new DID is requested by the subject, the Controller will create an issuance transaction. This transaction locks the output to two public keys: the Controller's public key and the subject's public key. This initial transaction is necessary to initiate the DID Document process. is used in the DID string: **did:dime:TxID0** as the Subject’s DID.
**Tx0** has a single input and a single output. The DID Document is published via a subsequent transaction **Tx** that spends the output of **Tx0**. See Figure 3. Note that when the Controller is required to issue a DID for itself, the Issuance transaction locks the output to both controller’s public keys (PKCD and PKC0). _[See Section 3.3. DID Controller](https://github.com/dime-coin/dimedid-method/blob/main/README.md#33-did-controller-and-did-resolver)_.  

**B: TxID1: DID Document transaction**

This is a subsequent transaction that spends the output of the issuance transaction **Tx0**. This transaction has a single input and a single output. This output contains a data payload with the DID Document.  **Tx1** output is locked to a one-of-two multi-sig script signed either by Subject public key or the Controller public key. Once the input of **Tx1** is signed by both keys, the transaction is broadcasted to the network. When validated by miners it will read as resolved by the DID Resolver.

![Figure 3_TX Anatomy](https://github.com/dime-coin/branding-assets/blob/main/vectors/TxAnatomy.jpg?raw=true)

> _Figure 3: TX Anatomy_

![Figure 4_How the Subject and the Controller keys are link to the DID?](https://github.com/dime-coin/branding-assets/blob/main/vectors/SubjectControllerKeyLink.jpg?raw=true)

> _Figure 4: How the Subject and the Controller keys are link to the DID?_

**C: Data payloads in the transaction outputs**

After OP_RETURN we can find a data payload. This data does not affect the spending conditions, and it is described below:

- `DIME-DID` Identifier specifying this is a transaction associated with the DIME-DID Method.
- `Identity Code` DID Controller configuration identifier.
- `DID Document JSON DID Document` or type transaction indicator <1/2/3>: Issuance, Update or key rotation, and Destroy respectively.  

**D: Implementation Example**

Below illustrates a detailed implementation of the DIME-DID Method as a reference example for DID issuance. This specification covers the process of requesting a DID from the subject to the DID controller. It includes two specific examples of the implementation:
- **DID Controller Role:** The DID controller can be run by any entity. It is important to note that the DIME-DID method does not require a centralized controller. Any organization or entity can run a DID controller and create a DID for itself, as specified in _[See Section 3.3. DID Controller](https://github.com/dime-coin/dimedid-method/blob/main/README.md#33-did-controller-and-did-resolver)_.
- **Database Persistence:** We demonstrate database persistence in this implementation as an example, although this is optional based on implementation preferences

![Frame 5_Create DID](https://github.com/dime-coin/branding-assets/blob/main/vectors/createDID.jpg?raw=true)

> _Figure 5: Create DID_

**F: Key Considerations**

- **Proof of Ownership:** The DID Subject proves possession of their private key by signing transaction **Tx1** and submitting it to the DID Controller.
- **Transaction Tx0:** The output of **Tx0** is secured using the public keys of both the DID Controller and the DID Subject.
- **Transaction Tx1:** The input of **Tx1** requires signatures from both the Subject and the Controller. The output will include the DID Document generated by the Controller. This output is locked with a one-of-two multi-signature scheme, allowing either the Controller or the Subject to spend it.
- **Contents of the DID Document:**
  - The DID of the Subject.
  - The public key associated with the DID Subject.
  - The DID of the Controller (used to identify the DID Controller by resolving their DID).
  - An authentication method for the DID Controller (a public key verifiable through the signature on the input of **Tx1**).

### 3.4.2 Resolve

The resolver uses the DID (TxID) to find the transaction in the ledger and identify the linked transactions containing the DID Document. Once the DID Document Tx has been identified the resolver does a status check on the output of the Tx via the DID Resolver. Who will find the TxID given and track UTXO status until the last UTXO update is found.

The DID Resolver can be independently built and operated, implemented according to this specification, or provided by a third party that supports the UTXO-DID method. This method permits the use of different resolvers, ensuring the users are not required to rely on or trust our specific implementation.

### 3.4.3 Update

#### A: DID Document Status Update

This section details how to change the content of a DID Document. The DID controller can change or update the status of a DID Document by creating a new transaction that spends the output of most recent transaction referring to the DID Document's status.

![Figure 6_Status Update](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDUtxoStatus2.jpg?raw=true)

> _Figure 6: Status Update_

#### B: Rotation of Keys

Both subject and controller can initiate rotation of keys. Execution of key rotation is dependent upon who is performing the rotation and the reason it is being done. Scheduled or voluntary rotations are different from  forced rotations due to compromised keys.

**Below we listed a series of use cases:**
- User Key Rotation with Valid Subject's Key
- User Key Rotation upon Compromised Subject's Key
- User Key Rotation because controller rotated its <PKC0> N key (user does not know if N was compromised or rotated regularly)
- Controller rotation of valid or compromised M key <PKCD>
- Controller rotation to update a valid <PKC0> key
- Controller rotation upon <PKC0> key compromised


**C: Subject Key Rotation**

There are multiple reasons why a Subject may need to rotate their key. These reasons may include routine operational practices such as voluntary or scheduled rotations to comply with an organizations policies, security concerns such as key compromise, or the necessity to maintain a valid controller attestation due to the rotation of the controller's key.

- **Subject Key’s compromised:**

If the subject's key has been compromised, it cannot be used to attest rights anymore. As a result, the DID Controller must establish an authentication process for the subject that does not rely on the compromised keys. Once the DID Subject is successfully authenticated through this alternative method, the DID Controller recognizes that the public key **PKS0** has been compromised. The controller then signs a new issuance transaction using its own key **PKC0.**

In this process, the output from the transaction referring to the latest DID Document transaction **TXn** becomes the input for a new funding transaction **TXf**. This new transaction locks the output to both the controller's unchanged public key and the subject's new public key. This ensures that future transactions can be securely authorized using the updated keys.

- **Subject Key’s not compromised:**

In all other cases where the subject's old key remains secure, authentication via an external channel is unnecessary. The DID Subject must use both the old and new keys to attest their authorization for key rotation and to prove ownership of the new key.

![Figure 7_DID Key Rotation](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDKeyRotation.jpg?raw=true)

> _Figure 7: DID Key Rotation_

**D: Controller Key Rotation**
There are multiple reasons a Controller key needs to be rotated: either regular operating reasons like voluntary, scheduled rotation to comply with policies, security reason like any of the Controller keys: PKCD or PKC0 has been compromised. The Controller can lose any of the following keys.
- `PKCD`: Master Key which changes their own DID Authentication as well as all the issued DIDs.
- `PKC0`: Public Key associated with their DID document, i.e. the Root key for all their DID Issuance.  

Only in the scenario in which the Controller losses his master key **PKCD’**, would require a different process for Key rotation. When changing **PKC0** the Controller will just be able to update the keys themselves.  

**E: Compromised PKCD**

The process begins with the DID Controller initiating a Master Key update, during which it updates its key to a new Master Public Key, **PKCD’**. Subsequently, the Controller generates a new DID for itself, **TxID0’**, linking the old public key to the new one. It then creates and publishes a new DID Document, **TxID1’**, by spending the unique output of **TxID0’**.

As a result of the Controller's keys being updated, all DID Documents of subjects that were co-signed by the Controller's keys need to be updated. To accomplish this, the Controller must rotate the controller keys in the DID Documents of all subjects. The DID Subject accepts the key rotation request. The DID Controller then generates a Key Rotation transaction, which the Subject must sign to spend the output of TxIDn that contains the latest status of the DID Document. See Figure 8. _See Figure 8_.

The process starts with funding a new DID issuance and DID Document transaction using the new Master Key. The controller then creates a Rotation Transaction and sends it to the DID Subject for signing. After the subject signs it, the transaction is returned to the controller. The Rotation Transaction is then stored and broadcast on the blockchain.

Next, a new DID Document for the user is generated, incorporating a new derivation factor and updated keys. The controller creates a Publish Transaction for the DID Subject, which the subject signs and returns. This Publish Transaction is then stored and broadcast on the blockchain.

Finally, the updated DID Document is confirmed to have been successfully created and recorded on the blockchain.

![Figure 8_DID Master Key rotation](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDMasterKeyRotation.jpg?raw=true)

> _* Figure 8: Notification of key rotation of end-user is a user experience decision, configurable and not mandatory. Invalid signatures will be rejected by blockchain_

**F: Compromised PKC0**

When a Controller needs to rotate their Controller Key associated with their DID Document—for instance, to change the root key for all their DID issuances—they will follow the same process depicted within the "loop" of the diagram above. The key difference in this scenario is that the Controller can independently perform the steps to create the Rotation Transaction and publish it on the blockchain. However, they still require the Subject to sign the updated DID Document. To facilitate this, the Controller will create a new Publish Transaction linked to the Rotation Transaction. _See Figure 9._

![Figure 9_TX Anatomy](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDTxAnatomy2.jpg?raw=true)

> _Figure 9: Tx Anatomy_

### 3.4.4 Destroy

In this section we explain how to destroy a DID. This method uses the spent status of the latest UTXO in the DID Document to indicate the active status of a DID. When the last transaction in the chain is spent, the DID is destroyed. See section 3.4.2, DID and DID Document Status. A DID can be destroyed by either the DID Subject or the DID Controller. Here are three ways the DID Subject can destroy its DID:
- **Subject is still in control of the private key and decides to destroy its DID,** through the DID controller by calling the controller's DID destruction service. Bellow we provide an implementation example. _See Figure 10_
- **Subject is not in control of the private key** (A specific example might be when the subject lost his/her device) and decides to destroy their DID.
- **Subject asks DID Controller to destroy on its behalf.** Note that to secure subject request we advise Controllers to apply a mandatory, strong authentication of DID Subject before executing any changes. Bellow we provide an implementation example. This will be signified by the transaction type indicator, as described in [section 3.4.1.](https://github.com/dime-coin/dimedid-method/blob/main/README.md#341-create) _See figure 11_

In all cases the destruction is initiated by the DID Subject.

![Figure 10_DID Destruction Initiated by Subject](https://github.com/dime-coin/branding-assets/blob/main/vectors/DestroyDID.jpg?raw=true)

> _Figure 10: DID Destruction initiated by DID Subject_

![Figure 11_DID Destruction Initiated by Controller](https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDControllerDestroy.jpg?raw=true)

> _Figure 11: DID Destruction initiated by DID Controller_

---

## 4. Governance Model using the DID-DIME method

_THIS SECTION IS NOT NORMATIVE_

The UTXO-Based DID Method supports a governance service where the **DID Subject** accepts a DID from a trusted **Controller** as valid. The **Verifier** will only accept as valid a DID Subject whose DID Document is co-signed by that specific Controller. As mentioned before, the DID Controller can be operated by any entity. The DID-DIME method does not require a centralized controller. Example below:

- Imagine a scenario where the DID Controller is run by the **International Academic Credential Consortium (IACC)**.
- Every DID issued by the IACC is always co-signed by this Controller. The verifier that checks the validity of a graduate's DID ensures it is always co-signed by the IACC Controller.
- The DID Controller establishes an ecosystem where value is derived from attestation to the keys of a DID Subject and the signature of the Controller. Initially, the Controller will issue a DID for itself following the process described in the UTXO DID method (_see section 3.4.1_).
- In this case, the DID Document will be self-attested. The Controller will issue a DID to an alternate key-pair, which will then be used as the master key-pair for attestation of DIDs to its audience.
- The trust framework supports a schema of key hierarchies and the issuance of the DID Controller. Once the Controller has been assigned a key, it becomes the master of that key for issuing all DIDs to its DID Subjects.

**DID PKCD = Master key and PKC0 = Controller Key to sign Subject DIDs.** When the Controller signs a new DID Document, they publish their public key to enable authentication of their own DID. For governance verification, the verifier uses the DID to locate the corresponding transaction on the ledger. Once the transaction is found, the verifier reviews the UTXO status and examines the DID Document. To confirm governance, the verifier must ensure that the transaction providing the TxID, which became the Subject's DID, has been co-signed by one of the Controller's published keys.

---

## 5.Low latency DID resolution

_THIS SECTION IS NOT NORMATIVE_

As discussed earlier (_See Section 3_), the creation of a DID and its associated DID Document involves two interconnected transactions linked by spending a unique UTXO (Unspent Transaction Output). In a blockchain, each transaction references the one before it, allowing for a sequential trace. Given a specific TxID (Transaction ID), one can navigate the ledger to find the preceding transaction.

The DID method requires that every status update for a DID be connected back to the initial transaction **TxID0**. Additionally, the DID controller must verify the UTXO status of the most recent transaction on the chain. This means we need to trace through each transaction step-by-step until we reach **TxID0**. To enhance efficiency in this process, our implementation utilizes an indexing service that enables forward transaction retrieval and streamlines DID status checks.

### Timing and Latency in DID Resolution Processes

Currently, the DID resolver searches only for transactions in mined or minted blocks. Given that Dimecoin has an average block time of approximately 50 seconds, which is significantly faster than Bitcoin's 10-minute intervals, this reduces the resolution time for newly issued DIDs. Since broadcasted transactions are not subject to reorganization or modification in the mempool, the mempool becomes the initial trusted source for transaction status checks.

Additionally, Dimecoin's blockchain supports large blocks, allowing most transactions in the mempool to be included in the subsequent block. This enhances the reliability of transactions within the mempool. The key innovation of this approach is that it achieves low resolution latency due to the faster block times. However, it also shifts the responsibility for the stability of the DID Document from the DID Resolver to the requester performing the status check.

### User-Controlled Security through Block Validation

This approach shifts the responsibility for determining DID security and stability from the DID-DIME method to the user. By using miner or staker block validation, users can assess the security of a DID based on the number of block confirmations. This method provides low resolve latency while giving users the flexibility to determine stability based on the DID Resolution Metadata. The metadata includes information on the number of confirmations (i.e., the distance from the mempool in blocks) that a resolved DID document has received. The DID-DIME method specifications will also offer clear guidelines on how different numbers of confirmations correspond to varying levels of stability and security guarantees:
- DID-DIME Method specification
  - **Resolution Process:** should specify that mempool will be searched too
  - **DID Resolution Metadata:** should document the new field defined in previous section
  - **Security Section:** should list recommendations on how number of confirmations maps to DID stability and DID Document stability

The DID Spec Registries should define a new field for where the resolver can signal the number of confirmations for the first DID transaction **Tx0** and the confirmations of the resolved (last by default) DID Document transaction.

| Confirmations.create    | DID Location    | Guidance of Use|
|----------|--------------|-----------------------------|
|0 | Mempool | Still in the mempool; do not rely on it |
| < 6 | Blockchain | Confirmed recently; handle with moderate care |
| >= 6 | Blockchain | Confirmed in several blocks; ready for normal use |


| Confirmations.update    | DID Documentat Location    | Guidance of Use|
|----------|--------------|-----------------------------|
|0 | Mempool | Still in the mempool; do not rely on it |
| < 6 | Blockchain |Confirmed recently; handle with moderate car |
| >= 6 | Blockchain | Confirmed in several blocks; ready for normal use |

```bash
"confirmations": {
- "create": 123,    // confirmations of the initial transaction for the resolved DID
- "update": 234     // confirmations of the DID Document transaction for the resolved DID}
```

For a newly created DID the number of confirmations is highly likely to be the same as both initial transactions are submitted to the dimecoin network together. The update field will signal the confirmations of the resolved DID Document, which by default is the last DID document on the chain, unless resolution of specific DID document version was requested by Version-ID.

The issuers and verifiers can configure number of valid blocks needed to accept a DID as resolved. It could be 0 confirmation requirement to **n** confirmations.

---

## 6. Data register analysis

_THIS SECTION IS NOT NORMATIVE_

This section outlines the technical reasons for choosing Dimecoin, including relevant cost and security considerations.

### 6.1 Distributed Ledger Technology

In December 2013, the Dimecoin protocol was launched, making it one of the longest running UTXO chains in existence. The DIME Blockchain ledger is a distributed platform that provides scalability, transparency, immutability, and efficient data consumption. Data can be published on the blockchain and retrieved within blockchain transactions.

Dimecoin offers rapid block times, with new blocks produced approximately every 50 seconds, significantly faster than Bitcoin's 10-minute intervals. This quick block generation enhances the speed at which transactions are confirmed on the network, making it more efficient for users.

In addition to its speed, Dimecoin boasts near-zero transaction fees, providing a cost-effective solution for executing transactions. This minimal fee structure is advantageous for applications that require frequent transactions or microtransactions, as it reduces the overall cost for users.

By applying this solution to the Dimecoin network, we capitalize on its fast transaction confirmations and low fees. This approach not only accelerates the resolution time for newly minted DIDs but also shifts the responsibility for the stability of the DID Document from the DID Resolver to the requester performing the status check. The combination of Dimecoin's speed and cost-efficiency enhances the overall effectiveness of implementing the DID method on this network.

### 6.2 Why not others? Ledger Comparison Analysis

- **BTC (Bitcoin)**: While Bitcoin is the most established UTXO-based ledger, its 10-minute block intervals and high average transaction fees make it unsuitable for applications requiring fast and cost-efficient DID operations. The limited transaction throughput of BTC (approximately 7 transactions per second) significantly hampers its scalability for high-volume use cases.

- **BCH:** A UTXO- PoW ledger with a maximum block size of 32MB. Although BCH has a higher transactions per second (TPS) rate than BTC, its transaction processing remains limited and while transaction fees are lower in average than BTC, they are still relatively high.
- **Ethereum (ETH):** Previously a PoW ledger, now using Proof of Stake (PoS) as its consensus mechanism. All statements and data refer to ETH before this change. The new adopted consensus mechanism allows ETH to process block faster than BTC and BCH and BSV. The transaction structure of an Ethereum will request, most likely to utilise a token protocol to store and monitor the DID Document. ERC-20, their most adopted token protocol overage transaction fee remains considerably high as the complexity of the smart contract increases, so does the gas fee. ETH has the highest average transaction fees among blockchains.
- **Private ledgers,** such as Hyperledger incur higher costs for implementation, maintenance, transaction fees and conventionally single authorities running the infrastructure.

Our solution requires high-volume transaction processing at low cost, as well as maintaining data integrity over time and across parties involved. Immutability and alteration records should be enforced by an independent process: the consensus mechanism. Additionally, it does not require the execution of any programmatic function at the block validation level, avoiding execution costs in transaction fees. Lastly in DIME there’s the 'first-seen rule' which means that validators will not accept a double-spend before block publication even for a higher fee if a miner receives a transaction, they verify it is correct, then accept it as valid. This means they will not accept a double-spend of the same input -- then add the transaction in the mempool. It may appear in the next block, or the block after. For these reasons, using the DIME blockchain benefits from its scalability, low cost, and data integrity provided by its hybrid PoW/POS mechanism.

---

## 7. Privacy Considerations

_THIS SECTION IS NOT NORMATIVE_

This section covers security considerations for the UTXO-DID Method. We discuss key storage and protection, usage policies, and security and privacy best practices.

### 7.1 Data minimisation and Personal identifiable information best practices

The UTXO-DID Method ensures that no personally identifiable information (PII) is stored, linked, or added to the DID, the DID Document, or the transaction resolving the DID and its associated DID Document. Since the network is public and immutable, any data recorded on the blockchain becomes permanent and cannot be fully removed.

### 7.2 DID Correlation Risk

There is a potential risk of identities being linked if they are used frequently or if their usage becomes publicly accessible. This introduces correlation risks, as detailed in [DID Correlation Risks](https://www.w3.org/TR/did-core/#did-correlation-risks). Below are best practices to help mitigate these risks:

- If a DID is compromised or the user feels uncomfortable with its exposure, the DID Subject can deactivate it by spending the associated output. Since TxIDs linked to DIDs are excluded from the transaction payment process, the only way to associate payments with identities is through Verifiable Credentials (VCs).
- To address privacy concerns related to transaction linkability in the UTXO-DID Method, users can create an unlimited number of DIDs. This allows for enhanced privacy by using different identities for separate purposes.
- If you are a verifier and a subject has shared a DID associated with a VC containing personal information, avoid sharing the verification history with other verifiers to safeguard the subject's privacy.

---

# 8. UTXO DID Method: Normative Reference

## 8.1 DID Syntax

- **DID method name:** dime
- **DID method specific identifier:** 64 characters long hexadecimal presentation of a DIME Blockchain transaction ID

The hexadecimal presentation MUST use lowercase characters for hexadecimal digits a–f.

```bash
Example: did:dime:8280eadd84515d071e942f1548af7891e0182bf83e7b5848a02b0a58543fbf5f
```

## 8.2 Verifiable Data Registry

The UTXO DID method SHOULD use the DIME Blockchain as a public ledger to store the DID related data and statuses. Each DID is recorded as a sequence of chained transactions of the following kinds:

- **DID Issuance Transaction**: the first transaction on the DID chain
- **DID Document Transaction:** the transaction which OP_RETURN data contains a version of the DID document
- **DID Destruction Transaction**: MUST be the last transaction on the DID chain which invalidates the DID
  
Due to the design of the blockchain, every DID Document transaction **MUST** be preceded by either a DID issuance transaction or a dedicated DID funding transaction. These funding transactions supply additional funds for network fees but do not alter the state of the DID.

Below text uses the following symbols that refer to SECP256K1 private and public keys:

- **C0 , PKC0:** DID Controller’s private and public key, respectively.
- **S0, PKS0:** DID Subject’s private and public keys, respectively.
- **SigC0, SigS0:** Signatures made using the DID Controller’s or DID Subject’s private keys, respectively.

It also uses term `identityCode`. This is a code that identifies the DID controller that's created by transactions. This code MUST be present, and it **SHOULD** be unique.

### 8.2.1 DID Issuance Transaction

The DID issuance transaction is structured with a single input and a single output:

- **Input Requirements:** The input spends the funding UTXO, which is provided out-of-band by the creator of the issuance transaction. This UTXO MUST contain sufficient funds to cover network fees for this transaction and the subsequent two transactions.

- **Output Requirements:** The output of the DID issuance transaction MUST include enough funds to cover network fees for the next two transactions.

- **Locking Script:** The locking script of the DID issuance transaction MUST require signatures from both the DID Controller and the DID Subject to spend it.

- **OP_RETURN Data Payload:**

    - The first segment MUST be set to the string literal did:dime.
    - The second segment MUST contain the identityCode.
    - The third segment MUST be set to the string literal 1 (numerical digit 1).
    - Additional segments MAY be included for implementation-specific purposes.

<img width="687" alt="Screenshot 2024-11-21 at 00 10 44" src="https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDIssuanceTx.jpg?raw=true">

### 8.2.2 DID Document Transaction

The DID document transaction is funded either by a DID issuance transaction or a dedicated DID funding transaction. It contains the DID document in the third segment of the `OP_RETURN` payload. The transaction has a single input, which **MUST** utilize the UTXO provided by the preceding DID issuance or funding transaction.

- **Output Requirements:**  
  The transaction's output **MUST** include adequate funds to cover the mining fee for the subsequent transaction.

- **Locking Script:**  
  The locking script **MUST** require a signature from either the DID Controller or the DID Subject to authorize spending.

- **OP_RETURN Data Payload:**  
  - The first segment **MUST** be the string literal `did:dime`.
  - The second segment **MUST** contain the `identityCode`.
  - The third segment **MUST** include the DID document represented as a JSON string.
  - Additional segments **MAY** be added for customized implementation purposes.

<img width="687" alt="Screenshot 2024-11-21 at 00 10 44" src="https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDDocumentTx.jpg?raw=true">

The transaction ID (TxID) of the DID document transaction serves as the `versionId` of the DID document and can be resolved accordingly.  
The timestamp of the block containing the DID document transaction serves as the `versionTime` of the DID document and can be resolved accordingly.

### 8.2.3 DID Destroy Transaction

The DID destruction transaction is funded by the preceding DID document transaction. It has one input that **MUST** spend the UTXO of the previous DID document transaction. This transaction **MUST** have a single output with a value of 0, rendering it unspendable. When present, the DID destruction transaction becomes the final transaction in the DID chain and effectively invalidates the DID.

- **Output Requirements:**  
  The output of the DID destruction transaction **MUST** have a value of 0 and **SHOULD** include no locking script other than `OP_RETURN`.

- **OP_RETURN Data Payload:**  
  - The first segment **MUST** be set to the string literal `did:dime`.
  - The second segment **MUST** contain the `identityCode`.
  - The third segment **MUST** be set to the string literal `3` (numerical digit 3).
  - Additional segments **MAY** be added for custom implementation purposes.

<img width="676" alt="Screenshot 2024-11-21 at 00 10 44" src="https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDdestructTx.jpg?raw=true">

### 8.2.4 DID Funding Transaction

The DID funding transaction does not alter the state of the DID and is solely used to provide additional funds needed to continue the DID transaction chain. It contains two inputs and one output:

- **Input Requirements:**  
  - The first input **MUST** spend an out-of-band UTXO provided by the creator of this transaction. This UTXO **MUST** include sufficient funds to cover network fees for two transactions.  
  - The second input **MUST** spend the UTXO from the preceding DID document transaction, which provides funds to cover network fees for one transaction.

- **Output Requirements:**  
  The output of the DID funding transaction **MUST** include sufficient funds to cover network fees for the next two transactions.

- **Locking Script:**  
  The locking script of the DID funding transaction **MUST** require signatures from both the DID Controller and the DID Subject to authorize spending.

- **OP_RETURN Data Payload:**  
  - The first segment **MUST** be set to the string literal `did:dime`.  
  - The second segment **MUST** contain the `identityCode`.  
  - The third segment **MUST** be set to the string literal `2` (numerical digit 2).  
  - Additional segments **MAY** be included for custom implementation purposes.

<img width="674" alt="Screenshot 2024-11-21 at 00 10 44" src="https://github.com/dime-coin/branding-assets/blob/main/vectors/DIDFundingTx.jpg?raw=true">

### 8.2.5 Example of DID Transaction Chain

_THIS SECTION IS NOT NORMATIVE_

Below, the example shows a DID transaction chain for a DID that had one change in the DID Document and then was destroyed.

<img width="711" alt="Screenshot 2024-11-21 at 00 10 44" src="https://github.com/dime-coin/branding-assets/blob/main/vectors/ExDIDTxChain.jpg?raw=true">

## 8.3 DID Operations

Authorization for performing operations is based on blockchain properties, which automatically reject transactions if the unlocking script fails to unlock the targeted UTXOs. Both the DID Controller and the DID Subject **MUST** have their own SECP256K1 keys, which they **MUST** use to sign the DID transactions being added to the DID's chain of transactions.

- **Key Requirements:**  
  - The DID Controller and DID Subject each possess unique SECP256K1 keys for signing.  
  - These keys are used to authorize and secure transactions on the blockchain.

- **Separate Entities:**  
  - If the DID Controller and DID Subject are implemented as separate entities, each **MUST** have their own DID.  
  - Resolving these DIDs yields their respective public keys.  

- **DID Relationship:**  
  - The DID Subject's DID Document **MUST** include the DID of its Controller in its listing.  

```json
{
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:dime:1909a27e2f9c01dbc99f6391f77cd96032e00b92ff601584b7e227009055e6da",
    "controller": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9",
    "verificationMethod": [
        {
            "id": "did:dime:1909a27e2f9c01dbc99f6391f77cd96032e00b92ff601584b7e227009055e6da#subject-key",
            "type": "JsonWebKey2020",
            "controller": "did:dime:1909a27e2f9c01dbc99f6391f77cd96032e00b92ff601584b7e227009055e6da",
            "publicKeyJwk": {
                "kty": "EC",
                "x": "l5sYB-y78yE-n8Fc1d9pZeVFYhGD8qWoFRk-abyr0p4",
                "y": "XVcP352DcjrO374NW-4iNfUUWLLu_ZvcNhZtWPFURAg",
                "crv": "secp256k1"
            } } ],
    "authentication": [
        "did:dime:1909a27e2f9c01dbc99f6391f77cd96032e00b92ff601584b7e227009055e6da#subject-key"
    ]
}
```

In Self-Soverign Identity (SSI) use, the DID document lists both public keys since the DID Controller’s DID does not exist:

```json
{
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9",
    "verificationMethod": [
        {
            "id": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9#subject-key",
            "type": "JsonWebKey2020",
            "controller": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9",
            "publicKeyJwk": {
                "kty": "EC",
                "x": "oA39rl7p8GjPi4oVJRhesnhm9M4RKl0_dWs6EjDSm84",
                "y": "l9j72B38c3VHlwk9-YtWyLovLFGU_Bkx1qa6DRLf5UQ",
                "crv": "secp256k1"
            }
        }
    ],
    "service": [
        {
            "id": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9#controller-website",
            "type": "LinkedDomains",
            "serviceEndpoint": "<service-endpoint-url>"
        }
    ],
    "authentication": [
        {
            "id": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9#auth",
            "type": "JsonWebKey2020",
            "controller": "did:dime:a2fc941316adc10d680c98a06bf68da88ec513c658a9dc5ef837058064b588f9",
            "publicKeyJwk": {
                "kty": "EC",
                "x": "-femws1TMAIQZLWNuhglkF9N6RrJAIJA7Yk64CavSEA",
                "y": "BvoLuvdFvLv1p3j1myLZrhCBmYvoBHtp15ol_BB81Yk",
                "crv": "secp256k1"
            }
        }
    ]
}
```

## 8.3.1 DID Creation

To create a DID, the DID Controller **MUST** publish two transactions to the blockchain:

- **DID Issuance Transaction** (_see A.2.1 DID Issuance Transaction_), and  
- **DID Document Transaction** (_see A.2.2 DID Document Transaction_) containing the first version of the DID Document.

The DID Controller is responsible for ensuring adequate funding to cover the network fees for these transactions.  
If the DID Subject is acting as its own Controller (Self-Sovereign Identity - SSI), it **MUST** own and use:

- **C0/PKC0** as the keypair representing the DID Controller.  
- **S0/PKS0** as the keypair representing the DID Subject.

## 8.3.2 DID Document Updates

To create a new version, or udpate, a DID Document, the DID Controller **MUST** publish two transactions to the blockchain:

- **DID Funding Transaction** (_see A.2.4 DID Funding Transaction_), which provides the funds necessary to cover the network fees for this and the subsequent DID Document transaction.  
- **DID Document Transaction** (_see A.2.2 DID Document Transaction_), which publishes the new version of the DID Document.

The DID Controller is responsible for providing funding for the DID Funding Transaction.

- The DID Funding Transaction **MAY** be signed by either the DID Subject or the DID Controller.  
- However, the DID Document Transaction **MUST** be signed by both the DID Subject and the DID Controller.  

This ensures mutual agreement between the DID Subject and the DID Controller on the new contents of the DID Document.

## 8.3.3 DID Deactivation

To deactivate, or destroy a DID, either thd DID Subject or DID Controller **MUST** publish a DID destruction transaction (_see A.2.3 DID Destruction Transaction_). The funds for this transaction are already available in the UTXO of the last transaction of the DID’s transaction chain.

## 8.3.4 DID Resolution

To resolve a DID to the latest version of the DID Document, the DID Resolver **MUST** perform the following steps:

1. Fetch the blockchain transaction whose transaction ID is the method-specific identifier of the DID. Decode the transaction ID from its hexadecimal representation to a binary number and designate it as the current transaction.
2. Fetch the transaction that spent UTXO 0 of the current transaction.
3. Check the type of the transaction:

   - **3.1 If it is a DID Document Transaction** (_see A.2.2 DID Document Transaction_):  
     - **3.1.1** If UTXO 0 of the current transaction is unspent, return the DID Document as the resolution result.  
     - **3.1.2** If UTXO 0 is spent, make this transaction current and repeat from step 2.  
   - **3.2 If it is a DID Funding Transaction** (_see A.2.4 DID Funding Transaction_):  
     Make this transaction the current transaction and repeat from step 2.  
   - **3.3 If it is a DID Destruction Transaction**:  
     Return the last observed DID Document as the resolution result, set the `deactivated` property to `true` in the DID Document metadata, and terminate the process.

Note: If a `versionId` query is present, the algorithm **MUST** modify step 3.1 as follows:

- **3.1 If it is a DID Document Transaction:**  
  - **3.1.1** Check if its transaction ID matches the value of the `versionId` query.  
    - **3.1.1.1** If yes, return the DID Document as the result of the resolution.  
    - **3.1.1.2** If no, check if the UTXO of this transaction is spent:  
      - **3.1.1.2.1** If the UTXO is unspent, set the `error` property of the DID resolution metadata to `notFound` and terminate.  
      - **3.1.1.2.2** If the UTXO is spent, designate this transaction as the current transaction and repeat step 2.  

And step 3.3 should read:

- **3.3 If it is a DID destructiont Transaction**
  Set error property of DID resolution metadata to `notFound` and terminate.

---

# 9.References and Credits

|   |                            Specification                                           | Description                |     Author(s)      |
|---|------------------------------------------------------------------------------------|-----------------------------| -------------------- |
| [1] | [Decentralized Identifiers(DIDs) v1.0](https://www.w3.org/TR/did-core/) | Core Architecture, data model, and representations | Manu Sporny, Dave Longley, Markus Sabadello, Drummond Reed, Orie Steele, Christopher Allen |
| [2] | [nChain Research](https://github.com/nchain-research/nChain-Identity-bsvdid-method)     | DID:BSV Method Specification: A UTXO Friendly Model | Thomas Moretti, Leon Mlakar, Bozo Dragojevic, Kapil Jain, Maria Eugenia Lopez|
| [3] | [Ethr Revocation 2022](https://spherity.github.io/vc-ethr-revocation-registry/)    | An Ethereum, EIP-5539 compliant and registry-based revocation mechanism for Verifiable Credentials Maintainer: Spherity GmbH ([email](mailto:lauritz.leifermann@spherity.com)) ([website](https://www.spherity.com/))| Philipp Bolte, Dennis vo der Bey, Lauritz Leifermann |
| [4] | [did:btc Method Specification](https://microstrategy.github.io/did-btc-spec/)    | DID:BTC Method Specifcation | Daniel McNally |
| [5] | [DID Use Cases](https://www.w3.org/TR/did-use-cases/) | w3c Use Cases and Requirements for Decentralized Identifiers | Kim Hamilton-Duffy, Ryan Grant, Adrian Gropper |