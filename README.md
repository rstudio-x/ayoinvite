# Digital Invitation Platform – Full Stack Development Specification

---

## 1. Business Requirements

### 1.1. Overview
A modern web platform allowing users to create digital event invitations (wedding, birthday, corporate, etc.), share them via link/QR/WhatsApp, collect RSVPs, manage guest check-ins, and monetize via pay-per-event or subscriptions. The platform must include separate dashboards for users (hosts) and administrators, and support QR-based payment via DOKU.

### 1.2. Core Objectives
- Enable seamless invitation creation with customizable templates.
- Support RSVP, guest management, and gift/wishlist features.
- Provide analytics and check-in (QR) functionality.
- Allow sharing via link, QR code, and WhatsApp.
- Monetize via pay-per-event, subscriptions, or premium features.
- Admin dashboard for platform management, moderation, and analytics.
- Secure, scalable, and user-friendly.

---

## 2. Functional Requirements

### 2.1. User (Host) Features
- Sign up/log in (email, Google, etc.).
- Dashboard listing all created events.
- Create/Edit invitation:
  - Upload main invitation content (image, PDF, or HTML).
  - Set event details (title, date, location, description).
  - Customize cover (with countdown, event name, optional photo/logo).
- RSVP/Reservation module:
  - Built-in form for guests (name, attendance, custom questions).
  - View/manage guest list; export as CSV/Excel.
- Gift/Wishlist section:
  - Host adds e-wallet, address, or wishlist link.
- Sharing:
  - Generate unique invitation link.
  - Generate QR code (for sharing and event check-in).
  - WhatsApp “Click to Chat” sharing.
- Analytics:
  - RSVP status, guest check-in stats, trends.
- Payment:
  - Pay-per-event (QRIS via DOKU), or subscribe for premium features.
  - Only after payment is event “activated” for full sharing/analytics.
- Communication:
  - Send reminders/updates to guests via email/WhatsApp.
- Profile/Account management.

### 2.2. Guest Features
- View invitation (responsive/mobile-first).
- RSVP via web form.
- Add event to calendar (Google/iCal).
- View event details, gift info.
- Check-in via QR code at event.

### 2.3. Admin Features
- Login (role-based access).
- Platform analytics dashboard (users, events, payments, RSVPs, check-ins).
- User management (view, search, suspend/reactivate, impersonate).
- Event/invitation management (search, moderate, disable/remove).
- Content moderation (flagged content/events queue).
- Payment/revenue management (track payments, configure pricing/plans).
- System configuration (limits, notifications, legal docs).
- View audit logs of all admin actions.
- Support ticket/feedback management.

---

## 3. Non-Functional Requirements

- Secure user authentication (JWT/OAuth).
- Data privacy (GDPR-compliant).
- Payment security (PCI DSS, HTTPS).
- Scalable (cloud-ready, containerized).
- Responsive UI/UX.
- Automated backups and error monitoring.
- Accessible (WCAG 2.1 compliance).

---

## 4. Technical Stack Recommendation

### 4.1. Frontend
- React (with hooks/context)
- Redux or Context API for state management
- Axios (API calls), react-router
- UI kit: Material-UI, Ant Design, or custom
- qrcode.react (QR generation)
- Chart.js or Recharts (analytics)
- Formik/Yup (forms/validation)

### 4.2. Backend
- Node.js with Express.js
- MongoDB (Mongoose ODM)
- Multer (file uploads)
- JWT for authentication
- Nodemailer (email), Twilio/WhatsApp API (reminders)
- DOKU QRIS integration (payment)
- Stripe/PayPal (optional, for international)
- Webhook handlers (for payment notifications)
- Winston/Morgan (logging)

### 4.3. DevOps & Infrastructure
- Docker (containerization)
- Nginx/Apache (reverse proxy)
- CI/CD: GitHub Actions, Jenkins, or GitLab CI
- Cloud: AWS, GCP, or DigitalOcean (S3 for file storage, EC2/App Engine for server)
- SSL/TLS everywhere

---

## 5. API Specification (Sample)

| Endpoint                  | Method | Description                                   |
|---------------------------|--------|-----------------------------------------------|
| /api/auth/register        | POST   | Register new user                             |
| /api/auth/login           | POST   | Log in user                                   |
| /api/invitations          | POST   | Create new invitation                         |
| /api/invitations/:id      | GET    | Get invitation details                        |
| /api/invitations/:id      | PUT    | Edit invitation                               |
| /api/invitations/:id/pay  | POST   | Initiate payment (DOKU QRIS)                  |
| /api/invitations/:id/rsvp | POST   | Guest RSVP submission                         |
| /api/invitations/:id/checkin | POST | Guest check-in via QR                         |
| /api/users/:id            | GET    | Get user dashboard data                       |
| /api/admin/users          | GET    | Admin: list/search users                      |
| /api/admin/events         | GET    | Admin: list/moderate invitations              |
| /api/admin/payments       | GET    | Admin: payment overview                       |

---

## 6. User Flow

1. **User registers/logs in.**
2. **Creates a new invitation:** Uploads content, sets event details, customizes cover.
3. **User previews invitation.**
4. **To activate/share:** User pays via DOKU QR (shown in-app, user scans and pays).
5. **After payment, event is live:** User gets links/QR/WhatsApp to share.
6. **Guests RSVP, view details, check-in at event via QR scan.**
7. **Host monitors dashboard:** RSVPs, check-ins, analytics, manages reminders.
8. **Admin oversees platform activity, payments, and moderation.**

---

## 7. Payment Flow (DOKU QRIS Integration)

- User initiates payment for event activation.
- Backend calls DOKU QRIS API, gets QR string.
- QR code is displayed to user; user scans/pay via e-wallet/bank app.
- DOKU sends payment notification (webhook) to backend.
- Backend marks event as paid/active; unlocks sharing/analytics.

---

## 8. Monetization Strategy

- **Pay-per-event:** One-time fee per event (via DOKU QRIS).
- **Subscriptions:** Unlimited events/premium features for monthly/yearly fee.
- **Feature unlocks:** Advanced analytics, guest SMS, custom branding as add-ons.
- **Free tier:** Limited features/events; prompt upgrade for full access.

---

## 9. Security & Compliance

- All sensitive data encrypted at rest and in transit.
- Regular vulnerability scanning and dependency updates.
- Data access via RBAC (users vs. admins).
- Detailed audit logs (admin actions, payment events).

---

## 10. Project Management

- Agile methodology (scrum/kanban).
- Milestones: MVP → Beta → Launch → Growth.
- Documentation: API (Swagger/OpenAPI), user/admin manuals.
- Testing: Unit, integration, end-to-end, UAT.
- Rollback/backup strategy.

---

## 11. Deliverables

- Source code (frontend + backend)
- Deployment scripts/Dockerfiles
- API documentation
- User/admin guides
- Payment (DOKU) integration tested and certified
- Live demo (staging & production environments)

---

## 12. Future Enhancements

- Multi-language support
- White-labeling for partners
- Mobile app (React Native)
- AI-powered guest analytics
