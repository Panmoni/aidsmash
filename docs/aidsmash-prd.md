# AidSmash Project Requirements Document
## 1. Mission and Vision
### Mission
AidSmash seeks to disrupt the global non-profit industry by providing a transparent, decentralized platform that connects non-profits directly with donors, leveraging Web3 technologies to ensure accountability, empower community governance, and enable milestone-based funding.

### Vision
To establish a worldwide ecosystem where non-profits of all sizes can efficiently raise funds, donors actively shape project outcomes through decentralized decision-making, and trust is fostered through transparent, verifiable progress—ultimately transforming the non-profit sector into a more equitable and impactful force.

## 2. Business Model
AidSmash operates as a decentralized platform with a token-based economy, designed to sustain operations while incentivizing participation. Key elements include:
- **Token Holder Voting**: Token holders, who demonstrate "skin in the game" (e.g., via staking or minimum holdings), vote on project suitability during a pre-submission phase, ensuring Sybil resistance and community oversight.
- **Transaction Fees**: A modest fee (e.g., 1-2%) on successful campaigns funds platform maintenance and development.
- **Milestone-Based Funding**: Funds are escrowed and released in tranches upon milestone completion, verified by a mini-DAO of donors, reducing scam risks.
- **Reputation System**: Non-profits earn reputation scores based on project success, unlocking higher funding limits and lower fees over time.
- **All-or-Nothing Funding**: Projects must raise their full amount within 4 weeks, or funds are returned, encouraging serious proposals.

## 3. Problem and Solution
### Problem
The non-profit sector suffers from:
- **Lack of Transparency**: Donors struggle to verify fund usage, eroding trust.
- **Inefficiencies**: High administrative overhead (10-15% of funds) and reliance on intermediaries limit resources for impact.
- **Accessibility Barriers**: Developing-world non-profits face restricted access to global donors and depend heavily on large, developed-world organizations.
- **Accountability Gaps**: Without oversight, funds can be misused, and projects may fail to deliver.

### Solution
AidSmash addresses these challenges by:
- **Decentralized Fundraising**: Connecting non-profits directly to donors via blockchain, bypassing middlemen.
- **Community Governance**: Token holders and donors vote on project suitability and milestone progress, ensuring credibility.
- **Milestone Funding**: Releasing funds only upon verified milestone completion, with first-time projects capped at $500 (developing world) or $1,000 (developed world).
- **Transparency Tools**: Public profiles and evidence uploads (video, photos, etc.) make progress visible to all.

## 4. Unique Value Proposition (UVP)
AidSmash stands out with:
- **Milestone Accountability**: Funds tied to verifiable progress reduce risks and build trust.
- **Community Empowerment**: Donors form mini-DAOs to oversee projects, giving them a direct role in outcomes.
- **Global Reach with Low Barriers**: Small initial funding caps enable first-time non-profits from any region to participate.
- **Reputation Incentives**: A transparent scoring system rewards success, fostering long-term accountability.

## 5. One-Liner
"Empowering non-profits with transparent, community-driven funding on Web3."

## 6. Target Market
- **Primary**: Non-profit organizations worldwide, especially small-to-medium entities in developing and developed regions seeking direct donor access.
- **Secondary**: Donors and philanthropists interested in transparent, impact-driven giving, particularly those open to Web3 technologies.
- **Geographic Focus**: Initial emphasis on regions with high non-profit activity and Web3 adoption (e.g., North America, Europe, Africa, Asia).

## 7. Competitive Advantage
AidSmash differentiates itself from traditional and Web3 fundraising platforms through:
- **Milestone-Based Oversight**: Combines community voting with staged funding to ensure accountability.
- **Sybil-Resistant Governance**: Token-based voting with "skin in the game" prevents manipulation.
- **Trust-Building for Newcomers**: Low initial funding caps ($500/$1,000) mitigate risks for untested non-profits.
- **Reputation Transparency**: Public scores incentivize performance and distinguish reliable organizations.

## 8. Technical Outline (System Architecture)
### 8.1 Blockchain and Smart Contracts
- **Blockchain**: Solana (chosen for low fees, fast transactions).
- **Smart Contracts** (Rust):
	- ProjectFactory.sol: Creates projects with milestones and funding goals.
	- FundingEscrow.sol: Escrows funds, releases tranches upon mini-DAO approval.
	- Governance.sol: Manages token holder voting for pre-submission and milestone verification.
	- Reputation.sol: Tracks and updates non-profit reputation scores.

