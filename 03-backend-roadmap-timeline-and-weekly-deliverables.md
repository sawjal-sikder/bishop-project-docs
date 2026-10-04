# HireConn Backend — 16-Week Implementation Roadmap & Weekly Milestone Tracker

> **Document Version:** 4.0.0  
> **Start Date:** October 5, 2026  
> **Target Production Launch:** January 24, 2027 (16 Weeks)

---

## 1. Baseline Audit of Existing Code vs Gaps to Bridge

An audit of your existing repository reveals that only the architectural foundation is present.

### What Is Already Done:

1. **Repository Setup:** Basic microservice repository structure is in place.
2. **Architectural Skeleton:** Service directories (`api-gateway/`, `identity-profile-service/`, `feed-service/`, `jobs-service/`, `chat-service/`, `notification-service/`, `ai-assistant-service/`) have been initialized with their foundational frameworks (Django/FastAPI).
3. **Infrastructure Planning:** High-level architecture design is completed, but no database models, business logic, or API endpoints have been implemented yet.

---

### What Remains to Be Done (The Next 16-Week Scope):

To achieve **100% parity with the Flutter frontend application**, the entire backend feature set must be built from scratch within the architectural skeleton:

1. **API Gateway:** Django-based reverse proxy routing and aggregation.
2. **Auth Service:** User registration, activation, OTP, login, token refresh, forgot password, Incognito Mode, Account Deletion, and authenticated password change.
3. **Profile Service:** 
   - Personal Profile creation, bios, work, interests taxonomy, 6-photo carousel.
   - Business Profile creation, categories, licensing, operating hours, contact privacy.
   - Profile Linking & 1-tap switching.
4. **Social Graph & Search:** Connection requests, mutual connections, business watchers, Discover Geo-Distance Search Engine, Find a Business Search Engine, QR scan instant resolution.
5. **Feed Service:** Post creation (Reflection, Question, Announcement, Resource), durations, rich attachments, recommendation timelines, 6 sentiment reactions, 6 typed comments, threaded replies, and bookmarks.
6. **Jobs Service:** Opportunity creation, job applications with resume uploads, express interest flows, and employer review dashboards.
7. **Chat Service:** Real-time Socket.IO chat, 1:1 conversations, media attachments, edits, unsends, pinning, embedded cards, and translation.
8. **Notifications & AI Assistant:** In-app feeds, push notifications, email templates, and Vine AI rewriting proxy.
9. **End-to-End Flutter Integration:** Full integration with the frontend app and production launch.

---

## 2. 16-Week Master Milestone Roadmap

| Phase                          |     Weeks     | Target Dates                | Focus Domain & Key Deliverables                                                                                                                                            |
| ------------------------------ | :-----------: | :-------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Phase 1: Gateway, Auth & Profiles** | **W01 – W04** | Oct 5 – Nov 1, 2026         | API Gateway routing, User registration/login, Personal & Business Profile CRUD, Profile linking, Verification requests.                            |
| **Phase 2: Social & Search**   | **W05 – W08** | Nov 2 – Nov 29, 2026        | Connection requests, Mutual connections, Business watchers, Discover geo-distance search engine, Find Business search, QR identity system.                       |
| **Phase 3: Feed & Jobs**       | **W09 – W12** | Nov 30 – Dec 27, 2026       | Post types, Expiration durations, Sentiment reactions, Typed comments with media, Threaded replies, Job opportunities & candidate review.           |
| **Phase 4: Chat, AI & Launch** | **W13 – W16** | Dec 28, 2026 – Jan 24, 2027 | Socket.IO chat engine, Media & reactions in chat, Push/Email notifications, Vine AI assistant, End-to-end integration, and Production Launch. |

---

## 3. Week-by-Week Detailed Breakdown & "What I Am Done" Checklists

---

### PHASE 1: Gateway, Auth & Profile Implementation (Weeks 1 – 4)

#### Week 1: API Gateway, Media Uploads & Core Authentication
**Dates:** October 5, 2026 – October 11, 2026  
**Goal:** Build the API Gateway reverse proxy, set up S3 uploads, and implement core user authentication (signup, login, OTP).

- [ ] **`GW-01`**: Implement API Gateway reverse proxy routing to backend services.
- [ ] **`CORE-01`**: Deploy central media upload pre-signed URL generator (`POST /api/media/v1/presign-upload/`).
- [ ] **`AUTH-01`**: Implement User registration, OTP generation, and account activation.
- [ ] **`AUTH-02`**: Implement Login, JWT token generation, and token refresh.
- [ ] **`AUTH-03`**: Implement Forgot Password and authenticated password change.
- [ ] **`AUTH-04`**: Implement Incognito Mode toggle and Account soft deletion.

