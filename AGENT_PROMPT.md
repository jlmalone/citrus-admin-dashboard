# 🤖 CLAUDE CODE WEB AGENT TASK - Citrus Admin Dashboard

**Repository**: citrus-admin-dashboard
**Priority**: 🔴 CRITICAL
**Estimated Effort**: 12-16 hours
**Current State**: Empty shell - build complete admin dashboard from scratch

---

## ⚠️ IDEMPOTENCY CHECK

```bash
if [ -f ".claude-agent-completed" ]; then
    echo "✅ Task already completed!"
    cat .claude-agent-completed
    exit 0
fi
```

---

## 📋 TASK: Build Enterprise Admin Dashboard for Citrus Platform

### Project Overview
Build a comprehensive **admin dashboard** for the Citrus receipt intelligence platform. This is the central command center for platform administrators to manage users, monitor system health, review receipts, manage merchants, and configure the entire platform.

### Architecture
- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript
- **UI**: React 19 + Tailwind CSS + shadcn/ui
- **Auth**: Firebase Admin SDK
- **Backend**: Ktor API (`http://localhost:8080/api/v2`)
- **Database**: Firebase Firestore (read via Admin SDK)
- **Charts**: Recharts or Chart.js
- **State**: Zustand or TanStack Query

---

## 🎯 FEATURES TO IMPLEMENT

### Core Features (Must Have)

#### 1. Authentication & Authorization
- Admin login with Firebase Auth
- Role-based access control (Super Admin, Admin, Support)
- Session management
- Secure token handling
- 2FA support

#### 2. Dashboard Overview
- **System Stats Cards**:
  - Total users
  - Total receipts (today/week/month/all-time)
  - Active users (last 24h/7d/30d)
  - Storage used
  - API requests (today/week)
  - Error rate
- **Charts**:
  - User growth over time
  - Receipt uploads over time
  - Top merchants by volume
  - Category distribution
- **Recent Activity Feed**:
  - New user signups
  - Recent receipts
  - System alerts
  - API errors

#### 3. User Management
- **User List View**:
  - Searchable table (name, email, signup date, status)
  - Filters (active, inactive, role, signup date range)
  - Pagination
  - Bulk actions (activate, deactivate, delete)
- **User Detail View**:
  - Profile information
  - Receipt count and stats
  - Activity history
  - Assigned roles
  - Storage usage
  - Last login
  - Account status toggle
- **User Actions**:
  - Create new user
  - Edit user profile
  - Reset password
  - Delete user (with confirmation)
  - View user receipts
  - Impersonate user (for support)

#### 4. Receipt Management
- **Receipt Review Queue**:
  - Flagged receipts (suspicious, low OCR confidence)
  - Pending moderation
  - Review interface with approve/reject
- **Receipt Search**:
  - Full-text search
  - Filters (user, date, merchant, amount, tags)
  - Advanced search builder
- **Receipt Detail View**:
  - Images (multi-photo carousel)
  - OCR text
  - Extracted data (merchant, total, items, date)
  - Confidence scores
  - Edit extracted data
  - Reassign to user
  - Delete receipt
  - View processing history

#### 5. Merchant Database Management
- **Merchant List**:
  - All merchants
  - Search and filters
  - Stats (total receipts, users)
- **Merchant Detail**:
  - Name, address, category
  - Logo upload
  - Edit information
  - Merge duplicate merchants
  - View receipts from this merchant
- **Bulk Operations**:
  - Import merchant database (CSV)
  - Export merchant list
  - Bulk categorization

#### 6. Tag Template Management
- **Tag Templates**:
  - Create system-wide tag templates
  - Assign colors and icons
  - Make tags mandatory for certain categories
  - Delete unused tags
- **Tag Analytics**:
  - Most used tags
  - Tag trends over time

#### 7. System Configuration
- **Settings**:
  - OCR provider settings
  - LLM endpoint configuration
  - Storage limits per user
  - API rate limits
  - Email templates
  - Notification settings
  - Feature flags
- **API Key Management**:
  - Generate API keys
  - Revoke keys
  - View API usage per key

#### 8. Analytics & Reports
- **Platform Analytics**:
  - User retention
  - Churn rate
  - Average receipts per user
  - Storage growth
  - Popular categories
  - Peak usage times
- **Custom Reports**:
  - Report builder
  - Scheduled reports
  - Export to CSV/PDF

#### 9. Audit Logs
- **Activity Log**:
  - All admin actions
  - User modifications
  - System changes
  - Login attempts
  - Searchable and filterable
- **Compliance Reports**:
  - GDPR data access requests
  - Data deletion logs

#### 10. Subscription & Billing (Stripe)
- **Subscription Management**:
  - View all subscriptions
  - Change plans
  - Cancel subscriptions
  - Issue refunds
- **Billing Dashboard**:
  - Revenue over time
  - MRR (Monthly Recurring Revenue)
  - Churn analysis
  - Failed payments

---

## 📐 PAGES & ROUTES

### Page Structure

```
/admin
├── / (dashboard overview)
├── /users
│   ├── / (user list)
│   ├── /[id] (user detail)
│   └── /new (create user)
├── /receipts
│   ├── / (receipt list)
│   ├── /[id] (receipt detail)
│   └── /review (review queue)
├── /merchants
│   ├── / (merchant list)
│   ├── /[id] (merchant detail)
│   └── /new (create merchant)
├── /tags
│   └── / (tag template management)
├── /analytics
│   └── / (analytics dashboard)
├── /settings
│   ├── / (system settings)
│   ├── /api-keys (API key management)
│   └── /billing (Stripe integration)
├── /audit-logs
│   └── / (audit log viewer)
└── /profile
    └── / (admin profile)
```

