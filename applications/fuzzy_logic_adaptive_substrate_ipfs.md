# Fuzzy Logic-Based Adaptive Blockchain Storage with Substrate and IPFS

- **Team Name:** Thandile Nododile (PhD Computer Science Candidate)
- **Payment Details:**
  - **DOT**: `14E7KnTayqveH8oGacW1FPYMSy1hPtV3sYoBwpBmZsq4tV9k`
  - **Payment**: `14E7KnTayqveH8oGacW1FPYMSy1hPtV3sYoBwpBmZsq4tV9k` (USDC)
- **Level:** 1

## Project Overview :page_facing_up:

### Overview

This research project develops a **fuzzy logic-based adaptive storage optimization layer** for Substrate blockchain integrated with IPFS. Building on proven prior work (MSc thesis + 3 peer-reviewed publications), this research introduces intelligent, dynamic storage management that automatically adjusts to varying workloads, network conditions, and data characteristics.

The project extends the Polkadot/Substrate ecosystem by creating a novel adaptive pallet that uses fuzzy logic inference to optimize when, where, and how data is distributed between on-chain storage and IPFS, significantly improving storage efficiency, throughput, and scalability for IoT and data-intensive applications.

### Project Details

#### Problem Statement

Current blockchain-IPFS integrations use static storage policies that cannot adapt to:
- Varying data sizes and types (numerical readings vs. images vs. sensor streams)
- Fluctuating network conditions and node availability
- Different priority levels for data integrity vs. retrieval speed
- Dynamic workload patterns in IoT applications

Our prior research (MSc thesis, 2025) demonstrated that Substrate-IPFS hybrid systems outperform Ethereum-IPFS in storage efficiency and throughput. However, the storage allocation decisions were manually configured, creating a bottleneck for real-world deployment at scale.

#### Proposed Solution

We propose a **fuzzy logic adaptive controller** integrated as a Substrate pallet that:

1. **Monitors** system state variables (data size, network latency, node count, throughput)
2. **Infers** optimal storage decisions using fuzzy rules (e.g., IF data_size is LARGE AND network_latency is LOW THEN prefer_ipfs is HIGH)
3. **Adapts** storage allocation dynamically without manual intervention
4. **Optimizes** the balance between on-chain integrity verification and off-chain IPFS storage

