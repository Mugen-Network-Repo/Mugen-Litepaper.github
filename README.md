# Mugen-Litepaper.github
Litepaper outlining Mugen's Technology and Thesis




# Mugen Litepaper

## 1. Summary

Mugen Network introduces the Programatic Intents and Messaging Protocol (PI-MP) to simplify and streamline blockchain interactions across diverse networks. By providing a standardized interface for decentralized applications (dApps), Mugen Network enhances user experiences, fosters developer efficiency, and accelerates the adoption of blockchain technology. This framework addresses the blockchain ecosystem's current fragmentation and offers a seamless solution for complex cross-chain workflows, particularly in gaming and other decentralized applications.

The PI-MP protocol enables efficient communication between different blockchain networks, reducing the complexity of managing multiple interactions. This not only optimizes performance but also lowers transaction costs, making blockchain technology more accessible to a broader audience.

## 2. Introduction

### 2.1 Current Situation

The blockchain ecosystem is rapidly expanding, leading to the emergence of numerous L1’s, L2’s , Rollup’s and decentralized applications (dApps) across various blockchain networks. However, this growth has also resulted in significant fragmentation, making it difficult for users and developers to navigate different protocols and engage in cross-chain interactions. Existing solutions for cross-chain asset transfers and interactions still need to be improved to address the broader challenges of user experience and application development.

### 2.2 Our Thesis

Mugen Network proposes the GMP+Intent Framework (Shogun) to bridge the gap in the current blockchain ecosystem. This innovative framework abstracts complex workflows, transforms ambiguous user intents into executable cross-chain workflows, and provides a standardized interface for dApps. By simplifying interactions and enhancing accessibility, Mugen Network aims to drive mainstream adoption and foster innovation within the blockchain space.

https://i.imgur.com/j8Xnqri.png

### 2.3 Vision and Goals

Our vision is to create a unified, interoperable blockchain ecosystem that simplifies user interactions and enhances application development. By leveraging the GMP+ Intent Framework, we aim to reduce fragmentation and enable seamless cross-chain communication, lowering barriers for developers and users alike.

## 3. GMP + Intent Framework

### 3.1 Meet Mugen — Introduction & What is it?

Mugen Network is a pioneering platform that leverages the GMP+ Intent Framework (Shogun) to streamline blockchain interactions. It is designed to support complex workflows and provide a unified interface for decentralized applications, particularly for cross-chain Bridging. Mugen Network simplifies the execution of user intents, making blockchain technology more accessible and user-friendly.

### 3.2 Why do we need Intents + GMP  for Web3?

The web3 Ecosystem is ever-growing with new L2s, Roll-ups and dApps being published almost everyday. However all of these ecosystems are particularly disconnected from each other without any robust mechanism as middleware to facilitate communication and exchange of liquidity in a sustainable manner. 

The current infrastructure does not facilitate dynamic communication or communication induced decisions which increase the transaction costs and make it hard for everyone to use these mediums for their cross-chain or multi-chain applications. 

Using Mugen , A crosschain swap ( USDT ETH to ARB on Arbitrum )that could have costed 10$ in execution cost would be done in as low as 2.5$ with 3 times faster settlement. 

https://i.imgur.com/PEyS9oV.png


## 4. Technical Architecture

https://i.imgur.com/UDMIwbl.png

**The Mugen Intent Handler is divided into four major modules, each with it’s own sub-components**

1. **Listener**
2. **Registry**
3. **Resolver**
4. **Liquidity Manager**

### **Component Details -**

1. **Listener**

Purpose:
The Listener component monitors events and trigger the Intent scripts within the network. It operates both on-chain and off-chain.

- Gateway Contract: Monitors and listens for events triggered by the Gateway contracts. These events signify actions that need to be processed by the Mugen Network.
- Custom Intent Triggerer: Listens for custom intent triggers from external sources. These triggers initiate specific actions or transactions within the network.

**2. Registry**

Purpose:
The Registry component allows developers and organizations to deploy and manage scripts on the Mugen Network. It ensures that scripts are interpreted correctly and stored securely.

Sub-Components:

- Interpreter: Interprets the scripts developed by the community. This ensures that the intents are understood and can be executed by the network.
- Intent Scripts Storage: A storage system where all interpreted scripts are securely stored. This allows for efficient retrieval and execution of scripts as needed.

**3. Resolver**

Purpose:
The Resolver component is responsible for executing the requested intents by running the relevant scripts. It integrates with several other systems to ensure accurate and efficient execution.