### 8.2 Backend
- **Framework**: ExpressJS (Node.js) for API management and blockchain interaction.
- **Database**: PostgreSQL for off-chain data (e.g., project metadata, user profiles).

#### APIs:
- Project submission and management.
- Donation processing.
- Voting and milestone verification.
- Reputation queries.

### 8.3 Frontend
- **Framework**: Vite + React for a fast, responsive UI.
- **Components**:
	- Project creation and dashboard for non-profits.
	- Donor interface for browsing, donating, and voting.
	- Profile pages displaying reputation and project history.

### 8.4 Web3 Integration
- **Wallets**: MetaMask, WalletConnect for user connectivity.
- **Token**: ERC-20 governance token for voting and incentives.
- **Tools**: ethers.js for blockchain interactions.

## 9. Key Features for MVP
### 9.1 Project Submission and Pre-Submission
Non-profits submit proposals with:
- At least 3 milestones (first milestone ≤10% of total).
- Documentation (e.g., video, photos).
- Funding goal ($500/$1,000 cap for first-timers).
- Token holders vote on suitability in a Sybil-resistant pre-submission phase.

### 9.2 Funding Mechanics
- **All-or-Nothing**: Full amount must be raised within 4 weeks, or funds return to donors.
- **Escrow**: Initial 10% released upon funding success; subsequent tranches require mini-DAO approval.
- **Evidence Upload**: Non-profits submit proof (video, photos, etc.) for milestone completion.

### 9.3 Community Governance
- Donors form a mini-DAO per project, voting on milestone evidence sufficiency.
- Voting weighted by donation amount; approval triggers fund release.
- Projects failing timely evidence submission enter a suspended state.

### 9.4 Reputation and Profiles
- **Reputation Score**: Increases with successful milestones; impacts future funding limits.
- **Profile Page**: Displays past projects, reputation, and uploaded evidence for transparency.

## 10. Development Roadmap for MVP
### Phase 1: Core Setup (Weeks 1-3)
- Deploy Solana smart contracts (ProjectFactory, FundingEscrow).
- Build backend APIs for project submission.
- Create basic frontend for project creation and viewing.
### Phase 2: Governance Integration (Weeks 4-6)
- Implement Governance.sol for token holder voting.
- Add mini-DAO voting to frontend.
- Test pre-submission process.
### Phase 3: Milestone and Funding (Weeks 7-9)
- Enhance FundingEscrow.sol for milestone releases.
- Develop milestone tracking and evidence upload UI.
- Integrate donor voting interface.
### Phase 4: Reputation and Polish (Weeks 10-11)
- Deploy Reputation.sol and link to project outcomes.
- Build profile pages with reputation display.
- Refine UI/UX for usability.
### Phase 5: Testing and Launch (Weeks 12-14)
- Audit smart contracts for security.
- Conduct pilot with select non-profits.
- Launch MVP and onboard initial users.

## 11. Risks and Mitigation
- **Smart Contract Bugs**: Mitigate with audits and testing on Solana devnet.
- **Low Adoption**: Target Web3-savvy non-profits and donors initially; offer onboarding support.
- **Governance Abuse**: Use Sybil-resistant voting (e.g., token staking) and reputation weighting.
- **Regulatory Hurdles**: Consult legal experts for global compliance.

## 12. Success Metrics
- **Projects Funded**: Number of successful campaigns.
- **Funds Raised**: Total amount collected.
- **Donor Participation**: Unique donors and voting engagement.
- **Reputation Growth**: Average score increase for active non-profits.

## 13. Conclusion
AidSmash redefines non-profit fundraising by leveraging Solana, Rust smart contracts, and a Typescript-based frontend (Vite + React) to create a transparent, community-governed platform. With milestone-based funding, low entry barriers, and a reputation system, it empowers non-profits globally while ensuring donor trust and engagement. This document provides a clear roadmap for the MVP, balancing your vision with practical implementation steps to disrupt the non-profit sector in 2025 and beyond.




----



ong tiene que ser responsable.
  - misión (metadata)
  - representantes (personas)
  - proyectos
    - misión
    - entregables
    - plazo de tiempo
    - hitos
    - metadata como imagenes, una propuesta escrita, extensa, region geografica donde va a operar. 

    newsletter

usuarios (donante), dan fondos, quieren accountability.