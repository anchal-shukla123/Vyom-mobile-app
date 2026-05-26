# Security And Data Notes

## Authentication

- Passwords are hashed with bcrypt before storage.
- Access tokens are sent as bearer tokens for protected APIs.
- Refresh tokens are stored server-side and can be rotated or invalidated.
- The mobile client stores auth tokens in SecureStore on native platforms.
- Web fallback uses localStorage only when running as a web build.
- Google sign-in verifies ID tokens on the backend.

## API Protection

- Sensitive auth routes use rate limiting.
- Payment-related routes use payment-specific rate limiting.
- Express middleware validates request bodies through validators.
- Protected routes use authentication middleware.
- Seller actions should be restricted to seller or admin roles.
- CORS and helmet are configured on the API server.

## Payment Security

- Razorpay order creation happens on the backend.
- Razorpay payment verification happens on the backend.
- Payment signatures are verified before marking payment as successful.
- Webhook signatures are checked for Razorpay webhook events.
- Refund and payment state are stored in backend database tables.

## Media And Storage

- Mobile uploads use Supabase public configuration where applicable.
- Backend media actions use service-role access where server-controlled uploads are needed.
- Documentation does not include Supabase keys or private bucket credentials.

## Realtime Security

- Socket.IO namespaces authenticate clients using tokens.
- Inbox sockets join user and conversation rooms only after authentication.
- Livestream sockets validate sessions and use room-based broadcasting.

## Data Domains

The app stores data in several business domains:

- Users and auth tokens
- Products and reviews
- Posts, saves, likes, follows
- Stories, views, reactions, highlights
- Livestream sessions and messages
- Cart and wishlists
- Orders, payments, refunds, tracking, coupons
- Seller onboarding and bank accounts
- Inbox conversations, alerts, and read states
- Data export requests and security settings

## Private Information Excluded From This Pack

This folder intentionally excludes:

- Source code
- API keys
- JWT secrets
- SMTP credentials
- Razorpay credentials
- Google OAuth secrets
- Supabase service role keys
- Agora certificates
- Database connection URLs
- Real user data

## Recommended Judge Talking Points

- The app demonstrates a full buyer-to-seller commerce loop.
- Security is handled server-side for auth, payments, and socket access.
- Payment secrets never need to be exposed in the mobile client.
- Native integrations are correctly separated from web or Expo Go limitations.
- The AI service is isolated so recommendations can evolve without rewriting the main API.

