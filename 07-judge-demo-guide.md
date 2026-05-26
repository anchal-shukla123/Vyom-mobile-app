# Judge Demo Guide

## Recommended 5-Minute Demo Flow

### 1. Open With The Problem

Explain that local sellers usually need separate tools for social content, product catalogs, chat, payments, and order management. Vyom combines those into one mobile commerce platform.

### 2. Show Buyer Discovery

Start from the Home tab:

- Stories at the top
- Live Now sessions
- Trending products
- For You products
- Location-aware product discovery

Then open the Feed tab:

- Show social posts and reels
- Mention likes, saves, seller follows, and product tagging

### 3. Show Product To Checkout

Open a product:

- Product images and details
- Seller information
- Wishlist and cart actions
- Similar or recommended products

Move to cart and checkout:

- Address selection
- Coupon or summary
- Razorpay payment option
- Order confirmation

### 4. Show Realtime Commerce

Open a livestream:

- Agora video area
- Chat panel
- Reactions
- Pinned product
- Buy Now modal
- Q&A flow

Explain that Socket.IO handles realtime chat and session updates, while Agora handles video.

### 5. Show Buyer-Seller Communication

Open Inbox:

- Conversations
- Realtime message updates
- Typing indicators
- Read state
- Alerts and order updates

### 6. Show Seller Side

Open Seller Dashboard:

- Revenue and order overview
- Product management
- Order status updates
- Wallet withdrawal request
- Review management
- Push notification registration

### 7. Explain Architecture

Use [System Architecture](./04-system-architecture.md):

- Mobile app: Expo and React Native
- Backend: Express REST API
- Database: PostgreSQL with pgvector
- Realtime: Socket.IO
- AI: FastAPI embedding service
- Payments: Razorpay
- Live video: Agora
- Storage: Supabase

## Short Pitch Script

Vyom is a social commerce app for local sellers and buyers. Buyers discover products through personalized recommendations, feeds, stories, and livestreams. Sellers can manage products, orders, reviews, and live selling from the same platform. The system uses a React Native mobile app, Express backend, PostgreSQL database, realtime Socket.IO channels, Razorpay payments, Agora livestreaming, Supabase media storage, and a FastAPI AI service for semantic recommendations.

## Questions Judges May Ask

### How is this different from a normal ecommerce app?

Vyom combines ecommerce with social content and live selling. Discovery happens through posts, reels, stories, seller profiles, and livestream sessions, not only through static product search.

### How are payments handled?

The backend creates Razorpay orders and verifies Razorpay signatures. The mobile app only opens the Razorpay checkout and sends the returned payment identifiers to the backend for verification.

### How does AI fit into the project?

Product title and description text can be sent to a FastAPI embedding service. The backend stores 384-dimensional vectors in PostgreSQL with pgvector, enabling semantic product search and smarter recommendations.

### How does realtime communication work?

Socket.IO handles authenticated namespaces for inbox and livestream. Inbox supports messages, typing, read receipts, alerts, and reactions. Livestream supports viewer counts, live chat, reactions, pinned products, Q&A, and session end events.

### What is production-ready here?

The app has domain-separated APIs, token-based auth, payment verification, database indexing, media storage, realtime channels, and native mobile integrations. Additional production work would include deeper observability, admin tools, load testing, and complete compliance review.