#### Technical Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     Substrate Runtime                           │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │              Fuzzy Logic Adaptive Pallet                 │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐  │   │
│  │  │ Fuzzifier   │→ │ Inference   │→ │ Defuzzifier     │  │   │
│  │  │ (Input)     │  │ Engine      │  │ (Output)        │  │   │
│  │  └─────────────┘  └─────────────┘  └─────────────────┘  │   │
│  │         ↑                                    ↓          │   │
│  │  ┌─────────────┐              ┌─────────────────────┐   │   │
│  │  │ State       │              │ Storage Decision    │   │   │
│  │  │ Monitor     │              │ Executor            │   │   │
│  │  └─────────────┘              └─────────────────────┘   │   │
│  └─────────────────────────────────────────────────────────┘   │
│                              ↓                                  │
│  ┌─────────────────┐    ┌─────────────────┐                    │
│  │ On-Chain        │    │ IPFS Off-Chain  │                    │
│  │ (CID + Metadata)│    │ (Raw Data)      │                    │
│  └─────────────────┘    └─────────────────┘                    │
└─────────────────────────────────────────────────────────────────┘
```

#### Fuzzy Logic System Design

**Input Variables (Fuzzified):**
| Variable | Fuzzy Sets | Description |
|----------|------------|-------------|
| data_size | SMALL, MEDIUM, LARGE | Size of incoming data payload |
| network_latency | LOW, MEDIUM, HIGH | Current network response time |
| node_availability | LOW, MODERATE, HIGH | Active nodes in the network |
| data_priority | LOW, NORMAL, CRITICAL | Application-defined importance |

**Output Variable:**
| Variable | Fuzzy Sets | Description |
|----------|------------|-------------|
| storage_preference | ONCHAIN_FULL, HYBRID, IPFS_FULL | Where to store data |

**Sample Fuzzy Rules:**
```
IF data_size IS SMALL AND data_priority IS CRITICAL THEN storage_preference IS ONCHAIN_FULL
IF data_size IS LARGE AND network_latency IS LOW THEN storage_preference IS IPFS_FULL
IF data_size IS MEDIUM AND node_availability IS HIGH THEN storage_preference IS HYBRID
```

#### Technology Stack
- **Blockchain Framework**: Substrate (Polkadot SDK)
- **Programming Languages**: Rust, Python
- **Off-chain Storage**: IPFS with Blake2 hashing
- **Fuzzy Logic**: Custom implementation in Rust (no_std compatible)
- **Testing**: Smart water meter data + infrared images (existing datasets from prior work)

#### Prior Work & Validation

This project builds directly on completed, peer-reviewed research:

| Prior Work | Contribution | Validation |
|------------|--------------|------------|
| MSc Thesis (2025) | Substrate-IPFS hybrid architecture, 10-node deployment, performance benchmarking | University of the Western Cape |
| IST-Africa 2023 | Blockchain-based secure data collection for IoT | IEEE published, doi: 10.23919/IST-Africa60249.2023.10187803 |
| ETNCC 2024 | Substrate + IPFS integration methodology | IEEE published, doi: 10.1109/ETNCC63262.2024.10767518 |
| IST-Africa 2025 | Hybrid blockchain-IPFS solution validation | IEEE published, doi: 10.23919/IST-Africa67297.2025.11060537 |

**Key Results from Prior Work:**
- Substrate-IPFS achieved **40% lower block sizes** than Ethereum-IPFS
- **Faster block confirmation times** (consistent 6-second blocks vs. variable Ethereum times)
- **Scalable performance** maintained across 3-10 node configurations
- Successfully handled **numerical data** (smart meter readings) and **image data** (infrared images)

#### What This Project Is NOT

- This is NOT a new blockchain or parachain
- This is NOT a token project
- This does NOT replace existing Substrate storage mechanisms
- This does NOT require any protocol-level changes to Polkadot

### Ecosystem Fit

#### Where and How Does This Fit?

This project fits into the **Polkadot infrastructure/tooling layer**, specifically:
- Enhances Substrate's data storage capabilities
- Provides reusable pallet for the ecosystem
- Addresses DePIN/IoT data management (W3F priority area)

#### Target Audience

1. **Substrate developers** building data-intensive dApps
2. **IoT/DePIN projects** on Polkadot requiring efficient data storage
3. **Researchers** working on blockchain scalability
4. **Enterprises** considering Polkadot for supply chain, healthcare, or smart city applications

#### What Need Does This Address?

The Polkadot ecosystem lacks **adaptive, intelligent storage optimization** for hybrid on-chain/off-chain architectures. Current solutions require manual configuration, limiting:
- Automatic scaling for variable workloads
- Optimization for different data types
- Self-tuning based on network conditions

#### Similar Projects

| Project | Difference from Our Work |
|---------|--------------------------|
| Crust Network | Focuses on decentralized storage incentives, not adaptive decision-making |
| CESS | Storage infrastructure, no fuzzy logic optimization |
| Generic IPFS pallets | Static storage policies without adaptive intelligence |

Our project is unique in applying **fuzzy logic control theory** to blockchain storage optimization, a novel approach not present in the current ecosystem.

## Team :busts_in_silhouette:

### Team Members

- **Thandile Nododile** - Lead Researcher & Developer
- **Prof. Clement N. Nyirenda** - Academic Supervisor & Research Advisor

### Contact

- **Contact Name:** Thandile Nododile
- **Contact Email:** 3692513@myuwc.ac.za
- **Website:** N/A (Academic research team)

### Legal Structure

- **Registered Address:** N/A (University-affiliated research)
- **Registered Legal Entity:** N/A (Individual grant with academic supervision)

### Team's Experience

**Thandile Nododile** (Lead Researcher & Software Dev Engineer)

- **Current**: PhD Candidate, Computer Science, University of the Western Cape
  - Research Focus: Fuzzy Logic-Based Adaptive Blockchain Storage Systems
- **Education**: 
  - MSc in Computer Science, University of the Western Cape, Cape Town, South Africa
  - BSc(Honours) in Computer Science, University of the Western Cape, Cape Town, South Africa
  - BSc Mathematics Statistical Science (Cum Laude), University of the Western Cape, Cape Town, South Africa
- **Technical Skills**: Substrate/Rust development, Python, IPFS integration, blockchain architecture
- **Role in Project**: Primary developer, implementation, testing, and documentation
- **Google Scholar**: https://scholar.google.com/citations?user=5npb5C0AAAAJ&hl=en

**Prof. Clement N. Nyirenda** (Academic Supervisor & Research Advisor)

- **Current**: Director of eResearch, University of the Western Cape (since August 2023)
- **Previous**: Senior Lecturer & Acting Head of Department, Computer Science, UWC
- **Education**: 
  - PhD in Computational Intelligence and Systems Science, Tokyo Institute of Technology
  - MScEng in Computer Engineering, University of KwaZulu-Natal
  - BSc in Electrical Engineering, University of Malawi
- **Research Interests**: Machine Learning, Computer Vision, Computational Intelligence, Blockchain Applications
- **Relevant Experience**: Active researcher in blockchain-powered platforms; recently presented on blockchain for agricultural applications at Food Indaba 2025
- **Role in Project**: Research direction, methodology oversight, quality assurance, academic validation
- **Google Scholar**: https://scholar.google.com/citations?user=G0d8UFEAAAAJ

**Research since 2022, resulting in:**
- 1 completed MSc thesis
- 3 co-authored peer-reviewed IEEE publications
- Ongoing PhD supervision

This established research partnership ensures continuity, quality, and successful delivery.

**Joint Publications:**

1. T. Nododile and C. Nyirenda, "A Blockchain-Based Secure Data Collection Mechanism for Smart Water Meters," IST-Africa 2023, IEEE, doi: 10.23919/IST-Africa60249.2023.10187803

2. T. Nododile and C. N. Nyirenda, "Advancing Blockchain-Enabled InterPlanetary File System with Substrate for Distributed Data Storage," ETNCC 2024, IEEE, doi: 10.1109/ETNCC63262.2024.10767518

3. T. Nododile and C. Nyirenda, "A Hybrid Blockchain-IPFS Solution for Secure and Scalable Data Collection and Storage in Smart Water Meters," IST-Africa 2025, IEEE, doi: 10.23919/IST-Africa67297.2025.11060537

### Team Code Repos

- https://github.com/6636345e

### Team LinkedIn Profiles

- Thandile Nododile: https://www.linkedin.com/in/6636345e/
- Prof. Clement Nyirenda: https://www.linkedin.com/in/nthambazale/

## Development Status :open_book:

### Prior Research Completed

This grant application builds on **completed and validated research**:

1. **MSc Thesis (March 2025)**: "Substrate Blockchain-Enabled InterPlanetary File System for Distributed Data Storage" - 100+ pages, comprehensive implementation and evaluation

2. **Working Codebase**: Existing Substrate-IPFS integration with:
   - Custom Substrate pallet for IPFS CID storage
   - Blake2 hashing integration
   - Multi-node deployment scripts
   - Performance benchmarking tools

3. **Datasets**: Real-world smart water meter data (numerical) and infrared medical images (binary) already prepared and tested

4. **Benchmarks**: Comparative analysis against Ethereum-IPFS completed, demonstrating Substrate superiority

### Research Gap Identified

The MSc thesis explicitly identified the need for **"mechanisms for dynamic addition or removal of nodes based on workload to ensure consistent performance and scalability"** (Future Works Section). The proposed fuzzy logic layer directly addresses this gap.

## Development Roadmap :nut_and_bolt:

### Overview

- **Total Estimated Duration:** 4 months
- **Full-Time Equivalent (FTE):** 1.0
- **Total Costs:** $10,000 USD

### Milestone 1 - Fuzzy Logic Engine Core

- **Estimated duration:** 2 months
- **FTE:** 1.0
- **Costs:** 5,000 USD

| Number | Deliverable | Specification |
|--------|-------------|---------------|
| **0a.** | License | Apache 2.0 |
| **0b.** | Documentation | Inline code documentation + README with architecture explanation |
| **0c.** | Testing Guide | Unit tests with >80% coverage, integration test guide |
| **0d.** | Docker | Dockerfile for running fuzzy logic engine tests |
| **1.** | Fuzzy Logic Library | Rust library (no_std compatible) implementing: fuzzification, Sugeno fuzzy inference engine, defuzzification |
| **2.** | Rule Configuration | JSON/TOML configuration format for fuzzy rules with validation |
| **3.** | Benchmark Suite | Performance benchmarks comparing fuzzy inference times |

### Milestone 2 - Substrate Pallet Integration

- **Estimated duration:** 2 months
- **FTE:** 1.0
- **Costs:** 5,000 USD

| Number | Deliverable | Specification |
|--------|-------------|---------------|
| **0a.** | License | Apache 2.0 |
| **0b.** | Documentation | Pallet documentation + integration guide |
| **0c.** | Testing Guide | Pallet unit tests + runtime integration tests |
| **0d.** | Docker | Dockerfile for running Substrate node with adaptive pallet |
| **0e.** | Article | Technical article explaining the project (Medium or similar) |
| **1.** | Adaptive Storage Pallet | Substrate pallet integrating fuzzy logic engine with: storage preference calculation, IPFS CID management, on-chain metadata storage |
| **2.** | State Monitoring | Off-chain worker for monitoring network conditions and data characteristics |
| **3.** | Basic Evaluation | Performance comparison: adaptive vs. static storage using existing smart water meter dataset |
| **4.** | Tutorial | Step-by-step guide for integrating the adaptive pallet into Substrate projects |

## Future Plans

### Short-term (Post-Grant / Follow-up Grant)

- **Comprehensive evaluation**: Extended testing with multiple datasets (infrared images, real-time IoT streams)
- **Research paper**: Submit to IEEE/ACM blockchain conference (WCCI 2026 target)
- **Community feedback**: Iterate on pallet design based on developer input
- Complete PhD thesis chapter on adaptive storage systems

### Long-term

- Propose pallet for inclusion in Substrate FRAME pallets library
- Explore integration with Polkadot parachains (Crust, CESS)
- Extend fuzzy logic system to handle cross-chain storage decisions
- Develop GUI dashboard for monitoring adaptive decisions

### Sustainability

- PhD completion ensures continued maintenance
- Professional blockchain developer role provides ongoing ecosystem involvement
- Open-source licensing enables community contributions

## Referral Program (optional) :moneybag:

- **Referrer:** N/A
- **Payment Address:** N/A

## Additional Information :heavy_plus_sign:

### How Did You Hear About the Grants Program?

Web3 Foundation website and Polkadot documentation research during PhD literature review.

### Additional Context

**Why This Research Matters for Polkadot:**

1. **DePIN/IoT Relevance**: W3F has identified DePIN as a priority area. This research provides practical infrastructure for IoT data management on Polkadot.

2. **African Research Context**: Conducted at University of the Western Cape, South Africa, contributing to blockchain research capacity in emerging markets.

3. **Proven Track Record**: Unlike many grant applications, this project has **already demonstrated results** through peer-reviewed publications and a completed MSc thesis.

4. **Practical Application**: Smart water meter use case addresses real infrastructure challenges in developing regions while validating the technology.

5. **Academic Rigour**: Supervised by Prof. Clement N. Nyirenda (Director of eResearch, UWC; PhD Tokyo Institute of Technology), ensuring research quality, methodology, and international standards. This is an established 3+ year research partnership with proven publication output.

**What Has Already Been Done:**
- ✅ 3 peer-reviewed IEEE publications
- ✅ Performance benchmarking vs. Ethereum (completed)
- ✅ Real-world datasets (smart meter + medical images)

**What This Grant Funds:**
- 🔲 Fuzzy logic adaptive layer (novel contribution)
- 🔲 Dynamic storage optimization
- 🔲 Substrate pallet implementation
- 🔲 Evaluation and documentation
