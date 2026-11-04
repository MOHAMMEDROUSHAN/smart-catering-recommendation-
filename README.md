# Smart Catering Recommendation and Management System

A modern, full-stack, enterprise-grade web application engineered to intelligently match event organizers with verified luxury caterers, artisanal chefs, and traditional banquet companies based on multi-parameter compatibility, availability, and budgets.

---

## 🌟 Key System Capabilities

1. **Intelligent Matchmaking Engine (Section 3.B)**:
   - Evaluates **8 core factors**: Location proximity (20%), Budget compatibility per plate (20%), Cuisine specialization (20%), Guest capacity thresholds (15%), Caterer calendar availability (15%), Supported event types (5%), and Additional equipment & staff services (5%).
   - Calculates dynamic suitability scores (e.g., **98% Match**, **87% Match**) with itemized breakdown scores.
   - Generates transparent, human-readable match explanations for every recommendation.

2. **Role-Based Access Control (3 Distinct Roles)**:
   - **Customer**: Manage event requirements, explore caterers, view AI recommendations, submit enquiries, compare received quotations side-by-side, chat & negotiate pricing, and confirm bookings.
   - **Caterer**: Manage business profile, showcase cuisine packages & food galleries, receive direct enquiries, prepare itemized quotations, negotiate proposals, and manage a digital availability calendar (block dates, prevent double-bookings).
   - **Administrator**: Comprehensive dashboard with system KPIs, caterer approvals & verification workflow, user management, and platform monitoring.

3. **Complete Commercial Workflow**:
   - Multi-step **Event Requirements Form**.
   - Side-by-side **Quotation Comparison Matrix** highlighting the best price per plate and dish variety.
   - Real-time **Negotiation & Messaging System** supporting price counter-offers and mutual agreement.
   - **Availability Management** with automated conflict prevention upon booking acceptance.
   - Verified **Rating & Review System** with star feedback and event categorization.

---

## 🛠️ Technology Stack

- **Frontend**: React 19, Tailwind CSS v4, Lucide Icons, Vite 6
- **Backend**: Node.js v24, Express.js 5, JSON Web Tokens (JWT), Bcrypt password hashing
- **Database**: Standard MySQL 8.0+ with dual engine adapter:
  - Connects directly to live MySQL server when available (`mysql2/promise`).
  - Automatically falls back to high-performance local persistent relational storage (`storage.json`) for instant out-of-the-box execution without database setup hurdles.
  - Complete pure SQL migration (`schema.sql`) and seed data (`seed.sql`) included for MySQL Workbench / phpMyAdmin.

---

## 🗄️ Database Architecture (All 14 Required Tables)

The database schema strictly adheres to the requirements:

| # | Table Name | Description & Key Foreign Keys |
|---|------------|--------------------------------|
| 1 | `Users` | Master authentication table with encrypted passwords, roles, verification status. |
| 2 | `Customers` | Customer profile linking to `Users(id)`. Stores address, city, dietary preferences. |
| 3 | `Caterers` | Caterer entity linking to `Users(id)`. Stores business name, status, rating, reviews count. |
| 4 | `Caterer_Profiles` | Rich profile data linking to `Caterers(id)`. Cuisines, price ranges, capacities, gallery, menus. |
| 5 | `Admin` | Administrative credentials and department linking to `Users(id)`. |
| 6 | `Event_Requirements` | Customer requirements linking to `Customers(id)`. Date, location, guests, budget, cuisines. |
| 7 | `Recommendations` | AI generated matches linking to `Event_Requirements(id)` and `Caterers(id)`. Score & reasons. |
| 8 | `Enquiries` | Direct customer requests linking to `Customers(id)` and `Caterers(id)`. |
| 9 | `Quotations` | Itemized proposals linking to `Enquiries(id)` and `Caterers(id)`. Per plate price, total cost, dishes. |
| 10 | `Negotiations` | Price negotiation thread linking to `Quotations(id)`. Tracks current counter-offer price. |
| 11 | `Messages` | Conversation history linking to `Negotiations(id)` and `Users(id)`. |
| 12 | `Availability` | Calendar dates linking to `Caterers(id)`. Marked 'available', 'booked', or 'blocked'. |
| 13 | `Bookings` | Confirmed bookings linking to `Quotations(id)`, `Customers(id)`, `Caterers(id)`. Unique booking code. |
| 14 | `Reviews` | Customer testimonials linking to `Caterers(id)` and `Customers(id)`. Rating (1-5 stars). |

