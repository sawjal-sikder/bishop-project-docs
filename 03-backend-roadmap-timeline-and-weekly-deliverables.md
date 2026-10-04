# HireConn Backend — 16-Week Implementation Roadmap & Weekly Milestone Tracker

> **Document Version:** 3.0.0  
> **Start Date:** October 5, 2026  
> **Target Production Launch:** January 24, 2027 (16 Weeks)  
> **Existing Codebase Baseline:** `/home/mohammadsajal/sajal/projects/bishop/bishop-backend-microservice`  
> **Frontend Source of Truth:** `/home/mohammadsajal/sajal/projects/bishop/bishop-frontend/gebenga_hireconn_share`  
> **Target Audience:** Engineering Team, Backend Developers (DRF), Project Managers, Client Stakeholders  

---

## 1. Baseline Audit of Existing Code vs Gaps to Bridge

An audit of your existing repository at [`/home/mohammadsajal/sajal/projects/bishop/bishop-backend-microservice`](file:///home/mohammadsajal/sajal/projects/bishop/bishop-backend-microservice) reveals a solid architectural foundation with several service skeletons already in place:


---

### What Remains to Be Done (The Next 16-Week Scope):
To achieve **100% parity with the Flutter frontend application**, the following features and upgrades must be completed:

1. **Auth Service Gaps:** Incognito Mode toggle, Account Deletion survey feedback capture, and authenticated password change.
2. **Profile Service Gaps:**
   - Personal Profile: Feed tagline (max 20 chars), Work (max 35 words), Interests taxonomy selection, and 6-photo carousel management.
   - Business Profile: Sub-categories, business insurance, licensing number/text, business languages, years active taxonomy, response time, and operating hours schedule.
   - Profile Linking & Switching: Database link between Personal Profile and Business Page, link confirmation, and 1-tap profile context switching.
   - First Name change request intake and verification badge approval status.
3. **Social Graph Gaps:**
   - Mutual connections intersection calculation (`/users/{id}/mutual-connections/`).
   - Discover Geo-Distance Search Engine (PostGIS/Haversine distance calculation, age range sliders, gender filters, location preference: Near Me / Another City / Anywhere, shared interests).
   - Find a Business Search Engine (Basic and Advanced search by size, type, years active, language, verified only).
   - QR scan instant resolution returning full personal/business profiles.
4. **Feed & Activities Gaps:**
   - Post types (`Reflection`, `Question`, `Announcement`, `Resource`), post durations (`24 hours`, `7 days`, `30 days`, `Evergreen`) with automatic expiration calculation (`expires_at`), rich attachments (multi-image gallery, video thumbnail, PDF document, voice note with consent tracking), and background context notes.
   - Timeline suggestion ranking (`Relevant to You`, `Connections Engaged`, `Trending`).
   - Multi-type reactions (Like, Favorite, Credible, Insightful, Debatable, Relevant).
   - 6 Typed Comments (`Insight`, `Question`, `Offer`, `Resource`, `Counterpoint`, `General`), media attachments on comments, threaded recursive replies (`ReplyModel`), and comment sorting (`bestDiscussions`, `latestReplies`, `byConversation`, etc.).
   - User Feed Activities dashboard (My Posts, My Comments, My Reactions, My Applied, My Notified).
5. **Jobs & Opportunities Gaps:**
   - Full application fields: Statement of interest, PDF resume storage, work authorization, visa sponsorship, work/location preferences, and voluntary EEOC demographics.
   - Express interest ("Notify" flow) without resume.
   - Employer application review dashboard (status: submitted, interview, accepted, rejected).
6. **Chat Service Gaps:**
   - Media attachments (image galleries, videos, PDFs, audio voice notes), in-place editing (`is_edited`), unsend/delete for all, emoji reactions (Love, Approved, Laughing, Eyes, Person, Idea), message pinning and scroll-to-pinned, shared post/comment rich cards (`sharedFeed`, `sharedComment`), in-chat message translation, and business "Message Watchers" broadcast announcements.
7. **Notifications & AI Assistant Gaps:**
   - Notification action CTAs (View Post, View Application, Open Chat, View Profile), push notification token registration (FCM/APNs), transactional email templates honoring communication preferences.
   - Vine AI Assistant prompt tuning matching the mobile widget (Audiences, Tones, Structure: Shorten/Expand).
8. **End-to-End Flutter Integration:**
   - Full integration with all screens in `lib/screens/` and `lib/app_features/`.

---

## 2. 16-Week Master Milestone Roadmap

| Phase | Weeks | Target Dates | Focus Domain & Key Deliverables |
|---|:---:|:---|:---|
| **Phase 1: Auth & Profiles** | **W01 – W04** | Oct 5 – Nov 1, 2026 | Baseline audit, Gateway hardening, Incognito mode, Personal 6-photo carousel, Business hours, Profile linking & switching, Verification badges. |
| **Phase 2: Social & Search** | **W05 – W08** | Nov 2 – Nov 29, 2026 | Connection requests lifecycle, Mutual connections, Business watchers, Discover geo-distance search engine, Find Business search, QR identity system. |
| **Phase 3: Feed & Jobs** | **W09 – W12** | Nov 30 – Dec 27, 2026 | Post types, 4 expiration durations, 6 sentiment reactions, 6 typed comments with media, Threaded replies, Feed activities, Job opportunities & candidate review. |
| **Phase 4: Chat, AI & Launch** | **W13 – W16** | Dec 28, 2026 – Jan 24, 2027 | Socket.IO chat upgrade (voice notes, pins, reactions, translation, broadcast), Push/Email notifications, Vine AI assistant, End-to-end integration, and Production Launch. |

---

## 3. Week-by-Week Detailed Breakdown & "What I Am Done" Checklists

---

### PHASE 1: Auth & Profile Expansion (Weeks 1 – 4)

#### Week 1: Gateway Hardening, S3 Upload Pipeline & Auth Service Completion
**Dates:** October 5, 2026 – October 11, 2026  
**Goal:** Harden API Gateway, deploy direct S3 pre-signed upload URL endpoint, and complete missing Auth features.
- [ ] **`GW-01`**: Verify API Gateway routes, CORS headers, rate limits, and trusted identity headers (`X-User-Id`, `X-User-Type`, `X-Request-Id`).
- [ ] **`CORE-03`**: Deploy central media upload pre-signed URL generator (`POST /api/media/v1/presign-upload/`) for Images, Videos, Audio notes, and PDFs.
- [ ] **`AUTH-06`**: Implement authenticated password change endpoint (`POST /api/auth/v1/password/change/`).
- [ ] **`AUTH-08`**: Implement Incognito Mode toggle endpoint (`PATCH /api/auth/v1/account/incognito/`) and state query.
- [ ] **`AUTH-07`**: Implement soft delete endpoint (`POST /api/auth/v1/account/delete/`) with feedback survey logging.
- **Mobile Screens Enabled:** `LoginScreen`, `SignUpScreen`, `OtpVerificationScreen`, `ChangePasswordScreen`, `DeleteAccountsScreen`.
- **Weekly Client Demo Milestone (Friday, Oct 9, 2026):** Upload photos to S3 via pre-signed URLs, log in on the Flutter app, toggle Incognito mode, and test password change.

#### Week 2: Personal Profile Expansion (Bio/Work Limits, Tagline, Interests & 6-Photo Carousel)
**Dates:** October 12, 2026 – October 18, 2026  
**Goal:** Upgrade `profileapp` to match `PersonalHomePage` (character constraints, tagline, interests taxonomy, and multi-photo carousel).
- [ ] **`PROF-01A`**: Add missing fields to `Profile` model: `feed_profile_tagline` (max 20 chars), `work` (max 35 words), and bio length enforcement (max 240 chars).
- [ ] **`PROF-01B`**: Implement 6-photo carousel array handling (`profile_photos` list with reordering, active indicators, and deletion).
- [ ] **`PROF-02A`**: Create master `Interest` taxonomy seed database (Technology, Design, Marketing, Health, etc.).
- [ ] **`PROF-02B`**: Implement `GET /api/profile/v1/interests/taxonomy/` and `GET/PUT /api/profile/v1/personal/me/interests/`.
- [ ] **`PROF-01C`**: Enforce public profile visibility rules (suppress profiles with `is_incognito = True`).
- **Mobile Screens Enabled:** `PersonalHomePage`, `PersonalPageDetailsScreen`, `EditPhotoScreen`.
- **Weekly Client Demo Milestone (Friday, Oct 16, 2026):** Personal user edits tagline, bio, and work summary, selects interest badges, and manages 6-photo carousel on the mobile app.

#### Week 3: Business Profile Expansion (Sub-Categories, Licensing, Hours & Contact Privacy)
**Dates:** October 19, 2026 – October 25, 2026  
**Goal:** Upgrade business profiles with sub-categories, licensing, operating hours schedule, and contact privacy toggles.
- [ ] **`PROF-03A`**: Expand business profile fields: `business_sub_category`, `is_business_insured`, `have_license`, `license_text`, `business_languages` array, `years_active` options, and `response_time_text`.
- [ ] **`PROF-04`**: Implement business weekly operating hours schedule endpoint (`GET/PUT /api/profile/v1/business/me/hours/`) storing Mon–Sun open/close times and closed days.
- [ ] **`PROF-05`**: Implement business contact information endpoint (`PATCH /api/profile/v1/business/me/contact-info/`) with public/private visibility toggles for email and phone.
- [ ] **`PROF-05B`**: Ensure public preview endpoint (`GET /api/profile/v1/business/{id}/`) hides email/phone if visibility is set to private.
- **Mobile Screens Enabled:** `BusinessBasicScreen`, `DescribeYourBusinessScreen`, `BusinessHoursScreen`, `ContactInformationScreen`, `BusinessPreviewPage`.
- **Weekly Client Demo Milestone (Friday, Oct 23, 2026):** Business owner configures hours and contact details; personal user views public preview with hidden private contact info.

#### Week 4: Profile Linking & Context Switching, Verification Badges & Settings Sync
**Dates:** October 26, 2026 – November 1, 2026  
**Goal:** Build account linking between Personal Profile and Business Page, 1-tap switching, verification badge request, and email/privacy settings.
- [ ] **`PROF-06`**: Work samples gallery CRUD (`POST/DELETE /api/profile/v1/business/me/work-samples/`).
- [ ] **`PROF-07A`**: Implement `ProfileLink` table linking Personal User ID and Business User ID with request and confirmation endpoints.
- [ ] **`PROF-07B`**: Implement 1-tap profile context switching endpoint returning authentication tokens for the linked profile.
- [ ] **`PROF-08`**: Business verification badge request submission and status tracking (`/api/profile/v1/business/me/request-verification/`).
- [ ] **`PROF-09`**: Sync communication email preferences (`GET/PATCH /api/profile/v1/preferences/emails/`).
- [ ] **`PROF-10`**: Sync privacy and messaging preferences (`allow_direct_messages`, `default_translation_language`, `is_connection_public`).
- [ ] **`PROF-11`**: First name change request intake.
- **Mobile Screens Enabled:** `PersonalHomePage` ("Link Business Pages" card), `BusinessPreviewPage`, `RequestVerificationScreen`, `CommunicationPreferencesScreen`, `ManagePreferencesScreen`, `ChangeFirstNameScreen`.
- **Weekly Client Demo Milestone (Friday, Oct 30, 2026):** Phase 1 complete sign-off; link personal profile to business page, test 1-tap switching, and submit verification badge request.

---

### PHASE 2: Social Graph, Discovery Engine & QR System (Weeks 5 – 8)

#### Week 5: Social Graph — Connection Requests Lifecycle & Active Connections Management
**Dates:** November 2, 2026 – November 8, 2026  
**Goal:** Complete connection request workflow (send, accept, decline, withdraw) and active connections management.
- [ ] **`SOC-01A`**: Refine `Connection` model and implement `POST /api/social/v1/connections/request/` with validation (cannot connect to self or existing connection).
- [ ] **`SOC-01B`**: Implement action endpoints: `accept/`, `decline/`, and `withdraw/`.
- [ ] **`SOC-01C`**: Implement incoming and outgoing pending request list endpoints with cursor pagination.
- [ ] **`SOC-02`**: Implement active connections list (`GET /api/social/v1/connections/`) and remove connection endpoint (`DELETE /connections/{user_id}/`).
- **Mobile Screens Enabled:** `PersonalCircleScreen` (New Requests, Sent Requests, All Connections tabs).
- **Weekly Client Demo Milestone (Friday, Nov 6, 2026):** Send connection request between two mobile devices, accept request, and manage active connections.

#### Week 6: Social Graph — Mutual Connections Calculation & Business Watchers Subscriptions
**Dates:** November 9, 2026 – November 15, 2026  
**Goal:** Calculate mutual connections between two users, and deliver business "Watch" subscriptions.
- [ ] **`SOC-03`**: Mutual connections intersection algorithm (`GET /api/social/v1/users/{id}/mutual-connections/`) returning mutual count and profile previews.
- [ ] **`SOC-04A`**: Implement watch/unwatch endpoints (`POST/DELETE /api/social/v1/business/{id}/watch/`).
- [ ] **`SOC-04B`**: Implement business owner watchers listing and search endpoint (`GET /api/social/v1/business/me/watchers/`).
- [ ] **`SOC-04C`**: Implement personal user watched businesses list (`GET /api/social/v1/personal/me/watched-businesses/`).
- **Mobile Screens Enabled:** `MutualFriendScreen`, `CircleWatchingListScreen`, `WatchersScreen`.
- **Weekly Client Demo Milestone (Friday, Nov 13, 2026):** Personal user watches business page; business owner searches watchers; view mutual friends on profile.

#### Week 7: Social Graph — Discover Geo-Distance Search Engine & Blocked Accounts
**Dates:** November 16, 2026 – November 22, 2026  
**Goal:** Nearby personal profile discovery engine with distance calculations, age sliders, location filters, and user blocking.
- [ ] **`SOC-05A`**: Integrate geospatial distance calculation (PostGIS or Haversine formula) in miles.
- [ ] **`SOC-05B`**: Implement `GET /api/social/v1/discover/profiles/` supporting all filters from `DiscoverFilterData` (Gender, Age range, Location preference [Near Me, Another City, Anywhere], Distance radius, Shared interests).
- [ ] **`SOC-05C`**: Suppress blocked users and incognito users from search results.
- [ ] **`SOC-08`**: Implement user blocking system (`POST/DELETE /api/social/v1/blocked-accounts/` and blocked list query).
- **Mobile Screens Enabled:** `DiscoverScreen`, `DiscoverFilterScreen`, `BlockedAccountScreen`.
- **Weekly Client Demo Milestone (Friday, Nov 20, 2026):** Adjust age and distance sliders in Discover filter screen; test blocking an account to verify immediate removal from discovery.

#### Week 8: Social Graph — Find a Business Search & QR Code Identity Resolution
**Dates:** November 23, 2026 – November 29, 2026  
**Goal:** Implement full-text business search (Basic & Advanced) and QR code generation & instant scan resolution.
- [ ] **`SOC-06A`**: Implement basic business search (keyword in name/services, category, state, city).
- [ ] **`SOC-06B`**: Implement advanced business search (business size, business type, years active, language, verified badge only).
- [ ] **`SOC-07A`**: QR code token issuance (`GET /api/social/v1/qr/my-qr/`).
- [ ] **`SOC-07B`**: QR resolution endpoint (`POST /api/social/v1/qr/resolve/`) returning full profile data for scanned codes.
- **Mobile Screens Enabled:** `FindBusinessSearchScreen`, `PersonalFindBusinessPageInitial`, `PersonalFindBusinessPageDetails`, `MyQrPage`, `PersonalFindBusinessScanqr`.
- **Weekly Client Demo Milestone (Friday, Nov 27, 2026):** Phase 2 complete sign-off; scan QR code with mobile camera to immediately open business profile.

---

### PHASE 3: Feed Engine, 6 Typed Comments & Job Opportunities (Weeks 9 – 12)

#### Week 9: Feed Service — Social Post Publishing, Expiry Lifecycles & Rich Attachments
**Dates:** November 30, 2026 – December 6, 2026  
**Goal:** Upgrade `feedapp` to support post types, 4 expiration durations, rich attachments, and background context.
- [ ] **`FEED-01A`**: Add fields to `Post`: `post_type` (`Reflection`, `Question`, `Announcement`, `Resource`), `post_duration` (`hours24`, `days7`, `days30`, `evergreen`), and automatic `expires_at` calculation.
- [ ] **`FEED-01B`**: Support background context notes, conversation entry points, and visibility targeting (`Everyone`, `Connections`).
- [ ] **`FEED-02`**: Implement rich attachments: multi-image galleries, video with thumbnail, PDF documents, and audio voice notes with consent tracking.
- [ ] **`FEED-01C`**: Implement post edit and delete endpoints.
- **Mobile Screens Enabled:** `SharePostScreen`, `SharePostNextScreen`, `PostBackgroundScreen`.
- **Weekly Client Demo Milestone (Friday, Dec 4, 2026):** Publish Reflection post with video and PDF attachments, background context notes, and 7-day expiration.

#### Week 10: Feed Service — Timelines, 6 Sentiment Reactions, Reposts & Bookmarks
**Dates:** December 7, 2026 – December 13, 2026  
**Goal:** Implement recommendation timeline queries, 6 sentiment reaction counters, reposts, and bookmarks.
- [ ] **`FEED-03`**: Implement `GET /api/feed/v1/timeline/` with cursor pagination, hiding expired posts, and recommendation ranking (`RelevantToYou`, `ConnectionsEngaged`, `Trending`).
- [ ] **`FEED-04`**: Upgrade reactions to multi-sentiment system with atomic counters (Like, Favorite, Credible, Insightful, Debatable, Relevant).
- [ ] **`FEED-05`**: Implement bookmark/save endpoint (`POST /posts/{id}/save/`) and saved posts query (`GET /posts/saved/`).
- [ ] **`FEED-05B`**: Implement repost endpoint (`POST /posts/{id}/repost/`).
- **Mobile Screens Enabled:** `FeedScreen`, `PostDetailsScreen`.
- **Weekly Client Demo Milestone (Friday, Dec 11, 2026):** Scroll infinite feed timeline, react with "Insightful" and "Debatable", bookmark post, and verify counters.

#### Week 11: Feed Service — 6 Typed Comments, Threaded Replies & Feed Activities Dashboard
**Dates:** December 14, 2026 – December 20, 2026  
**Goal:** Upgrade comments with the 6 taxonomy types, threaded replies, comment sorting, and personal/business activity dashboards.
- [ ] **`FEED-06`**: Upgrade `Comment` model to support the 6 types: `Insight`, `Question`, `Offer`, `Resource`, `Counterpoint`, `General`, with media attachments (image, video, PDF, voice).
- [ ] **`FEED-07`**: Implement threaded recursive replies (`parent_comment_id` matching `ReplyModel` hierarchy).
- [ ] **`FEED-08`**: Implement comment sorting strategies: `bestDiscussions`, `latestReplies`, `byConversation`, `fromAuthor`, `differentViewpoints`.
- [ ] **`FEED-10`**: Feed activities dashboard endpoints: My Posts, My Comments, My Reactions, My Applied, My Notified.
- **Mobile Screens Enabled:** `CommentBottomSheet`, `FeedActivitiesScreen`.
- **Weekly Client Demo Milestone (Friday, Dec 18, 2026):** Post an "Insight" comment with image attachment, reply to comment, sort by "Best Discussions", and inspect Feed Activities screen.

#### Week 12: Jobs Service — Hiring Opportunity Publishing, Applications & Candidate Review
**Dates:** December 21, 2026 – December 27, 2026  
**Goal:** Complete recruitment engine: opportunity postings, opportunity search, candidate applications with resume uploads, and employer review.
- [ ] **`JOBS-01`**: Upgrade `Opportunity` model to store compensation in integer cents and add `expected_response` (`apply` vs `notify`).
- [ ] **`JOBS-02`**: Implement opportunity search engine (`GET /api/jobs/v1/opportunities/search/`).
- [ ] **`JOBS-03`**: Candidate job application submission with statement of interest, resume PDF, work preferences, work authorization, sponsorship, voluntary EEOC demographics, and idempotency key.
- [ ] **`JOBS-04`**: Express interest ("Notify" flow) for lightweight applications.
- [ ] **`JOBS-05`**: Employer candidate review dashboard (view applicants, inspect resume PDF, update status: submitted/interview/accepted/rejected).
- [ ] **`JOBS-06`**: Candidate application history endpoint (`GET /api/jobs/v1/my-applications/`).
- **Mobile Screens Enabled:** `OpportunityDetailsScreen`, `OpportunitySearchScreen`, `JobApplyScreen`, `JobApplicationDetailsScreen`, `ApplicationSuccessScreen`.
- **Weekly Client Demo Milestone (Friday, Dec 25, 2026):** Phase 3 complete sign-off; post a job opportunity, apply with resume PDF, and review candidate in employer dashboard.

---

### PHASE 4: Real-Time Chat, Notifications, AI Assistant & Launch (Weeks 13 – 16)

#### Week 13: Real-Time Chat — Socket.IO Gateway, Inboxes, Media, Edits & Unsends
**Dates:** December 28, 2026 – January 3, 2027  
**Goal:** Upgrade chat service to support Socket.IO connection, inboxes with message requests, media attachments, edits, and unsends.
- [ ] **`CHAT-01`**: Deploy Socket.IO cluster with JWT handshake authentication and Redis pub/sub adapter.
- [ ] **`CHAT-02`**: Conversation inbox management, unread count badges, and "Message Requests" isolation for non-connections.
- [ ] **`CHAT-03`**: Real-time message sending, history cursor pagination, and read receipts (`isSeen`).
- [ ] **`CHAT-04`**: Chat media attachments (photos, videos with thumbnails, PDFs, audio voice note playback).
- [ ] **`CHAT-05`**: In-place message editing (`is_edited: true`) and unsend (delete for everyone).
- [ ] **`CHAT-06`**: Threaded replies (`replyTo` message reference).
- **Mobile Screens Enabled:** `ChatListScreen`, `MessageScreen`, `ChatBubbleWidget`.
- **Weekly Client Demo Milestone (Friday, Jan 1, 2027):** Two devices chatting in real-time, sending audio voice notes, editing a sent message, and unsending a message.

#### Week 14: Real-Time Chat — Reactions, Pins, Embeds, Translation & Broadcasts
**Dates:** January 4, 2027 – January 10, 2027  
**Goal:** Deliver message reactions, pinning, embedded post/comment cards, in-chat translation, and business "Message Watchers" broadcast.
- [ ] **`CHAT-07`**: Message pinning and quick navigation (pin/unpin messages, pinned list, scroll-to-pinned).
- [ ] **`CHAT-08`**: Real-time message reactions with emoji pickers (Love, Approved, Laughing, Eyes, Person, Idea).
- [ ] **`CHAT-09`**: Embedded post cards in chat (`sharedFeed`, `sharedComment`).
- [ ] **`CHAT-10`**: In-chat message translation using user default language with Redis caching.
- [ ] **`CHAT-11`**: Business "Message Watchers" broadcast endpoint delivering asynchronous updates to all followers.
- [ ] **`CHAT-12`**: Chat moderation (block user from chat, report conversation).
- **Mobile Screens Enabled:** `MessageScreen` (Reactions/Pins/Translation), `MessageReactionPicker`, `MessageWatchersScreen`.
- **Weekly Client Demo Milestone (Friday, Jan 8, 2027):** Pin a chat bubble, translate a message, share a post card into chat, and broadcast a message to all watchers.

#### Week 15: Notifications & Vine AI Assistant Service
**Dates:** January 11, 2027 – January 17, 2027  
**Goal:** Deploy domain event consumers, in-app notification feed, mobile push alerts, transactional emails, and Vine AI rewriting proxy.
- [ ] **`NOTIF-01`**: Celery/RabbitMQ event consumers for `auth.*`, `social.*`, `feed.*`, `jobs.*`, `chat.*`.
- [ ] **`NOTIF-02`**: In-app notification feed with CTAs (View Post, View Application, Send Message).
- [ ] **`NOTIF-03`**: Firebase Cloud Messaging (FCM) & Apple APNs push notification dispatch for offline users.
- [ ] **`NOTIF-04`**: Transactional email dispatch honoring user communication preferences.
- [ ] **`AI-01`**: Vine AI rewriting proxy (`POST /api/ai/v1/vine/rewrite/`) with Audience, Tone (Professional, Friendly, Thoughtful, etc.), and Structure (Shorten, Expand).
- [ ] **`SUPP-01`**: Support ticket intake and moderation reporting (`SUPP-02`).
- [ ] **`SUPP-03`**: Admin review endpoints for business verification badges and first name changes.
- **Mobile Screens Enabled:** `NotificationScreen`, `AiWriterWidget` (Vine), `ContactSupportScreen`, `ContactUsScreen`.
- **Weekly Client Demo Milestone (Friday, Jan 15, 2027):** Receive push notifications on phone for messages and applications; test Vine AI rewriting a post with "Professional" tone.

#### Week 16: End-to-End Integration, Security Audit, Load Testing & Production Launch
**Dates:** January 18, 2027 – January 24, 2027  
**Goal:** Comprehensive Flutter mobile regression, database query optimization, load testing, and live production deployment.
- [ ] **`SYS-01`**: Complete end-to-end regression testing across all Flutter screens against staging backend.
- [ ] **`SYS-02`**: Database performance tuning (PostgreSQL foreign key indexing, spatial indices, cursor query execution plans).
- [ ] **`SYS-03`**: Security audit (JWT rotation checks, Gateway rate limiting, S3 pre-signed URL expiry verification, CORS lockdown).
- [ ] **`SYS-04`**: Concurrency load testing (simulate 1,000 concurrent Socket.IO connections and high-volume feed pagination).
- [ ] **`SYS-05`**: Automated health checks, Prometheus/Grafana metrics, and Sentry error monitoring setup.
- [ ] **`SYS-06`**: Production cloud deployment (AWS ECS / RDS / ElastiCache Redis setup).
- [ ] **`SYS-07`**: Final client sign-off and production handover.
- **Final Launch Milestone (Sunday, January 24, 2027):**  

---