Sub-Components:

- Quotation Oracle: Calculates and provides the gas and fees required to resolve a requested intent. This ensures that transactions can be executed without any delays due to insufficient gas or fees.
- Off-Chain Data Oracle: Provides necessary off-chain data to assist in the execution of transactions. This can include data from external APIs, databases, or other off-chain sources.
- Transaction Manager: Handles all transaction and relayer logic across all chains. This ensures that transactions are executed correctly and efficiently, regardless of the blockchain they are on.

**4. Liquidity Manager**

Purpose:
The Liquidity Manager ensures that there is sufficient liquidity to facilitate cross-chain transactions. It integrates with various liquidity providers and pools.

Sub-Components:

- Mugen Pools: A liquidity pool contract that allows anyone to provide liquidity. This liquidity is used to facilitate cross-chain transactions, ensuring that there are enough funds to complete transactions across different blockchains.
- Aggregators/Fillers: Third-party contracts that provide additional liquidity and fill cross-chain orders. These can be external liquidity providers or decentralized exchanges that help in maintaining liquidity within the network.

### 4 Technology Behind Mugen

### 4.1 Processing Message and Intents

The Mugen Network processes messages and intents in three distinct ways. Below is a detailed explanation of each method:

**1. Message only**

In this method, a message is passed from the source chain to the destination chain through a resolver without executing any intent scripts. This is a straightforward message relay process.

**2. Message with Intents**

In this method, the message includes a parameter that instructs the resolver to execute an intent script. The message data acts as a parameter to the script, and the result of the script execution is sent to the destination chain.

**3. Only Intents**

In this method, intents are triggered externally by a custom intent trigger. The intent script is executed first, and the result is then passed as a message from the source chain to the destination chain. (make it this way - result is then passed on to another script or ends up as transaction message on destination chain)

### 4.2 Journey of an Intent/Message on Mugen network

- **Intent Creation:** Developers create intents as scripts and deploy them to the Mugen Network through registry.
- **Script Interpretation:** The Registry component interprets the scripts and stores them securely.
- **Intent Initiation:** User send message/intent through the gateway contract which emit an initiation event.
- **Listener:** The Listener component monitors for events and triggers, both on-chain through gateway contract and off-chain custom intent tirggerer.
- **Intent Resolution:** The Resolver component executes the scripts, with the Quotation Oracle providing the necessary gas and fee calculations and the Off-Chain Data Oracle supplying required external data.
- **Transaction Management:** The Transaction Manager ensures that all transactions are handled correctly as per the intent script across different blockchains.
- **Liquidity Provision:** The Liquidity Manager ensures there is sufficient liquidity to facilitate transactions, integrating with Mugen Pools and Aggregators/Fillers as needed.

### 4.3 Decentralised Gas Oracle

https://imgur.com/9e7868b8-e00e-4edd-94cf-5497d52ecc92

The Decentralized Gas Price Oracle system in the Mugen Network is designed to provide accurate and reliable gas price quotations for executing intents on the blockchain. This system involves multiple components working together to ensure the process is secure, decentralized, and efficient. Here’s a detailed explanation of the architecture and process:

**Quotation service**

The Quotation Service gets the gas price data by aggregating information from multiple individual gas price oracles. This service checks the correctness of the gas price data by comparing inputs from various oracles and provides a reliable quotation for transaction execution.

The service verifies the authenticity of the data by checking the signatures provided by each oracle using ECDSA.

## 5. Mugen Network

### 5.1 Protocol Overview

Mugen Network's protocol is designed to facilitate seamless cross-chain interactions and support complex workflows. It includes the Cross-chain Intent Framework, which abstracts user intents and provides a standardized interface for decentralized applications. The protocol ensures secure, efficient, and scalable execution of cross-chain workflows.

### 5.1 Core Product Stack

The Core Product Stack consists of several key components designed to facilitate efficient cross-chain interactions:

1. **GMP+ Intent Framework**: This is the backbone of Mugen Network, enabling seamless execution of cross-chain workflows.
2. **Decentralized Gas Oracle**: Provides reliable gas price quotations to ensure efficient and cost-effective transactions.
3. **Liquidity Pools**: Ensures sufficient liquidity for cross-chain transactions, integrating with external liquidity providers as needed.

Community Driven Products are designed to induce community participation and knowledge base expansion around the product and its ecosystem.  They include -

1. Marketplace for Scripts
2. IDE 
3. Gas Oracle 
4. Script Simulator 
5. TXN Explorer

