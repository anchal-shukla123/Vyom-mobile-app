# API Reference

Base path: `/api/v1`

The mobile app talks to a Node/Express backend through REST APIs and Socket.IO. Protected routes require a bearer access token. The mobile client refreshes expired tokens through the refresh endpoint.

## Authentication APIs

| Method | Path | Purpose |
|---|---|---|
| POST | `/auth/register` | Create account |
| POST | `/auth/verify-email` | Verify email OTP/code |
| POST | `/auth/resend-verification` | Resend verification email |
| POST | `/auth/login` | Login with email and password |
| POST | `/auth/google` | Login with Google ID token |
| POST | `/auth/forgot-password` | Request password reset |
| POST | `/auth/reset-password` | Reset password |
| POST | `/auth/refresh` | Issue new access and refresh tokens |
| POST | `/auth/logout` | Logout and invalidate refresh token |
| GET | `/auth/me` | Get current user profile |
| PATCH | `/auth/location` | Update buyer location |

## Account APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/account/dashboard` | Buyer account dashboard |
| PATCH | `/account/profile` | Update user profile |
| GET | `/account/orders` | Basic order list |
| GET | `/account/orders/detailed` | Detailed order list with filters |
| POST | `/account/orders/:orderId/cancel` | Cancel order |
| POST | `/account/orders/:orderId/reorder` | Reorder previous order |
| POST | `/account/orders/:orderId/rating` | Submit product/order rating |
| GET | `/account/cart` | Cart detail |
| GET | `/account/cart/count` | Cart count |
| POST | `/account/cart/add` | Add product to cart |
| PATCH | `/account/cart/items/:productId` | Update cart quantity |
| DELETE | `/account/cart/items/:productId` | Remove cart item |
| DELETE | `/account/cart` | Clear cart |
| GET | `/account/wishlist` | Wishlist items |
| GET | `/account/wishlist/collections` | Wishlist collections |
| POST | `/account/wishlist/collections` | Create wishlist collection |
| POST | `/account/wishlist/collections/items` | Save product into collection |
| GET | `/account/addresses` | Address list |
| POST | `/account/addresses` | Create or save address |
| POST | `/account/seller-onboarding` | Submit seller onboarding |
| PATCH | `/account/security` | Update security preferences |
| POST | `/account/push-token` | Register Expo push token |
| POST | `/account/data-export` | Request data export |

## Feed And Social APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/feed/for-you` | Personalized feed |
| GET | `/feed/following` | Feed from followed sellers |
| GET | `/feed/reels` | Reel-style feed |
| GET | `/feed/local` | Local feed |
| GET | `/posts` | Feed posts |
| GET | `/posts/me` | Current user's posts |
| GET | `/posts/saved` | Saved posts |
| GET | `/posts/products/me` | Current seller's products for tagging |
| POST | `/posts` | Create post |
| POST | `/posts/products` | Create product through post flow |
| POST | `/posts/live` | Start live stream through post flow |
| DELETE | `/posts/:postId` | Delete post |
| POST | `/posts/:postId/like` | Like post |
| DELETE | `/posts/:postId/like` | Unlike post |
| POST | `/posts/:postId/save` | Save post |
| DELETE | `/posts/:postId/save` | Unsave post |
| POST | `/posts/sellers/:sellerId/follow` | Follow seller |
| DELETE | `/posts/sellers/:sellerId/follow` | Unfollow seller |

## Product APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/products` | Product list with search, category, sorting, and location params |
| GET | `/products/featured` | Featured products |
| GET | `/products/for-you` | Personalized product recommendations |
| GET | `/products/categories` | Product categories |
| GET | `/products/:productId` | Product detail |
| POST | `/products/:productId/wishlist` | Add product to wishlist |
| DELETE | `/products/:productId/wishlist` | Remove product from wishlist |

