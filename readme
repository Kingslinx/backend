Stellar Spend Backend
Backend infrastructure powering Stellar Spend, a WhatsApp-native financial platform built on the Stellar blockchain that enables users to send, receive, save, and spend digital assets directly from WhatsApp.
Overview
The Stellar Spend Backend serves as the core orchestration layer between:
WhatsApp Cloud API
Stellar Blockchain
Soroban Smart Contracts
AI Services
User Authentication
Merchant Services
Payment Processing
Compliance Systems
It provides secure APIs, transaction processing, wallet management, and conversational financial services for users interacting through WhatsApp.
Core Responsibilities
Wallet Management
Create Stellar wallets
Link wallets to phone numbers
Manage trustlines
Retrieve balances
Generate transaction history
Payment Processing
Peer-to-peer transfers
Merchant payments
Asset transfers
Stablecoin transactions
Cross-border remittances
User Management
Registration
Authentication
PIN management
KYC verification
Account recovery
WhatsApp Integration
Message processing
Conversation management
Interactive menus
Notification delivery
Smart Contract Integration
Escrow
Savings vaults
Merchant settlements
Loyalty programs
AI Services
Intent recognition
Natural language transaction parsing
Financial insights
Customer support automation
Technology Stack
Framework
NestJS
Why NestJS?
Scalable architecture
Dependency Injection
Modular design
Enterprise-grade patterns
TypeScript-first
nestjs
typescript
Database
PostgreSQL
Stores:
Users
Wallets
Transactions
Merchants
KYC records
Conversation history
Prisma ORM
Benefits:
Type-safe queries
Migration support
Excellent TypeScript integration
npm install prisma @prisma/client
Cache & Queue
Redis
Used for:
Session storage
OTP management
Rate limiting
Conversation state
npm install redis
BullMQ
Used for:
Transaction processing
Notifications
Wallet creation jobs
Blockchain monitoring
npm install bullmq
Blockchain Layer
Stellar SDK
Official SDK for interacting with Stellar.
npm install @stellar/stellar-sdk
Features:
Account creation
Payments
Trustline management
Asset transfers
Transaction signing
Soroban Integration
Smart contract interactions for:
Escrow
Savings
Merchant settlements
AI Layer
OpenAI API
Used for:
Conversational banking
Intent extraction
Transaction parsing
Example:
User sends:
Send 20 USDC to Emeka
AI extracts:
{
  "intent": "SEND_MONEY",
  "amount": 20,
  "asset": "USDC",
  "recipient": "Emeka"
}
Authentication
JWT
npm install @nestjs/jwt passport-jwt
Used for:
Admin authentication
Merchant dashboard access
Internal services
OTP Verification
Supported channels:
WhatsApp
SMS
Email
Monitoring
Sentry
npm install @sentry/node
Tracks:
Exceptions
Failed transactions
API failures
Prometheus
System metrics collection.
Grafana
Visualization dashboards.
Architecture
┌──────────────────────────┐
│      WhatsApp User       │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ WhatsApp Cloud API       │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ API Gateway              │
└─────────────┬────────────┘
              │
 ┌────────────┼─────────────┐
 ▼            ▼             ▼
Auth      Messaging     AI Service
Service    Service
 │            │
 ▼            ▼
User      Transaction
Service    Service
 │            │
 ▼            ▼
Prisma    Stellar SDK
 │            │
 ▼            ▼
Postgres  Stellar Network
              │
              ▼
      Soroban Contracts
Project Structure
src/

├── app.module.ts

├── common/
│   ├── decorators/
│   ├── guards/
│   ├── interceptors/
│   ├── filters/
│   └── utils/

├── config/
│   ├── database.config.ts
│   ├── redis.config.ts
│   ├── stellar.config.ts
│   └── whatsapp.config.ts

├── modules/

│   ├── auth/
│   ├── users/
│   ├── wallets/
│   ├── transactions/
│   ├── whatsapp/
│   ├── messaging/
│   ├── merchants/
│   ├── assets/
│   ├── savings/
│   ├── escrow/
│   ├── kyc/
│   ├── ai/
│   ├── notifications/
│   └── analytics/