#### Week 2: Personal Profile Service
**Dates:** October 12, 2026 – October 18, 2026  
**Goal:** Build Personal Profile creation, bio management, interests taxonomy, and photo carousels.

- [ ] **`PROF-01`**: Create `Profile` models and basic CRUD endpoints (`MeProfileView`).
- [ ] **`PROF-02`**: Implement `feed_profile_tagline`, `work` fields, and bio constraints.
- [ ] **`PROF-03`**: Implement 6-photo carousel array handling and reordering.
- [ ] **`PROF-04`**: Create master `Interest` taxonomy seed database and selection endpoints.
- [ ] **`PROF-05`**: Enforce public profile visibility rules (suppress incognito profiles).

#### Week 3: Business Profile Service
**Dates:** October 19, 2026 – October 25, 2026  
**Goal:** Build Business Profiles with sub-categories, licensing, operating hours, and contact privacy.

- [ ] **`PROF-06`**: Create Business Profile models (sub-categories, insurance, licensing, languages, years active).
- [ ] **`PROF-07`**: Implement business weekly operating hours schedule endpoint.
- [ ] **`PROF-08`**: Implement business contact information endpoint with public/private visibility toggles.
- [ ] **`PROF-09`**: Ensure public preview endpoints respect privacy toggles.

#### Week 4: Profile Linking, Settings & Verification
**Dates:** October 26, 2026 – November 1, 2026  
**Goal:** Build account linking between Personal Profile and Business Page, context switching, and user settings.

- [ ] **`PROF-10`**: Implement `ProfileLink` table and 1-tap profile context switching.
- [ ] **`PROF-11`**: Business verification badge request submission and status tracking.
- [ ] **`PROF-12`**: Sync communication email preferences and privacy settings.
- [ ] **`PROF-13`**: First name change request intake.

---

### PHASE 2: Social Graph, Discovery Engine & QR System (Weeks 5 – 8)

#### Week 5: Connection Requests & Active Connections
**Dates:** November 2, 2026 – November 8, 2026  
**Goal:** Build connection request workflow (send, accept, decline, withdraw) and active connections management.

- [ ] **`SOC-01`**: Create `Connection` model and implement request endpoints.
- [ ] **`SOC-02`**: Implement action endpoints: accept, decline, withdraw.
- [ ] **`SOC-03`**: Implement pending request lists with cursor pagination.
- [ ] **`SOC-04`**: Implement active connections list and remove connection endpoint.

#### Week 6: Mutual Connections & Business Watchers
**Dates:** November 9, 2026 – November 15, 2026  
**Goal:** Calculate mutual connections and deliver business "Watch" subscriptions.

- [ ] **`SOC-05`**: Implement mutual connections intersection algorithm.
- [ ] **`SOC-06`**: Implement business watch/unwatch endpoints.
- [ ] **`SOC-07`**: Implement business owner watchers listing and search.
- [ ] **`SOC-08`**: Implement personal user watched businesses list.

#### Week 7: Discover Geo-Distance Search Engine & Blocked Accounts
**Dates:** November 16, 2026 – November 22, 2026  
**Goal:** Build nearby personal profile discovery engine and user blocking.

- [ ] **`SOC-09`**: Integrate geospatial distance calculation (PostGIS/Haversine).
- [ ] **`SOC-10`**: Implement Discovery endpoint with filters (Gender, Age, Location, Distance, Shared interests).
- [ ] **`SOC-11`**: Implement user blocking system and suppress blocked/incognito users from search.

#### Week 8: Find a Business Search & QR Identity Resolution
**Dates:** November 23, 2026 – November 29, 2026  
**Goal:** Implement full-text business search and QR code generation/resolution.

- [ ] **`SOC-12`**: Implement basic and advanced business search endpoints.
- [ ] **`SOC-13`**: QR code token issuance endpoint.
- [ ] **`SOC-14`**: QR resolution endpoint returning full profile data for scanned codes.

---

### PHASE 3: Feed Engine, Comments & Job Opportunities (Weeks 9 – 12)

#### Week 9: Social Post Publishing & Rich Attachments
**Dates:** November 30, 2026 – December 6, 2026  
**Goal:** Build Post models, expiry lifecycles, and rich attachment support.

- [ ] **`FEED-01`**: Create `Post` model with `post_type` and `post_duration` fields.
- [ ] **`FEED-02`**: Support background context notes and visibility targeting.
- [ ] **`FEED-03`**: Implement rich attachments (galleries, video, PDF, audio).
- [ ] **`FEED-04`**: Implement post edit and delete endpoints.