## Seller APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/sellers/dashboard` | Seller dashboard data |
| PATCH | `/sellers/orders/:orderId/status` | Update seller order status |
| GET | `/sellers/orders/:orderId/invoice` | Get invoice URL or invoice data |
| POST | `/sellers/products` | Create seller product |
| PATCH | `/sellers/products/:productId` | Update seller product |
| DELETE | `/sellers/products/:productId` | Delete seller product |
| POST | `/sellers/wallet/withdrawals` | Request wallet withdrawal |
| POST | `/sellers/reviews/:reviewId/reply` | Reply to review |
| POST | `/sellers/reviews/:reviewId/report` | Report review |
| POST | `/sellers/notifications/push-token` | Register seller push token |
| GET | `/sellers/:sellerId` | Public seller profile |
| GET | `/sellers/:sellerId/products` | Seller products |
| GET | `/sellers/:sellerId/reviews` | Seller reviews |
| GET | `/sellers/:sellerId/posts` | Seller posts |
| GET | `/sellers/:sellerId/stories` | Seller stories |
| GET | `/sellers/:sellerId/lives` | Seller live sessions |
| POST | `/sellers/:sellerId/follow` | Follow seller |
| DELETE | `/sellers/:sellerId/follow` | Unfollow seller |
| PATCH | `/sellers/:sellerId/photo` | Update seller photo |

## Story APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/stories/feed` | Story feed |
| POST | `/stories` | Create story |
| GET | `/stories/:storyId` | Story detail |
| POST | `/stories/:storyId/view` | Mark story viewed |
| POST | `/stories/:storyId/react` | React to story |
| GET | `/stories/:storyId/viewers` | Story viewers |
| DELETE | `/stories/:storyId` | Delete story |

## Livestream APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/livestream/sessions` | List live sessions |
| GET | `/livestream/sessions/:sessionId` | Get session detail |
| POST | `/livestream/sessions` | Create livestream session |
| POST | `/livestream/sessions/:sessionId/end` | End livestream |
| GET | `/livestream/sessions/:sessionId/token` | Get Agora token |
| GET | `/livestream/sessions/:sessionId/messages` | Get chat history |
| POST | `/livestream/orders` | Place order from livestream |

## Inbox APIs

| Method | Path | Purpose |
|---|---|---|
| GET | `/inbox` | Inbox summary |
| POST | `/inbox/sellers/:sellerId/conversation` | Start or get seller conversation |
| GET | `/inbox/conversations/:conversationId/messages` | Conversation messages |
| POST | `/inbox/conversations/:conversationId/messages` | Send message |
| POST | `/inbox/conversations/:conversationId/read` | Mark conversation read |
| POST | `/inbox/orders/:orderId/read` | Mark order notification read |
| POST | `/inbox/alerts/:alertId/read` | Mark alert read |
| POST | `/inbox/alerts/clear` | Clear alerts |

## Order And Payment APIs

| Method | Path | Purpose |
|---|---|---|
| POST | `/orders/checkout-summary` | Calculate checkout summary |
| POST | `/orders` | Place order |
| POST | `/orders/verify-payment` | Verify Razorpay payment |
| GET | `/orders` | List orders |
| GET | `/orders/:orderId` | Order detail |
| POST | `/orders/:orderId/cancel` | Cancel order |
| GET | `/payment-methods` | Saved payment methods |
| POST | `/payment-methods` | Save payment method |
| DELETE | `/payment-methods/:methodId` | Delete payment method |
| POST | `/coupons/validate` | Validate coupon |
| POST | `/webhooks/razorpay` | Razorpay webhook receiver |

## AI Service APIs

The AI service is a separate FastAPI service.

| Method | Path | Purpose |
|---|---|---|
| GET | `/health` | Health check and active model |
| POST | `/embedding` | Generate 384-dimensional normalized text embedding |

Embedding request intent:

- Product title
- Product description

Embedding response intent:

- Embedding vector
- Dimensions
- Model name

## Realtime Socket Namespaces

### `/inbox`

Client emits:

- `join_conversation`
- `leave_conversation`
- `send_message`
- `typing`
- `mark_read`
- `mark_order_read`
- `mark_alert_read`
- `add_reaction`

Server emits:

- `new_message`
- `message_status_update`
- `typing_start`
- `typing_stop`
- `user_status_change`
- `order_update`
- `new_alert`
- `reaction_added`

### `/livestream`

Client emits:

- `join-session`
- `leave-session`
- `send-message`
- `send-reaction`
- `pin-message`
- `pin-product`
- `toggle-qa`
- `answer-question`

Server emits:

- `viewer-count`
- `new-message`
- `reaction-update`
- `message-pinned`
- `product-pinned`
- `qa-toggled`
- `session-ended`
- `new-question`