├── prisma/
│   ├── schema.prisma
│   └── migrations/

├── jobs/
│   ├── transaction.processor.ts
│   ├── notification.processor.ts
│   └── blockchain.processor.ts

├── blockchain/
│   ├── stellar.service.ts
│   ├── wallet.service.ts
│   ├── transaction.service.ts
│   └── soroban.service.ts

└── main.ts
Environment Variables
Create a .env file:
# Application
PORT=3000
NODE_ENV=development

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/stellar_spend

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379

# JWT
JWT_SECRET=super_secret_key

# WhatsApp
WHATSAPP_TOKEN=
WHATSAPP_PHONE_ID=
WHATSAPP_VERIFY_TOKEN=

# OpenAI
OPENAI_API_KEY=

# Stellar
STELLAR_NETWORK=testnet
STELLAR_HORIZON_URL=https://horizon-testnet.stellar.org

# Soroban
SOROBAN_RPC_URL=https://soroban-testnet.stellar.org

# Sentry
SENTRY_DSN=
Installation
Clone Repository
git clone https://github.com/your-org/stellar-spend-backend.git

cd stellar-spend-backend
Install Dependencies
npm install
Setup Database
npx prisma migrate dev
Generate Prisma Client
npx prisma generate
Run Development Server
npm run start:dev
Core Modules
Auth Module
Responsibilities:
Registration
Login
PIN verification
JWT issuance
Wallet Module
Responsibilities:
Wallet creation
Wallet lookup
Balance retrieval
Trustline creation
Endpoints:
POST /wallets/create
GET /wallets/:id
GET /wallets/:id/balance
Transaction Module
Responsibilities:
Send funds
Receive funds
Transaction history
Transaction validation
Endpoints:
POST /transactions/send
GET /transactions/history
WhatsApp Module
Responsibilities:
Webhook handling
Message processing
Interactive menus
Endpoints:
POST /webhooks/whatsapp
GET /webhooks/verify
AI Module
Responsibilities:
Intent detection
Natural language parsing
Financial assistant
Example Intent:
{
  "intent": "CHECK_BALANCE"
}
Database Schema
User
model User {
  id          String   @id @default(uuid())
  phoneNumber String   @unique
  walletId    String?
  pinHash     String?
  createdAt   DateTime @default(now())
}
Wallet
model Wallet {
  id         String   @id @default(uuid())
  publicKey  String   @unique
  encryptedKey String
  userId     String   @unique
  createdAt  DateTime @default(now())
}
Transaction
model Transaction {
  id          String   @id @default(uuid())
  hash        String
  amount      Decimal
  assetCode   String
  senderId    String
  receiverId  String
  status      String
  createdAt   DateTime @default(now())
}
Security Considerations
Wallet Security
Never store private keys in plain text.
Recommended:
AES-256 encryption
AWS KMS
HashiCorp Vault
MPC wallet infrastructure
Transaction Verification
Require:
PIN verification
OTP verification
Fraud checks
before signing transactions.
Rate Limiting
Use Redis-backed throttling to prevent:
Spam
Abuse
Brute-force attacks
Deployment
Docker
Build image:
docker build -t stellar-spend-backend .
Run:
docker run -p 3000:3000 stellar-spend-backend
Production Infrastructure
Recommended:
Amazon Web Services ECS/EKS
Cloudflare
Sentry
Grafana Labs
PostgreSQL
Redis
Roadmap
Phase 1
Wallet creation
WhatsApp onboarding
Balance checks
P2P transfers
Phase 2
USDC support
Merchant payments
QR payments
Phase 3
Savings contracts
Escrow contracts
AI financial assistant
Phase 4
Remittances
Lending
Insurance products
Business accounts
Mission
Stellar Spend Backend powers a WhatsApp-native financial ecosystem that makes blockchain transactions as simple as sending a message, bringing accessible digital finance to millions of users through the Stellar network.