---

## 🚀 Quick Start Guide

### 1. Install Dependencies
```bash
# Server dependencies (root directory)
npm install

# Client dependencies
npm --prefix client install
```

### 2. Build Client Production Assets
```bash
npm run build:client
```

### 3. Start the Server
```bash
npm start
```
The server will start on: **`http://localhost:5000`** serving both the REST API endpoints (`/api/*`) and the responsive React web application.

---

## 🔑 Pre-Configured Demo Accounts (1-Click Login Available)

For instant evaluation, the platform includes a **1-Click Demo Login** dropdown on the navbar and login page:

| Role | Email | Password | Pre-loaded Context |
|------|-------|----------|--------------------|
| **Customer** | `customer@demo.com` | `customer123` | Priya Sharma: Wedding reception enquiry, received quotes, active negotiations |
| **Caterer** | `caterer@royalfeast.com` | `caterer123` | Royal Feast Luxury Banquets: Active enquiries, submitted proposals, calendar |
| **Admin** | `admin@smartcatering.com` | `admin123` | Eleanor Vance: Pending caterer approvals, platform metrics, user moderation |

---

## 🧭 Site Map (All 20 Functional Pages)

1. **Home Page**: Hero section, quick search, live stats, featured caterers, 4-step workflow, cuisine chips, reviews.
2. **Find Caterers**: Advanced catalog with search, filters (location, budget, cuisine, capacity, diet) and sorting.
3. **Smart Recommendations**: Interactive AI matchmaking wizard with dynamic match scores and explanations.
4. **Caterer Details**: Profile, sample menu packages, food gallery, verified reviews, and direct quote request.
5. **Customer Registration**: Secure signup with personal and dietary preferences.
6. **Caterer Registration**: Comprehensive business onboarding with pricing, capacity, and cuisines.
7. **Login Page**: Authentication with role detection, password reset, and 1-click demo login buttons.
8. **Customer Dashboard**: Overview of requirements, enquiries, quotations, negotiations, and confirmed bookings.
9. **Caterer Dashboard**: Enquiries inbox, quotation creator, negotiation chat, and calendar manager.
10. **Admin Dashboard**: System KPIs, caterer approvals/suspensions, user list, and enquiry monitoring.
11. **Event Requirements Form**: Multi-step wizard capturing event parameters to trigger instant matchmaking.
12. **Enquiry Page / Modal**: Direct quote request modal for specific caterers.
13. **Quotation Comparison Page**: Side-by-side comparison matrix highlighting the best price deal.
14. **Negotiation / Messaging Page**: Real-time communication thread with counter-offer price proposals.
15. **Availability Calendar**: Visual schedule manager with conflicting booking prevention.
16. **About Us**: Platform philosophy, verified kitchen standards, and gastronomy mission.
17. **How It Works**: 8-step breakdown of the complete customer-to-caterer workflow.
18. **Contact Us**: Contact information, headquarters address, and support ticketing form.
19. **User Profile**: Personal info, contact details, dietary settings, and avatar management.
20. **FAQ Page**: Comprehensive questions and answers for hosts and catering businesses.

---

## 📂 MySQL Import (Optional)
If you wish to use a live MySQL instance instead of the built-in storage:
1. Ensure MySQL is running on port 3306.
2. Import `server/database/schema.sql` and `server/database/seed.sql` into your database.
3. Configure your credentials in `.env` (`DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, `DB_PORT`).
4. Restart the server; it will automatically detect and link to MySQL!

