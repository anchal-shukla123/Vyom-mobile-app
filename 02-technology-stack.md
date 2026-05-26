# Technology Stack

## Mobile App

- Expo SDK 54
- React Native 0.81
- React 19
- Expo Router for file-based navigation
- React Navigation compatible bottom tabs and native stacks
- TypeScript
- Zustand for app state
- Axios for REST API calls
- Socket.IO client for realtime messaging and livestream events
- Expo SecureStore for native token storage
- localStorage fallback for web builds
- Expo Notifications for push notification tokens
- Expo Image Picker, Image Manipulator, File System, and Compressor for media workflows
- Expo Location for buyer location based features
- React Native Agora for livestream video in native builds
- React Native Razorpay for payment checkout in native builds
- Supabase JS client for storage and public media URLs

## Backend API

- Node.js 20+
- Express 5
- CommonJS modules
- PostgreSQL with `pg`
- Socket.IO server for realtime channels
- JSON Web Tokens for authentication
- bcryptjs for password hashing
- express-validator for request validation
- express-rate-limit for protection on sensitive endpoints
- helmet, cors, and morgan for baseline API security and logging
- Nodemailer for email verification and password reset emails
- Google Auth Library for Google ID token verification
- Razorpay API integration for payments, captures, refunds, and webhooks
- Agora token generation for livestream access

## AI Service

- FastAPI
- Uvicorn
- sentence-transformers
- PyTorch
- Pydantic
- Default model: `all-MiniLM-L6-v2`
- Embedding dimension: 384

## Data And Storage

- PostgreSQL relational database
- pgvector extension for product embeddings
- Supabase Storage for media upload and public asset delivery
- Tables cover users, products, posts, stories, livestreams, inbox, orders, payments, coupons, refunds, seller onboarding, seller bank accounts, wishlists, carts, addresses, reviews, and tracking.

## External Integrations

- Google OAuth for sign-in
- Razorpay for payment gateway flow
- Agora for live video sessions
- Supabase Storage for product, post, and story media
- Expo Push Notifications for device notifications
- SMTP email provider for verification and password reset messages
- Render-hosted production API endpoint pattern

## Development And Deployment Notes

- Mobile development uses Expo start scripts.
- The API base URL resolves automatically for local, LAN, and production environments.
- Production API base pattern: `https://vyom-e260.onrender.com/api/v1`
- Local backend default: `http://localhost:5000/api/v1`
- AI service default: `http://localhost:8000`
- Native modules such as Agora, Google native sign-in, and Razorpay require a development or standalone build, not plain Expo Go.

