# Decode Network

> **An open-source, hybrid Web2-Web3 platform for decentralized identity, secure communication, and community coordination**

[![Production](https://img.shields.io/badge/Production-Live-brightgreen)](https://decode.decodenetwork.app)
[![License](https://img.shields.io/badge/License-MIT-blue)](LICENSE)
[![Architecture](https://img.shields.io/badge/Architecture-Microservices-orange)](docs/decode)

---

## 🎯 The Problem

Web3 promises user ownership, yet most developer communities remain on Web2 platforms where identity, data, and governance are centralized—fragmenting collaboration and limiting verifiable reputation. When Web3 projects depend on Web2 infrastructure, they introduce centralization risks into ostensibly decentralized ecosystems.

**Key Challenges:**
- **Fragmented Identity**: Developer reputation on Discord doesn't transfer to GitHub; contributions are invisible across platforms
- **Centralization Risks**: Discord servers can be banned, GitHub repositories removed, leaving communities without recourse
- **No Verifiable Reputation**: No mechanism for developers to build verifiable on-chain reputation based on contributions and skills
- **Limited Interoperability**: Existing solutions lack open APIs and composable architectures
- **Scalability vs. Decentralization Trade-offs**: Pure blockchain solutions face performance limitations, while pure Web2 solutions sacrifice verifiability

## ✨ The Solution

**Decode Network** addresses these challenges with a pragmatic hybrid architecture that combines the performance and familiarity of Web2 infrastructure with progressive Web3 features for identity, reputation, and coordination.

Builders can **plug in or fork** Decode's ecosystem apps—**DeHive** (community development/coordination) and **DEiD** (user identity/reputation)—and compose them into their own products. Open-source teams can build directly on top of Decode's batteries-included primitives instead of rebuilding them.

---

## 🏗️ Architecture Overview

Decode Network comprises three interconnected ecosystem applications:

### 1. **Decode Portal** (Web2 Foundation)
The main application providing secure authentication, social graph functionality, and a hardened client-server protocol.

**Key Features:**
- Multi-factor authentication (email/password, TOTP 2FA, wallet-based SSO)
- Social graph with relationship mapping (following, connections)
- Real-time notifications via WebSocket
- Profile aggregation (Web2 + Web3 data)
- Device fingerprinting and session management

**Technology:** NestJS microservices, MongoDB, Neo4j, Redis, RabbitMQ

### 2. **DEiD** (Decentralized Identity)
A FastAPI-based system integrated with EVM smart contracts using the EIP-2535 Diamond Standard.

**Key Features:**
- On-chain user profiles with W3C DID compliance
- Verifiable badge system with validator signatures
- Reputation scoring with Merkle-based snapshots
- Social account linking with cryptographic attestation
- Portable, verifiable identity across platforms

**Technology:** FastAPI, Solidity (Diamond Standard), IPFS, The Graph

### 3. **DeHive** (Community Coordination)
A fully on-chain community platform with privacy-preserving messaging and payment capabilities.

**Key Features:**
- End-to-end encrypted messaging (AES-256)
- Native and ERC20 token payments in chat
- Gas-efficient token airdrops (EIP-1167 clone pattern)
- Payment permits (EIP-2612) for gasless approvals
- Deterministic conversation IDs and key management

**Technology:** Solidity (Diamond Standard), The Graph subgraphs, IPFS

---

## 🚀 Key Features

### Authentication & Security
- ✅ **Hybrid Authentication**: Email/password or wallet signature verification
- ✅ **TOTP Two-Factor Authentication**: Time-based one-time passwords for enhanced security
- ✅ **Wallet SSO**: Single Sign-On across Portal, DEiD, and DeHive
- ✅ **Device Fingerprinting**: Advanced session security
- ✅ **JWT with RSA-256**: Industry-standard token-based authentication

### Decentralized Identity (DEiD)
- ✅ **On-Chain Profiles**: User-owned identity on Ethereum (Sepolia testnet)
- ✅ **Verifiable Badges**: Cryptographic attestation of achievements
- ✅ **Reputation Scores**: Transparent, verifiable scoring system
- ✅ **Social Account Linking**: Connect Web2 accounts with cryptographic proof
- ✅ **W3C DID Compliance**: Standards-based decentralized identifiers

### Community Coordination (DeHive)
- ✅ **End-to-End Encrypted Messaging**: Privacy-preserving communication
- ✅ **In-Chat Payments**: Send native ETH or ERC20 tokens directly in conversations
- ✅ **Gas-Efficient Airdrops**: ~97% gas savings using EIP-1167 clone pattern
- ✅ **Payment Permits**: Gasless token approvals via EIP-2612
- ✅ **On-Chain Verifiability**: All messages and payments are verifiable on-chain

### Infrastructure & Observability
- ✅ **Microservices Architecture**: 6 independently deployable services
- ✅ **Real-Time Monitoring**: Datadog dashboards for business metrics, performance, and system health
- ✅ **Smart Contract Monitoring**: Real-time on-chain analytics for DEiD and DeHive contracts
- ✅ **CI/CD Pipeline**: Automated testing, building, and deployment via GitHub Actions
- ✅ **IPFS Integration**: Self-hosted IPFS node for decentralized content storage

---

## 🎓 Technical Problems Solved

### 1. **Smart Contract Gas Optimization**
**Problem:** Initial airdrop implementation consumed excessive gas, making large distributions impractical.

**Solution:** Implemented EIP-1167 minimal proxy pattern (clone factories), achieving **~97% gas savings** compared to traditional deployment methods.

**Impact:** Enabled cost-effective token distributions for community rewards and airdrops.

### 2. **Inter-Service Data Consistency**
**Problem:** Maintaining consistency between MongoDB (user profiles) and Neo4j (relationships) in a microservices architecture.

**Solution:** Implemented eventual consistency with Redis-based cache invalidation and background synchronization jobs.

**Impact:** Achieved sub-500ms API latency while maintaining data integrity across distributed services.

### 3. **Hybrid Web2-Web3 Authentication**
**Problem:** Balancing user experience (Web2 familiarity) with decentralization (Web3 ownership).

**Solution:** Built flexible authentication supporting both email/password and wallet signature verification, with seamless SSO across all ecosystem apps.

**Impact:** 93% of users appreciated the hybrid approach, with 67% using wallet authentication as primary method.

### 4. **End-to-End Encrypted On-Chain Messaging**
**Problem:** Providing privacy-preserving messaging while maintaining on-chain verifiability.

**Solution:** Implemented symmetric encryption (AES-256) with per-user encrypted keys stored on-chain, ensuring message privacy with deterministic conversation IDs.

**Impact:** 80% of users appreciated the encryption and on-chain verifiability features.

### 5. **Scalable Blockchain Indexing**
**Problem:** Real-time querying of on-chain events for DeHive messaging, payments, and airdrops.

**Solution:** Built three Graph Protocol subgraphs (dehive-messaging, dehive-payment, dehive-airdrop) with deterministic event indexing.

**Impact:** Achieved 100% deterministic event indexing with <2 block latency.

### 6. **Modular Smart Contract Architecture**
**Problem:** Managing multiple logical modules (Profile, Badge, Score, Message, PaymentHub) with shared state and upgradeability.

**Solution:** Adopted EIP-2535 Diamond Standard, enabling modular facets with shared storage and upgradeability without state migration.

**Impact:** Reduced code duplication, enabled iterative development, and maintained upgradeability without redeployment.

---

## 📊 Performance Metrics

| Metric | Target | Achieved | Status |
|--------|--------|----------|--------|
| **API Latency (Median)** | <500ms | <500ms | ✅ |
| **Test Pass Rate** | ≥95% | ≥95% | ✅ |
| **System Uptime** | ≥99% | 99.7% | ✅ |
| **Event Indexing Latency** | <2 blocks | <2 blocks | ✅ |
| **User Satisfaction** | ≥4.0/5.0 | 4.3/5.0 | ✅ |
| **Task Completion Rate** | ≥90% | 94% | ✅ |
| **Request Throughput** | - | 60,000 requests/day | ✅ |

**Production Performance (1-month observation):**
- Successfully handled 60,000+ requests/day with stable performance
- 95th percentile API latency <1s
- Database query response times <200ms for 95% of requests
- Zero high-severity vulnerabilities identified

---

## 🛠️ Technology Stack

### Web2 Layer
- **Backend Framework:** NestJS (TypeScript)
- **Identity Service:** FastAPI (Python)
- **Databases:** MongoDB, Neo4j, Redis
- **Message Queue:** RabbitMQ
- **CI/CD:** GitHub Actions, Docker
- **Infrastructure:** Google Cloud Platform (GCP), DigitalOcean
- **Monitoring:** Datadog (APM, Logs, Metrics)

### Web3 Layer
- **Smart Contracts:** Solidity with EIP-2535 (Diamond Standard)
- **Storage:** IPFS (InterPlanetary File System)
- **Indexing:** The Graph Protocol (3 subgraphs)
- **Network:** Ethereum Sepolia Testnet
- **Frontend:** Next.js with Web3 integration

### Security & Standards
- **Authentication:** JWT (RSA-256), TOTP, OAuth 2.0
- **Encryption:** AES-256, RSA-256, HTTPS
- **Standards:** W3C DIDs, EIP-2535, EIP-1167, EIP-2612
- **Security:** OWASP Top 10 compliance, OpenZeppelin patterns

---

## 🏛️ Architecture Highlights

### Microservices Design
- **6 Independent Services:** API Gateway, Auth, User, Wallet, Relationship, Notification
- **Domain Separation:** Each service encapsulates distinct business logic
- **Technology Flexibility:** Different data stores optimized per service
- **Independent Scaling:** High-traffic services scale independently

### Diamond Standard Implementation
- **Modular Facets:** Profile, Badge, Score, Message, PaymentHub
- **Shared Storage:** Efficient state management across facets
- **Upgradeability:** Add, replace, or remove facets without redeployment
- **Gas Efficiency:** Shared libraries reduce code duplication

### Hybrid Architecture Benefits
- **Performance:** Sub-500ms API latency (Web2 speed)
- **Verifiability:** On-chain identity and reputation (Web3 trust)
- **User Experience:** Familiar Web2 patterns with progressive Web3 enhancement
- **Composability:** Open APIs and SDKs for extension

---

## 🌐 Open Source & Composable

Decode Network is designed for **inheritance and extension**. Builders can:

- **Plug In:** Use Decode's ecosystem apps as drop-in components
- **Fork:** Customize and extend DeHive or DEiD for specific needs
- **Compose:** Build new products on top of Decode's primitives
- **Extend:** Leverage open APIs and SDKs for integration

**No Vendor Lock-in:** Decode operates as a reference implementation, foundation, or component—not a "super app" that locks users in.

---

## 📚 Documentation

Comprehensive documentation is available in the [docs](./docs) directory:

- **Architecture Diagrams:** C4 model visualizations (Context, Container, Component)
- **Feature Flows:** 78+ sequence diagrams documenting all major features
- **Database Schemas:** ERD diagrams for MongoDB and Neo4j
- **API Documentation:** RESTful APIs and GraphQL endpoints
- **Smart Contract Documentation:** Contract interfaces and deployment guides

---

## 🚦 Getting Started

### Prerequisites
- Node.js 18.x
- Python 3.11
- Docker & Docker Compose
- Hardhat (for smart contract development)
- Sepolia testnet ETH (for on-chain interactions)

### Quick Start
```bash
# Clone repositories
git clone https://github.com/decodenetwork/portal.git
git clone https://github.com/decodenetwork/deid.git
git clone https://github.com/decodenetwork/dehive.git

# Follow setup instructions in each repository
```

### Production Deployment
Visit **[https://decode.decodenetwork.app](https://decode.decodenetwork.app)** to experience the live system.

---

## 🤝 Contributing

We welcome contributions! Decode Network is built for the community, by the community.

- **Report Issues:** Open GitHub issues for bugs or feature requests
- **Submit PRs:** Follow our contribution guidelines
- **Join Discussions:** Participate in architecture and feature discussions
- **Build Extensions:** Create your own apps using Decode's primitives

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔗 Links

- **Production:** [https://decode.decodenetwork.app](https://decode.decodenetwork.app)
- **Documentation:** [docs/](./docs)
- **Report:** [REPORT.md](./REPORT.md)

---

## 📧 Contact

**Nguyen Dinh Hoang Son**
Email: pason.dev@gmail.com

---

**Built with ❤️ for the Web3 developer community**

*Decode Network demonstrates that decentralized identity and collaboration can coexist with pragmatic, scalable Web2—using separation of concerns, open standards, and public APIs/SDKs to provide a composable base others can extend for transparent coordination and faster open innovation.*

