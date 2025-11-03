# Unimob

**Your campus life, all in one place.**

[![Live Project](https://img.shields.io/badge/Live-unimob.in-teal)](https://unimob.in)
[![Tech Stack](https://img.shields.io/badge/Stack-SvelteKit%20%7C%20Go%20%7C%20PostgreSQL-blue)]()

---

## 📋 Project Overview

### Description
Unimob is a unified campus platform that brings together study materials, discussion forums, and community networking for students, aspirants, and alumni. We're solving the fragmentation problem in campus life where students juggle multiple WhatsApp groups, scattered Google Drive links, and expensive subscription services.

### Problem Statement
Students face:
- **Scattered Resources:** Notes and materials spread across dozens of Drive links and messaging groups
- **Disorganized Communication:** Multiple WhatsApp groups with no structure or searchability
- **High Costs:** Expensive subscription services for basic study materials
- **Poor Connectivity:** No efficient way to connect with seniors, juniors, or alumni
- **Lack of Organization:** No centralized hub for campus-related information and discussions

### Key Features

#### 🎓 Smart Study Materials Hub
- **Global Subject Library:** Organized notes that work across colleges with intelligent categorization
- **Smart Search & Filtering:** Find materials by college, program, or field instantly
- **Fair Credit Economy:** Earn credits by sharing quality notes; access premium content without subscriptions
- **Admin Approval System:** Quality control ensures only valuable resources earn credits
- **PDF Rendering:** Seamless document viewing with pdf2htmlEX integration

#### 💬 Organized Discussion Forums
- **Multi-Level Hierarchy:** Forums organized by Institute → Program → Field
- **Cross-Generation Networking:** Connect with juniors, seniors, and alumni in one place
- **Interest Communities:** Clubs, sports groups, and hobby-based discussions
- **Real-time Engagement:** Post, comment, and vote on discussions

#### 🔐 Verified Community
- **Invite-Only System:** Controlled growth with verified users (~500 members currently)
- **Institute Verification:** Automatic verification through unique institution mappings
- **Secure Payments:** Razorpay integration for premium features

### Tech Stack

**Frontend:**
- SvelteKit (Static Build)
- DaisyUI + Tailwind CSS
- TypeScript

**Backend:**
- Go (Golang)
- Chi Router
- PostgreSQL Database

**Infrastructure & Tools:**
- DigitalOcean VPS
- Nginx (Reverse Proxy)
- pdf2htmlEX (PDF Rendering)
- Razorpay (Payment Gateway)

---

## 🏗️ System Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Client Layer                          │
│              (SvelteKit Static Frontend)                     │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTPS
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Nginx Reverse Proxy                       │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   Go Backend (Chi Router)                    │
│  ┌──────────────┬──────────────┬──────────────┬──────────┐ │
│  │   Auth       │   Materials  │   Forums     │ Credits  │ │
│  │   Service    │   Service    │   Service    │ Service  │ │
│  └──────┬───────┴──────┬───────┴──────┬───────┴────┬─────┘ │
└─────────┼──────────────┼──────────────┼────────────┼───────┘
          │              │              │            │
          └──────────────┴──────────────┴────────────┘
                         │
                         ▼
          ┌──────────────────────────────┐
          │   PostgreSQL Database        │
          │                              │
          │  • Users & Auth              │
          │  • Institutes/Programs       │
          │  • Study Materials           │
          │  • Forums & Posts            │
          │  • Credits System            │
          └──────────────────────────────┘
```

### Component Interaction Flow

#### 1. User Onboarding
```
User Request → Invite Validation → Registration → 
Institute Selection → Program/Field Mapping → 
Account Creation → Access Granted
```

#### 2. Study Materials Flow
```
User Uploads PDF → Backend Processing (pdf2htmlEX) → 
Admin Review Queue → Approval Decision → 
(If Approved) Credits Awarded + Material Published → 
Searchable in Global Library
```

#### 3. Forum Interaction
```
User Creates Post → Forum Level Selection 
(Institute/Program/Field) → 
Post Stored with Hierarchy → Other Users View/Comment/Vote → 
Engagement Tracked
```

#### 4. Credit Economy
```
Upload Approved Material → Earn Credits → 
Browse Premium Content → Spend Credits → 
Access Unlocked
```

### Database Architecture

**Core Tables:**
- `meerkat` (users table - singular naming convention)
- `institute` - Educational institutions
- `program` - Academic programs (e.g., B.Tech, MBA)
- `field` - Specific fields of study (e.g., Computer Science)
- `institute_program_field` - Unique mapping table for each college configuration
- `material` - Study resources with metadata
- `forum` - Discussion forums with hierarchy
- `post` - User posts and comments
- `credit_transaction` - Credit earning/spending log

**Key Features:**
- UUID primary keys for all tables
- Foreign key constraints for data integrity
- Hierarchical organization with single-table mapping
- Single-quote string literals in SQL

---

## 🚀 Deployment Information

### Live Project
**URL:** [https://unimob.in](https://unimob.in)

### Hosting Details
- **Provider:** DigitalOcean VPS (Ubuntu Linux)
- **Web Server:** Nginx
- **Application Server:** Go binary with systemd service
- **Database:** PostgreSQL (same server)

### Architecture Setup
```
Internet → DigitalOcean VPS
           ├── Nginx (Port 80/443)
           │   └── Reverse proxy to Go app
           ├── Go Backend (Internal port)
           └── PostgreSQL (Port 5432)
```

### Basic Setup Overview
1. **Frontend Build:** SvelteKit static build deployed to VPS
2. **Backend Service:** Go binary running as systemd service
3. **Database:** PostgreSQL with manual migrations
4. **SSL/TLS:** HTTPS enabled via Nginx configuration
5. **PDF Processing:** pdf2htmlEX installed for document rendering

---

## 🔮 Feature Enhancement Scope

### Planned Enhancements for Next Phase

#### 1. **Alumni Network Integration** 🎯
**Purpose:** Create a dedicated alumni engagement system to bridge the gap between current students and graduates.

**Features:**
- Alumni profiles with graduation year, current company, and expertise
- Mentorship matching system
- Career guidance forums
- Job posting and referral system
- Alumni-exclusive networking events

**Expected Impact:**
- Strengthens institutional connections across generations
- Provides career guidance to current students
- Creates value for alumni to stay engaged
- Opens B2B opportunities with corporate partnerships

#### 2. **Campus Club Management System** 🎪
**Purpose:** Solve the problem of clubs struggling to reach students and manage events effectively.

**Features:**
- Club registration and verified handles
- Event creation and promotion tools
- Centralized event calendar
- Attendance tracking and certificates
- Club-specific forums and announcements

**Expected Impact:**
- Increases event attendance by 3-5x through centralized discovery
- Reduces administrative burden on club organizers
- Improves campus engagement metrics
- Creates a single source of truth for campus activities

#### 3. **Ad Server for Campus Opportunities** 💼
**Purpose:** Monetization through relevant, non-intrusive advertisements for internships, events, and student-focused products.

**Features:**
- Targeted ad placement based on program/field
- Internship and job opportunity ads
- Campus event promotions
- Student product/service marketplace
- Revenue sharing with content creators

**Expected Impact:**
- Sustainable revenue model without user subscriptions
- Value-added content (job opportunities) instead of disruptive ads
- Support for student entrepreneurship
- Scalable across multiple institutions

#### 4. **Mobile Application** 📱
**Purpose:** Increase accessibility and engagement through native mobile experience.

**Tech Stack:**
- React Native (based on your prototyping experience)
- Shared Go backend APIs
- Push notifications for forum updates and events

**Expected Impact:**
- Higher daily active users (mobile-first student behavior)
- Push notifications increase engagement by 40-60%
- Offline access to downloaded study materials
- Location-based features for campus events

---

## 👥 Contributors

### Core Team

**Nikhil Mishra** - Full Stack Developer

**Manik Zutshi** - Full Stack Developer

---

## 📊 Current Status

- **Launch Date:** May 2025
- **Current Users:** ~300 members (invite-only) (1000+ before invite-only)
- **Institutions:** YMCA, Faridabad.
- **Study Materials:** Growing library with credit-based economy
- **Growth Model:** Controlled expansion with verified communities

---

## 🎯 Future Vision

Unimob aims to become the **default campus operating system** for Indian universities—where every student naturally goes for:
- Study materials and academic resources
- Peer discussions and community engagement
- Alumni networking and career guidance
- Campus events and club activities
- Professional development opportunities

By centralizing fragmented campus experiences, we're building more than a platform—we're creating an ecosystem where students, alumni, and institutions collaborate seamlessly.

---

## 📞 Contact

For inquiries, partnerships, or feedback:
- **Website:** [unimob.in](https://unimob.in)
- **Project Type:** Education Technology / Social Impact

**Built with ❤️ by students, for students.**