#### Week 10: Recommendation Timelines, Reactions & Bookmarks
**Dates:** December 7, 2026 – December 13, 2026  
**Goal:** Build recommendation timeline queries and 6-sentiment reactions.

- [ ] **`FEED-05`**: Implement timeline endpoint with pagination and recommendation ranking.
- [ ] **`FEED-06`**: Build multi-sentiment reaction system with atomic counters.
- [ ] **`FEED-07`**: Implement bookmark/save post endpoint and saved posts query.
- [ ] **`FEED-08`**: Implement repost endpoint.

#### Week 11: Typed Comments, Threaded Replies & Activities
**Dates:** December 14, 2026 – December 20, 2026  
**Goal:** Build 6 typed comments, threaded replies, and feed activity dashboards.

- [ ] **`FEED-09`**: Create `Comment` model supporting 6 types and media attachments.
- [ ] **`FEED-10`**: Implement threaded recursive replies.
- [ ] **`FEED-11`**: Implement comment sorting strategies (best discussions, latest, etc.).
- [ ] **`FEED-12`**: Build Feed activities dashboard endpoints (My Posts, My Comments, My Reactions).

#### Week 12: Job Opportunities & Candidate Applications
**Dates:** December 21, 2026 – December 27, 2026  
**Goal:** Build recruitment engine, job postings, and candidate applications.

- [ ] **`JOBS-01`**: Create `Opportunity` model and job posting endpoints.
- [ ] **`JOBS-02`**: Implement opportunity search engine.
- [ ] **`JOBS-03`**: Build candidate job application submission with resume uploads and EEOC fields.
- [ ] **`JOBS-04`**: Express interest ("Notify") flow for lightweight applications.
- [ ] **`JOBS-05`**: Employer candidate review dashboard endpoints.

---

### PHASE 4: Real-Time Chat, Notifications, AI Assistant & Launch (Weeks 13 – 16)

#### Week 13: Real-Time Chat Engine
**Dates:** December 28, 2026 – January 3, 2027  
**Goal:** Build Socket.IO chat service, 1:1 messaging, and media attachments.

- [ ] **`CHAT-01`**: Deploy Socket.IO cluster with JWT authentication.
- [ ] **`CHAT-02`**: Build Conversation models, inbox management, and unread counts.
- [ ] **`CHAT-03`**: Implement real-time message sending and history pagination.
- [ ] **`CHAT-04`**: Support chat media attachments (photos, videos, PDFs, voice).
- [ ] **`CHAT-05`**: Implement in-place message editing and unsends.

#### Week 14: Chat Reactions, Pins, Embeds & Broadcasts
**Dates:** January 4, 2027 – January 10, 2027  
**Goal:** Deliver advanced chat features (reactions, pins, translation).

- [ ] **`CHAT-06`**: Implement message pinning and quick navigation.
- [ ] **`CHAT-07`**: Real-time message reactions with emoji pickers.
- [ ] **`CHAT-08`**: Support embedded post/comment cards in chat.
- [ ] **`CHAT-09`**: In-chat message translation endpoint.
- [ ] **`CHAT-10`**: Business "Message Watchers" broadcast endpoint.

#### Week 15: Notifications & Vine AI Assistant
**Dates:** January 11, 2027 – January 17, 2027  
**Goal:** Deploy event consumers, notifications, and AI features.

- [ ] **`NOTIF-01`**: Build Celery/RabbitMQ event consumers for platform events.
- [ ] **`NOTIF-02`**: Implement in-app notification feed.
- [ ] **`NOTIF-03`**: Integrate Firebase Cloud Messaging (FCM) & Apple APNs for push notifications.
- [ ] **`NOTIF-04`**: Transactional email dispatch honoring user preferences.
- [ ] **`AI-01`**: Build Vine AI rewriting proxy for text expansion/shortening/tone.

#### Week 16: Security Audit, Load Testing & Production Launch
**Dates:** January 18, 2027 – January 24, 2027  
**Goal:** Finalize system integration, performance tuning, and launch.

- [ ] **`SYS-01`**: End-to-end regression testing with the Flutter frontend.
- [ ] **`SYS-02`**: Database performance tuning (indices, query optimization).
- [ ] **`SYS-03`**: Security audit (JWT checks, Gateway rate limiting, CORS).
- [ ] **`SYS-04`**: Concurrency load testing.
- [ ] **`SYS-05`**: Production cloud deployment setup (AWS).
- [ ] **`SYS-06`**: Final client sign-off and production handover.
- **Final Launch Milestone (Sunday, January 24, 2027):**
