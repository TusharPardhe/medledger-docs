# MedLedger

#### Your health. Your data. Your control.

[![Next.js](https://img.shields.io/badge/Next.js-19.0-black)](https://nextjs.org/)
[![XRPL](https://img.shields.io/badge/XRPL-Blockchain-blue)](https://xrpl.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.8-blue)](https://www.typescriptlang.org/)
[![Prisma](https://img.shields.io/badge/Prisma-6.12-2D3748)](https://www.prisma.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4.1-38B2AC)](https://tailwindcss.com/)

> **Empowering patients with true ownership of their medical data through blockchain technology**

MedLedger is a decentralised electronic health record management platform that leverages the XRP Ledger (XRPL) to give patients complete control over their medical records. Built with privacy-first principles, cryptographic security, and seamless healthcare integration.

---

## Key Features

### **Patient Data Ownership**

-   **True Data Sovereignty**: Patients own and control access to their medical records
-   **IPFS Storage**: Medical data encrypted and stored on decentralized IPFS network
-   **NFT Certificates**: Each medical record minted as an NFT on XRPL for immutable ownership
-   **Privacy-First Design**: Only metadata stored in database, actual data encrypted off-chain

### **Cryptographic Consent Protocol**

-   **Bidirectional Consent**: Advanced cryptographic consent mechanism
-   **Time-Bound Access**: Automatic expiration of data access permissions
-   **Granular Control**: Patients can grant access to specific data types
-   **Real-Time Notifications**: Instant alerts for access requests and data usage

### **Hybrid Payment System**

-   **Multi-Currency Support**: FIAT (USD, EUR) and Crypto (XRP, RLUSD)
-   **XRPL Payments**: Native integration with XRP Ledger for micro-transactions
-   **RippleNet Integration**: Institutional payment infrastructure (planned)
-   **Payment Escrow**: Smart contract-based escrow for data sharing agreements

---

## Architecture Overview

MedLedger implements a sophisticated microservices architecture with comprehensive healthcare standards compliance:

### **System Architecture**

```mermaid
flowchart TD
    subgraph "Frontend Layer"
        WEB[Web Application]
        MOBILE[Mobile PWA]
        API_DOCS[API Documentation]
    end

    subgraph "API Gateway"
        GATEWAY[Load Balancer]
        AUTH[Authentication]
        RATE[Rate Limiting]
    end

    subgraph "Core Services"
        PATIENT[Patient Service]
        PROVIDER[Provider Service]
        RECORDS[Records Service]
        ACCESS[Access Control]
        XRPL_SVC[XRPL Service]
    end

    subgraph "Data Layer"
        POSTGRES[(PostgreSQL)]
        IPFS[IPFS Cluster]
        XRPL[XRP Ledger]
    end

    WEB --> GATEWAY
    MOBILE --> GATEWAY
    GATEWAY --> AUTH
    AUTH --> PATIENT
    AUTH --> PROVIDER
    PATIENT --> POSTGRES
    RECORDS --> IPFS
```

---

## User Journey Flows

### 1. Patient Onboarding & XRPL Wallet Creation

```mermaid
flowchart TD
    A[User Registration] --> B[Email Verification]
    B --> C[Login to Dashboard]
    C --> D[6-Step Onboarding Modal]
    D --> E[Personal Information]
    E --> F[Location Details]
    F --> G[Medical Data Types]
    G --> H[Specialties Selection]
    H --> I[XRPL Wallet Generation]
    I --> J[Wallet Confirmation]
    J --> K[Onboarding Complete]

    I --> L[Connect to XRPL Testnet]
    L --> M[Generate Cryptographic Keys]
    M --> N[Fund with Test XRP]
    N --> O[Store Wallet Address]
```

### 2. Medical Record Upload & NFT Minting

```mermaid
flowchart TD
    A[Patient Uploads Document] --> B[Client-Side Encryption]
    B --> C[Upload to IPFS]
    C --> D[Generate IPFS Hash]
    D --> E[Create NFT Metadata]
    E --> F[Mint NFT on XRPL]
    F --> G[Store NFT Token ID]
    G --> H[Update Dashboard]

    C --> I[IPFS Node 1]
    C --> J[IPFS Node 2]
    C --> K[IPFS Node 3]
```

### 3. Cryptographic Consent Protocol

```mermaid
flowchart TD
    subgraph "Provider Side"
        A[Provider Search] --> B[Find Patient]
        B --> C[Request Data Access]
        C --> D[Submit to XRPL]
    end

    subgraph "Patient Side"
        E[Receive Notification] --> F[Review Request]
        F --> G{Grant Access?}
        G -->|Yes| H[Generate Access Keys]
        G -->|No| I[Deny Request]
    end

    D --> E
    H --> J[Encrypt AES Key]
    J --> K[Create Active Access]
    K --> L[Provider Access Granted]
```

---

## Technology Stack

### **Frontend**

-   **Next.js 19.0** - React framework with App Router
-   **React 19.0** - Modern React with Server Components
-   **TypeScript 5.8** - Type-safe development
-   **Tailwind CSS 4.1** - Utility-first CSS framework
-   **Framer Motion** - Smooth animations and transitions
-   **Lucide React** - Beautiful icons and UI elements

### **Backend**

-   **Next.js API Routes** - Serverless API endpoints
-   **Prisma 6.12** - Type-safe database ORM
-   **PostgreSQL** - Primary database
-   **NextAuth.js** - Authentication framework
-   **JWT** - Secure token-based authentication
-   **Zod** - Runtime type validation

### **Blockchain & Storage**

-   **XRPL (XRP Ledger)** - Blockchain infrastructure
-   **IPFS** - Decentralized file storage
-   **NFT.Storage** - IPFS pinning service
-   **Crypto-JS** - Client-side encryption

### **Healthcare Integration**

-   **FHIR R4** - Healthcare data standards
-   **HL7** - Healthcare messaging standards
-   **DICOM** - Medical imaging standards
-   **SMART on FHIR** - Healthcare app platform

### **Security & Compliance**

-   **bcrypt** - Password hashing
-   **JOSE** - JWT encryption/decryption
-   **HIPAA/GDPR** - Privacy compliance
-   **Audit Logging** - Complete access trails

---

## Project Structure

```
medledger/
├── 📁 src/
│   ├── 📁 app/                          # Next.js App Router
│   │   ├── 📁 api/                      # API endpoints
│   │   │   ├── 📁 auth/                 # Authentication APIs
│   │   │   │   ├── login/route.ts       # User login
│   │   │   │   ├── register/route.ts    # User registration
│   │   │   │   ├── verify-email/route.ts # Email verification
│   │   │   │   └── resend-verification/ # Resend verification
│   │   │   ├── 📁 medledger/           # Core platform APIs
│   │   │   │   ├── 📁 auth/            # XRPL authentication
│   │   │   │   ├── 📁 patient/         # Patient services
│   │   │   │   │   ├── onboarding/     # Patient onboarding
│   │   │   │   │   └── approve-access/ # Access approval
│   │   │   │   ├── 📁 records/         # Medical records
│   │   │   │   └── 📁 providers/       # Provider services
│   │   │   ├── 📁 xrpl/                # XRPL integration
│   │   │   └── 📁 user/                # User management
│   │   ├── 📁 dashboard/               # Patient dashboard
│   │   ├── 📁 records/                 # Medical records UI
│   │   ├── 📁 profile/                 # User profile
│   │   ├── 📁 login/                   # Authentication pages
│   │   ├── 📁 register/                # Registration pages
│   │   └── 📁 docs/                    # Documentation
│   ├── 📁 components/                   # React components
│   │   ├── 📁 ui/                      # Base UI components
│   │   └── 📁 medledger/               # Platform components
│   │       ├── 📁 onboarding/          # Onboarding components
│   │       ├── 📁 dashboard/           # Dashboard components
│   │       └── 📁 records/             # Records components
│   ├── 📁 lib/                         # Utility libraries
│   │   ├── auth.ts                     # Authentication logic
│   │   ├── xrpl-service.ts            # XRPL integration
│   │   ├── secure-storage.ts          # Encryption utilities
│   │   ├── email-service.ts           # Email notifications
│   │   └── schema-services.ts         # Database services
│   ├── 📁 types/                       # TypeScript definitions
│   └── middleware.ts                   # Request middleware
├── 📁 prisma/                          # Database
│   ├── schema.prisma                   # Database schema
│   ├── migrations/                     # Database migrations
│   └── seed.ts                         # Database seeding
├── 📁 docs/                            # Documentation
│   └── flow-diagrams.md               # Technical diagrams
├── 📁 scripts/                         # Utility scripts
└── 📁 public/                          # Static assets
```

---

## Database Schema

MedLedger uses a privacy-first database design where only metadata and access controls are stored:

### **Core Models**

-   **Patient** - User identity and XRPL wallet information
-   **HealthcareProvider** - Verified medical professionals
-   **PatientDataNft** - References to IPFS-stored medical data
-   **DataAccessRequest** - Provider requests for patient data
-   **ActiveDataAccess** - Active permissions and encrypted keys
-   **DataAccessLog** - Complete audit trail

### **Schema Highlights**

```prisma
model Patient {
    id                      String    @id @default(uuid())
    patientId               String    @unique // ML-2024-001234
    email                   String    @unique
    walletAddress           String    @unique // XRPL address
    encryptedSecretHash     String?   // Password hash
    profileNftTokenId       String?   // XRPL NFT ID
    isSearchable            Boolean   @default(true)
    emailVerified           Boolean   @default(false)
    // Relations to data, requests, access logs
}

model PatientDataNft {
    id             String      @id @default(uuid())
    nftTokenId     String      @unique // XRPL NFT ID
    nftStorageHash String      // IPFS hash
    dataType       DataType    // Medical data category
    encryptedTitle String?     // Patient-readable title
    // No actual medical data stored here
}
```

---

## API Endpoints

### **Authentication APIs**

```http
POST   /api/auth/register              # User registration
POST   /api/auth/login                 # User login
POST   /api/auth/verify-email          # Email verification
POST   /api/auth/resend-verification   # Resend verification
GET    /api/auth/status                # Auth status check
POST   /api/auth/logout                # User logout
```

### **Patient APIs**

```http
GET    /api/medledger/patient/onboarding/progress    # Get onboarding status
POST   /api/medledger/patient/onboarding/progress    # Save onboarding step
POST   /api/medledger/patient/onboarding/complete    # Complete onboarding
POST   /api/medledger/patient/approve-access         # Approve provider access
GET    /api/patient/access-requests                  # Get access requests
```

### **Medical Records APIs**

```http
POST   /api/medledger/records          # Upload medical record
GET    /api/medledger/records          # List patient records
PUT    /api/medledger/records/:id      # Update record metadata
DELETE /api/medledger/records/:id      # Delete record
```

### **XRPL Integration APIs**

```http
POST   /api/xrpl/verify-wallet         # Verify XRPL wallet
GET    /api/xrpl/verify-status/:id     # Check transaction status
```

### **User Management APIs**

```http
GET    /api/user/profile               # Get user profile
PUT    /api/user/profile               # Update user profile
GET    /api/user/patient/data          # Get patient data summary
POST   /api/user/account/save/record   # Save medical record
```

---

## Installation & Setup

### **Prerequisites**

-   Node.js 18+ and npm/yarn
-   PostgreSQL 14+ database
-   XRPL Testnet account (for development)
-   IPFS node or NFT.Storage account

### **1. Clone Repository**

```bash
git clone https://github.com/TusharPardhe/Medledger.git
cd medledger
```

### **2. Install Dependencies**

```bash
npm install
# or
yarn install
```

### **3. Environment Configuration**

Create `.env.local` file:

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/medledger"

# Authentication
JWT_SECRET="your-super-secure-jwt-secret"
NEXTAUTH_SECRET="your-nextauth-secret"
NEXTAUTH_URL="http://localhost:3000"

# Email Service
BREVO_API_KEY="your-brevo-api-key"
BREVO_SENDER_EMAIL="noreply@yourdomain.com"

# XRPL Configuration
XRPL_NETWORK="testnet" # or "mainnet" for production
XRPL_WEBHOOK_SECRET="your-webhook-secret"

# IPFS/Storage
NFT_STORAGE_API_KEY="your-nft-storage-key"
PINATA_API_KEY="your-pinata-key"
PINATA_SECRET_KEY="your-pinata-secret"

# Security
ENCRYPTION_KEY="your-32-character-encryption-key"
```

### **4. Database Setup**

```bash
# Generate Prisma client
npm run db:generate

# Run migrations
npm run db:migrate

# Seed with demo data
npm run db:seed
```

### **5. Development Server**

```bash
npm run dev
```

Visit `http://localhost:3000` to see the application.

---

## Available Scripts

### **Development**

```bash
npm run dev              # Start development server
npm run build            # Build for production
npm run start            # Start production server
npm run lint             # Run ESLint
```

### **Database**

```bash
npm run db:generate      # Generate Prisma client
npm run db:migrate       # Run database migrations
npm run db:seed          # Seed database with demo data
npm run db:studio        # Open Prisma Studio
npm run db:reset         # Reset database
npm run db:status        # Check migration status
```

### **Testing & Quality**

```bash
npm run knip             # Find unused dependencies
npm run test:secure-exchange  # Test XRPL integration
```

---

## 🔧 Configuration

### **Database Configuration**

MedLedger uses PostgreSQL with Prisma ORM. The schema is designed for:

-   **Privacy**: Only metadata stored, actual data on IPFS
-   **Performance**: Optimized queries with proper indexing
-   **Compliance**: Audit trails and access logging
-   **Scalability**: Horizontal scaling support

### **XRPL Configuration**

```typescript
// XRPL network configuration
const xrplConfig = {
    network: process.env.XRPL_NETWORK || 'testnet',
    server: 'wss://s.altnet.rippletest.net:51233', // Testnet
    // server: 'wss://xrplcluster.com', // Mainnet
};
```

### **Security Configuration**

-   **JWT Tokens**: Secure session management
-   **Password Hashing**: bcrypt with 12 salt rounds
-   **Data Encryption**: AES-256-GCM for medical data
-   **API Rate Limiting**: DDoS protection
-   **CORS**: Strict origin policies

---

## Flow Diagrams

MedLedger includes comprehensive technical documentation with 7 detailed flow diagrams:

> **Note**: Click [`here`](./docs/flow-diagrams.md) for detailed charts.

### 1. **Patient Onboarding & XRPL Wallet Creation Flow**

Complete 6-step onboarding process with XRPL wallet generation and progressive profile updates.

### 2. **Medical Record Upload & NFT Minting Flow**

End-to-end process for encrypting, storing on IPFS, and minting medical data as NFTs on XRPL.

### 3. **Cryptographic Consent Protocol Flow**

Bidirectional consent mechanism between patients and providers using XRPL transactions.

### 4. **Database Schema Architecture & Data Flow**

Normalized database design with XRPL integration points and privacy-first architecture.

### 5. **Healthcare System Integration & API Architecture Flow**

Integration with Epic, Cerner, FHIR, HL7, and other healthcare standards.

### 6. **UI/UX Architecture & Component Structure**

Complete component hierarchy with accessibility and responsive design considerations.

### 7. **Hybrid Payment Systems Architecture Flow**

Multi-currency payment system supporting FIAT, XRP, RLUSD, and RippleNet integration.

---

## Security Features

### **Data Protection**

-   **End-to-End Encryption**: AES-256-GCM encryption for medical data
-   **Zero-Knowledge Architecture**: Platform cannot access patient data
-   **IPFS Storage**: Decentralized, tamper-proof storage
-   **Cryptographic Signatures**: XRPL-based data integrity

### **Access Control**

-   **Time-Bound Permissions**: Automatic expiration of access rights
-   **Granular Control**: Patients control specific data types
-   **Audit Trails**: Complete access logs with IP tracking
-   **Multi-Factor Authentication**: XRPL wallet + password verification

### **Compliance**

-   **HIPAA Compliance**: Healthcare data protection standards
-   **GDPR Compliance**: European privacy regulations
-   **SOC 2 Type II**: Security controls and procedures
-   **Regular Security Audits**: Third-party penetration testing

---

## Deployment

### **Environment Setup**

```bash
# Production build
npm run build

# Database migration for production
npm run db:migrate-deploy

# Start production server
npm run start
```

### **Environment Variables**

Ensure all production environment variables are configured:

-   Database connection strings
-   JWT secrets
-   XRPL mainnet configuration
-   Email service credentials
-   IPFS/storage provider keys

---

## Contributing

We welcome contributions to MedLedger! Please read our contributing guidelines:

### **Development Process**

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Add tests if applicable
5. Commit changes: `git commit -m 'Add amazing feature'`
6. Push to branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

### **Code Standards**

-   Follow TypeScript best practices
-   Use ESLint configuration
-   Write meaningful commit messages
-   Include tests for new features
-   Update documentation as needed

---

<div align="center">

**Built with ❤️ for healthcare data ownership**

[🌐 Website](https://medledgers.org)

</div>