---

## 🛠️ TECHNICAL SPECIFICATIONS

### Dependencies (package.json)

```json
{
  "dependencies": {
    "next": "^15.1.0",
    "react": "^19.0.0",
    "react-dom": "^19.0.0",
    "typescript": "^5.7.0",
    "tailwindcss": "^3.4.0",
    "firebase-admin": "^13.0.0",
    "axios": "^1.7.0",
    "zustand": "^5.0.0",
    "@tanstack/react-query": "^5.62.0",
    "recharts": "^2.15.0",
    "@radix-ui/react-*": "latest",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.1.0",
    "tailwind-merge": "^2.7.0",
    "lucide-react": "^0.468.0",
    "date-fns": "^4.1.0",
    "zod": "^3.24.0",
    "react-hook-form": "^7.54.0",
    "@stripe/stripe-js": "^5.2.0"
  }
}
```

### Environment Variables (.env.example)

```env
# Firebase Admin
FIREBASE_PROJECT_ID=citrusreceipts
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=firebase-adminsdk-xxxxx@citrusreceipts.iam.gserviceaccount.com

# Backend API
NEXT_PUBLIC_API_BASE_URL=http://localhost:8080/api/v2

# Stripe (optional)
STRIPE_SECRET_KEY=sk_test_xxxxx
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_xxxxx

# Auth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-secret-key-here
```

### API Client Setup

Create `lib/api-client.ts`:
```typescript
import axios from 'axios';

const apiClient = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_BASE_URL,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Add Firebase ID token to requests
apiClient.interceptors.request.use(async (config) => {
  const token = await getCurrentUserToken(); // Get Firebase token
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

export default apiClient;
```

---

## 🎨 UI COMPONENTS (use shadcn/ui)

Install shadcn/ui components:
```bash
npx shadcn@latest init
npx shadcn@latest add button card table dialog form input label select badge avatar dropdown-menu
```

Key components to build:
- `<StatCard>` - Dashboard stat cards with icons
- `<UserTable>` - Sortable, filterable user table
- `<ReceiptCard>` - Receipt display with image and details
- `<MerchantBadge>` - Merchant logo + name
- `<ActivityFeed>` - Real-time activity stream
- `<SearchBar>` - Advanced search with filters
- `<ConfirmDialog>` - Confirmation for destructive actions
- `<ImageCarousel>` - Multi-photo viewer
- `<ChartCard>` - Wrapper for charts with loading states

---

## ✅ SUCCESS CRITERIA

- [ ] Dashboard displays system stats and charts
- [ ] User management (CRUD operations)
- [ ] Receipt review and moderation works
- [ ] Merchant database management functional
- [ ] Tag template system working
- [ ] System settings can be configured
- [ ] Audit logs visible and searchable
- [ ] Stripe billing integration (basic)
- [ ] Analytics dashboard displays charts
- [ ] Responsive design (works on tablet)
- [ ] Dark mode support
- [ ] Loading states and error handling
- [ ] Role-based access control enforced

---

## 🎬 COMPLETION PROTOCOL

```bash
cat > .claude-agent-completed << 'EOF'
✅ TASK COMPLETED

Repository: citrus-admin-dashboard
Task: Build enterprise admin dashboard for Citrus platform
Completed: $(date -u +"%Y-%m-%d %H:%M:%S UTC")
Agent: Claude Code Web

Summary:
- ✅ Next.js 15 with TypeScript
- ✅ Complete admin dashboard with 10+ pages
- ✅ User management (CRUD, roles, impersonation)
- ✅ Receipt review and moderation
- ✅ Merchant database management
- ✅ Tag template system
- ✅ System configuration
- ✅ Analytics dashboard with charts
- ✅ Audit log viewer
- ✅ Stripe billing integration
- ✅ Firebase Admin SDK integration
- ✅ Responsive design with dark mode

Pages Created:
- Dashboard overview with stats
- User list and detail views
- Receipt list, detail, and review queue
- Merchant management
- Tag templates
- Analytics dashboard
- System settings
- Audit logs
- Admin profile

Next Steps:
1. npm install
2. Copy .env.example to .env.local and configure Firebase + Stripe
3. npm run dev
4. Visit http://localhost:3000/admin
5. Login with admin Firebase credentials

Integration:
- Works with Citrus Ktor backend (localhost:8080)
- Reads from Firebase Firestore via Admin SDK
- Optional Stripe integration for billing
EOF

git add .
git commit -m "🍊 Complete Citrus Admin Dashboard

- Full admin interface for platform management
- User, receipt, merchant, and tag management
- System configuration and monitoring
- Analytics and audit logs
- Stripe billing integration
- Responsive design with dark mode"

git push origin main
```

---

## 📝 NOTES

- **Security**: Ensure all admin routes require authentication and proper role checks
- **Performance**: Use server-side rendering for initial load, client-side for interactions
- **Scalability**: Implement pagination for all lists (users, receipts, merchants)
- **UX**: Add loading skeletons, optimistic updates, and error boundaries
- **Mobile**: Admin dashboard should be functional on tablets, not required for phones

---

**Ready to build the enterprise admin command center! 🚀**
