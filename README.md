# RoomX

A desktop-first web application for creators and traders to run private, subscription-based live rooms.

## Features

- **User Authentication**: Email/password and social login via Clerk
- **Room Management**: Creators can create and manage their live rooms
- **Live Streaming**: Real-time video and screen sharing via LiveKit
- **Subscription System**: Stripe-powered subscription payments
- **Real-time Chat**: Interactive chat during live sessions
- **Access Control**: Subscription-based access to rooms
- **Member List**: See who's currently watching

## Tech Stack

- **Frontend**: Next.js 14 (App Router) with Tailwind CSS
- **Authentication**: Clerk
- **Database**: Supabase (PostgreSQL)
- **Live Streaming**: LiveKit Cloud
- **Payments**: Stripe Subscriptions
- **Hosting**: Vercel

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- Clerk account
- Supabase account
- LiveKit Cloud account
- Stripe account

### Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd RoomX
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.local.example .env.local
```

Fill in your environment variables in `.env.local`:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/dashboard
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/dashboard
CLERK_WEBHOOK_SECRET=whsec_...

# Supabase Database
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

# LiveKit Cloud
NEXT_PUBLIC_LIVEKIT_URL=wss://your-project.livekit.cloud
LIVEKIT_API_KEY=your-api-key
LIVEKIT_API_SECRET=your-api-secret

# Stripe Payments
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...

# App Configuration
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### Database Setup

You can use either **local PostgreSQL** or **Supabase**:

#### Option 1: Local PostgreSQL (Recommended for Development)
1. Install PostgreSQL locally
2. Create a database: `createdb roomx`
3. Run migrations: See `LOCAL_POSTGRES_SETUP.md` for detailed instructions
4. Set `DATABASE_URL` in `.env.local`:
   ```env
   DATABASE_URL=postgresql://postgres:postgres@localhost:5432/roomx
   ```

#### Option 2: Supabase (Cloud)
1. Create a new Supabase project
2. Run the SQL migrations from `supabase/migrations/` in the Supabase SQL editor:
   - `001_create_users_table.sql`
   - `002_create_rooms_table.sql`
   - `003_create_subscriptions_table.sql`
   - `004_create_room_participants_table.sql`
   - `005_create_functions_and_triggers.sql`
   - `006_enable_rls_policies.sql`
3. Set Supabase environment variables (see below)

### Clerk Setup

1. Create a Clerk account and application
2. Configure authentication providers (Email, Google, GitHub, etc.)
3. Set up webhooks:
   - Webhook URL: `https://your-domain.com/api/webhooks/clerk`
   - Events: `user.created`, `user.updated`, `user.deleted`
   - Copy the webhook secret to `CLERK_WEBHOOK_SECRET`

### LiveKit Setup

1. Create a LiveKit Cloud account
2. Create a new project
3. Copy your project URL, API key, and API secret to the environment variables

### Stripe Setup

1. Create a Stripe account
2. Get your API keys from the Stripe Dashboard
3. Set up webhooks:
   - Webhook URL: `https://your-domain.com/api/webhooks/stripe`
   - Events: `checkout.session.completed`, `customer.subscription.*`, `invoice.payment_*`
   - Copy the webhook secret to `STRIPE_WEBHOOK_SECRET`

### Development

Run the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Build

Build for production:

```bash
npm run build
npm start
```

### Deployment

1. Push your code to GitHub
2. Connect your repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy!

## Project Structure

```
RoomX/
├── app/                    # Next.js App Router
│   ├── api/               # API routes
│   │   ├── rooms/        # Room management endpoints
│   │   ├── subscriptions/ # Subscription endpoints
│   │   └── webhooks/     # Webhook handlers
│   ├── dashboard/        # Dashboard pages
│   ├── room/            # Live room pages
│   ├── subscribe/       # Subscription pages
│   ├── layout.tsx       # Root layout
│   └── page.tsx         # Landing page
├── components/          # React components
│   ├── LiveRoom.tsx    # Live room component
│   └── SubscribeButton.tsx
├── lib/                 # Utility libraries
│   ├── livekit/        # LiveKit utilities
│   ├── stripe/         # Stripe utilities
│   ├── supabase/       # Supabase utilities
│   ├── types/          # TypeScript types
│   └── utils/          # Helper functions
├── middleware.ts        # Next.js middleware (Clerk)
└── package.json
```

## Documentation

- [Architecture](./ARCHITECTURE.md) - System architecture and design
- [Database Schema](./DATABASE_SCHEMA.md) - Database schema and migrations
- [Feature Breakdown](./FEATURE_BREAKDOWN.md) - MVP feature list

## Development Workflow

1. **Day 1-2**: Project setup and authentication
2. **Day 3**: Database setup and migrations
3. **Day 4-5**: Room management APIs and UI
4. **Day 6-7**: LiveKit integration
5. **Day 8-9**: Stripe integration and subscriptions
6. **Day 10**: Access control and testing
7. **Day 11-12**: Polish and deployment

## License

Private - All rights reserved

# RoomX
