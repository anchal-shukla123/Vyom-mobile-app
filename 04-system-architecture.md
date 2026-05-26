# System Architecture

## High-Level Architecture

```mermaid
flowchart TD
  A["Vyom Mobile App<br/>Expo + React Native"] --> B["REST API<br/>Node.js + Express"]
  A --> C["Socket.IO Realtime Gateway"]
  A --> D["Supabase Storage<br/>Media Uploads"]
  A --> E["Razorpay Native Checkout"]
  A --> F["Agora Native Video SDK"]

  B --> G["PostgreSQL Database"]
  B --> H["Supabase Storage Admin API"]
  B --> I["Razorpay API + Webhooks"]
  B --> J["Google OAuth Verification"]
  B --> K["SMTP Email Provider"]
  B --> L["Expo Push Notifications"]
  B --> M["FastAPI AI Service"]

  M --> N["Sentence Transformer Model<br/>384-dim embeddings"]
  G --> O["pgvector Product Embeddings"]
```

## Runtime Components

### Mobile Client

The mobile app handles navigation, UI state, auth token storage, media picking, checkout screens, livestream UI, and realtime socket connections. It calls the backend through an Axios client that attaches bearer tokens and refreshes expired access tokens.

### API Server

The backend exposes versioned REST routes under `/api/v1`. It validates requests, enforces authentication, reads and writes PostgreSQL data, talks to external services, sends standardized responses, and manages webhooks.

### Realtime Server

Socket.IO powers two major realtime areas:

- `/inbox` namespace for chat, typing, read receipts, order updates, alerts, and reactions.
- `/livestream` namespace for session joins, viewer counts, messages, reactions, pinned products, Q&A, and session end events.

### AI Recommendation Service

The FastAPI service creates normalized text embeddings for products. The backend can request embeddings and store them in PostgreSQL with pgvector for semantic search and recommendation behavior.

### Database

PostgreSQL stores business data. Major domains include:

- Users and authentication tokens
- Products and product reviews
- Posts, likes, saves, follows, and feed data
- Stories, story views, and reactions
- Livestream sessions, messages, Q&A, and pinned products
- Cart, wishlist, and wishlist collections
- Orders, order items, tracking, coupons, payments, refunds, and disbursements
- Seller onboarding, seller bank accounts, and seller dashboard data
- Inbox conversations, messages, reactions, alerts, and read states

## Authentication Flow

```mermaid
sequenceDiagram
  participant User
  participant App as Mobile App
  participant API as Express API
  participant DB as PostgreSQL
  participant Google as Google OAuth

  User->>App: Login with email or Google
  App->>API: Submit credentials or Google ID token
  API->>Google: Verify Google token when used
  API->>DB: Load or create user
  API->>DB: Store refresh token record
  API-->>App: Access token, refresh token, user profile
  App->>App: Store tokens securely
  App->>API: Send bearer token on protected requests
  API-->>App: Refresh tokens when access token expires
```

## Product Discovery Flow

```mermaid
sequenceDiagram
  participant App
  participant API
  participant DB
  participant AI as AI Service

  App->>API: Request products, featured, for-you, or search
  API->>AI: Create search embedding when semantic search applies
  AI-->>API: 384-dimensional embedding
  API->>DB: Query products, sellers, wishlist state, reviews, embeddings
  DB-->>API: Product rows and related data
  API-->>App: Enriched product cards and details
```

## Checkout Flow

```mermaid
sequenceDiagram
  participant Buyer
  participant App
  participant API
  participant Razorpay
  participant DB

  Buyer->>App: Review cart and checkout
  App->>API: Create checkout summary
  App->>API: Place order
  API->>DB: Create order and payment record
  API->>Razorpay: Create Razorpay order for prepaid payment
  Razorpay-->>API: Razorpay order id
  API-->>App: Order and payment gateway data
  App->>Razorpay: Open native checkout
  Razorpay-->>App: Payment id and signature
  App->>API: Verify payment
  API->>Razorpay: Verify and capture
  API->>DB: Mark payment/order status
  API-->>App: Confirmed order state
```

## Livestream Flow

```mermaid
sequenceDiagram
  participant Seller
  participant Buyer
  participant App
  participant API
  participant Socket as Socket.IO
  participant Agora

  Seller->>API: Create livestream session
  API-->>Seller: Session id
  App->>API: Request Agora token
  API-->>App: Agora app id, token, channel, uid
  App->>Agora: Join video channel
  Buyer->>Socket: Join livestream session
  Socket-->>App: Viewer count, messages, reactions
  Seller->>Socket: Pin product, toggle Q&A, answer question
  Buyer->>API: Place live order
  API-->>App: Live order result
```

## Scalability Considerations

- REST routes are separated by domain, which makes it easier to scale features independently.
- Cached GET responses in the mobile Axios layer reduce repeated network calls.
- Realtime traffic is separated into inbox and livestream namespaces.
- Product embeddings are isolated in a lightweight AI service.
- Database indexes exist for frequent filters: users, products, ratings, locations, posts, livestreams, stories, orders, payments, wishlists, inbox, and vector search.

