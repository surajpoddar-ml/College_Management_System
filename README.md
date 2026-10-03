<div align="center">

# 🏫 Chautari

### Your Campus, Connected.

**A full-stack MERN campus community platform with AI-powered assistance, real-time messaging, canteen ordering with interactive table map, and role-based management for students, teachers, staff, and administrators.**

![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-5-000000?style=flat&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-4-010101?style=flat&logo=socket.io&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?style=flat&logo=tailwindcss&logoColor=white)

![License](https://img.shields.io/badge/License-ISC-blue)
![Node](https://img.shields.io/badge/Node-20+-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

</div>

---

## 📖 Project Overview

**Chautari** (Nepali: "चौतारी" — a resting place / community gathering spot) is a comprehensive MERN-stack web application designed to digitize and streamline daily campus operations for colleges in Nepal. It serves as a centralized hub connecting students, teachers, staff, and administrators through shared modules including attendance tracking, timetable management, campus canteen operations with an interactive table map, lost & found, event management, peer help systems, library & sports resource management, coursework submission, and real-time chat — all powered by an AI campus assistant (Chautari AI).

---

## 🎯 Project Objectives

- Digitize manual campus processes (attendance, timetables, canteen credits, announcements)
- Provide role-based dashboards for students, teachers, staff, and administrators
- Enable real-time communication between campus members via Socket.IO
- Introduce an AI-powered campus assistant (Chautari AI) that answers queries using live database context
- Offer a modern, responsive, and accessible UI built with Tailwind CSS 4
- Centralize campus resources: library books, sports equipment, classroom booking, and department contacts
- Support canteen food ordering with an interactive real canteen photo table map

---

## ✨ Features

| Module | Description |
|---|---|
| 🔐 **Auth & Roles** | Register/Login with JWT in httpOnly cookies; 4 roles: student, teacher, staff, admin; account approval system |
| 📊 **Student Dashboard** | Attendance, timetable, events, canteen, lost & found, campus help, SSD help, chat, resources, vacant classes, profile |
| 🛠️ **Admin Dashboard** | Manage attendance, events, announcements, canteen, lost & found, resources, campus help, timetable, SSD, users |
| 🏫 **Admin Department Panels** | Super, Canteen, SSD, RTE, and Resources department-specific admin sections with separate login per section |
| 🤖 **Chautari AI** | RAG-powered campus assistant using Groq LLM with live database context — attendance, timetable, events, canteen, lost & found, library, sports, classrooms |
| 💬 **Real-Time Chat** | 1-on-1 DMs and group conversations with Socket.IO, read receipts, file attachments, message deletion |
| 👥 **Friends System** | Send/accept/reject friend requests; DM chat requires accepted friendship |
| 📢 **Announcements** | Priority-based (Low/Medium/High/Urgent) campus announcements by department |
| 📅 **Events** | College & community events with registration, capacity limits, and status tracking |
| ✅ **Attendance** | Student attendance tracking (Present/Absent) with report request system |
| 📋 **Timetable** | Weekly timetable management with module, lecturer, room, and group linking; schedule changes |
| 🍽️ **Canteen** | Menu management (categories, NPR pricing, special/popular flags), interactive aerial photo table map for seat selection, student canteen order placement, and credit tracking |
| 🔍 **Lost & Found** | Post lost/found items with claims system, status tracking, text search, and CCTV request integration |
| 🏕️ **Campus Help** | Peer-to-peer help request system with threaded responses and attachments |
| 🆘 **SSD Help** | Student Support Division help system (CCTV requests, sports requests) |
| 📚 **Library** | Book catalog with borrow request workflow (pending → approved → returned) |
| 🏀 **Sports** | Sports equipment inventory with request/approval workflow |
| 🏫 **Classrooms** | Classroom management, room requests, and vacant room finder |
| 🎓 **Modules & Groups** | Academic module master list (code + name) and section groups for timetable assignment |
| 📝 **Coursework** | Teacher-created coursework with student submission, file upload via ImageKit |
| 📹 **CCTV Requests** | Students can request CCTV footage review for lost item incidents |
| 🔔 **Notifications** | Real-time notification system with 20+ notification types and read/unread tracking |
| 🤝 **Volunteering** | Volunteer opportunities, applications, and verified hour records |
| 🌐 **DevCorps Portal** | Separate community portal with membership, workshops, documentation, constitution management |
| 📱 **Responsive Design** | Mobile-first UI with Tailwind CSS 4; dark & light theme support |
| 🖼️ **Image Uploads** | ImageKit-powered image hosting with crop modal for profiles and covers |
| 🔔 **Push Notifications** | Web Push (VAPID) notifications for PWA-style alerts |

---

## 🤖 Chautari AI (RAG System)

Chautari AI is a Retrieval-Augmented Generation system providing each student a personalized campus assistant:

- **Live Data Context**: On every query, the system fetches the student's real attendance, timetable, canteen menu & credit balance, active events, announcements, volunteering records, lost & found items, classroom requests, CCTV requests, library borrows, and sports requests directly from MongoDB
- **LLM Backend**: Uses Groq SDK with `qwen/qwen3-8b` model (`allam-2-7b` as fallback on rate limits)
- **System Prompt**: Instructs the model to answer in plain, friendly language using only the provided real data — no hallucinations
- **Conversation History**: Maintains last 6 messages for context-aware multi-turn conversations
- **Accessible UI**: Floating AI chat widget available globally across all authenticated pages

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        CLIENT (Vite 8)                       │
│   React 19 + React Router 7 + Tailwind CSS 4 + Socket.IO   │
│   Contexts: Auth | Chat | Notification | AIChat | Theme     │
│   Pages: Login | Signup | Student | Teacher | Staff | Admin  │
│   + DevCorps Portal | Admin Department Sections             │
└──────────────────────────┬──────────────────────────────────┘
                           │  HTTP + WebSocket
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                     SERVER (Express 5)                        │
│   JWT Auth Middleware | Role Middleware | Error Handler      │
│   Socket.IO Server (authenticated via httpOnly cookie)      │
│   30 Route Modules | 22+ Controllers | 45 Mongoose Models   │
│   Utilities: Notification Emitter | Token Generator | CORS  │
└──────────────────────────┬──────────────────────────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────────┐
        │ MongoDB  │ │ ImageKit │ │ Groq LLM API │
        │ Atlas    │ │ (Images) │ │ (Chautari AI) │
        └──────────┘ └──────────┘ └──────────────┘
```

---

## 🛠️ Technology Stack

### Frontend

| Technology | Version | Purpose |
|---|---|---|
| React | 19 | UI library |
| React Router | 7 | Client-side routing |
| Tailwind CSS | 4 | Utility-first styling |
| Axios | 1.x | HTTP client |
| Socket.IO Client | 4.x | Real-time WebSocket communication |
| Lucide React | 1.x | Icon library |
| React Hot Toast | 2.x | Toast notifications |
| React Easy Crop | 6.x | Image cropping for profile/cover uploads |
| pdfjs-dist | 6.x | PDF viewer for coursework submissions |
| Vite | 8 | Build tool and dev server |

### Backend

| Technology | Version | Purpose |
|---|---|---|
| Node.js | 20+ | Runtime |
| Express | 5 | Web framework |
| Mongoose | 9 | MongoDB ODM |
| Socket.IO | 4 | Real-time server |
| jsonwebtoken | 9 | Authentication (httpOnly cookies) |
| bcryptjs | 3 | Password hashing |
| Multer | 2 | File upload handling |
| ImageKit | 6 | Cloud image hosting |
| Groq SDK | 1.x | AI/LLM integration |
| pdfkit | 0.x | Server-side PDF generation |
| web-push | 3.x | Web Push / VAPID notifications |
| dotenv | 17 | Environment variable management |
| cookie-parser | 1.x | Cookie parsing middleware |

### Infrastructure & Services

| Service | Purpose |
|---|---|
| MongoDB Atlas | Cloud database |
| ImageKit | Image CDN and transformations |
| Groq Cloud | LLM inference (Qwen 3.8B, Allam 2 7B) |
| Web Push (VAPID) | PWA push notifications |
| Google DNS (8.8.8.8) | SRV record resolution fix for MongoDB Atlas |

---

## 📂 Project Structure

```
MERN-SEP-PROJECT/
├── client/                          # Frontend (Vite 8 + React 19)
│   ├── public/
│   │   ├── favicon.png              # Chautari logo favicon (32×32)
│   │   ├── apple-touch-icon.png     # iOS home-screen icon (180×180)
│   │   ├── icon-192.png             # PWA icon (192×192)
│   │   ├── canteen/
│   │   │   └── canteen-map.jpg      # Real aerial canteen photo (table map)
│   │   └── ...other static assets
│   ├── src/
│   │   ├── api/                     # Axios API service modules (24 files)
│   │   │   ├── axiosInstance.js     # Configured Axios with credentials
│   │   │   ├── auth.js
│   │   │   ├── aiChatApi.js
│   │   │   ├── announcementApi.js
│   │   │   ├── attendanceApi.js
│   │   │   ├── campusHelpApi.js
│   │   │   ├── canteenApi.js
│   │   │   ├── chatApi.js
│   │   │   ├── classroomApi.js
│   │   │   ├── classroomRequestApi.js
│   │   │   ├── eventsApi.js
│   │   │   ├── friendApi.js
│   │   │   ├── groupApi.js
│   │   │   ├── lostFoundApi.js
│   │   │   ├── moduleApi.js
│   │   │   ├── notificationApi.js
│   │   │   ├── resourcesApi.js
│   │   │   ├── ssdHelpApi.js
│   │   │   ├── timetableApi.js
│   │   │   ├── uploadApi.js
│   │   │   ├── userApi.js
│   │   │   ├── vacantClassesApi.js
│   │   │   ├── volunteerApi.js
│   │   │   └── volunteerOpportunityApi.js
│   │   ├── auth/
│   │   │   ├── ProtectedRoute.jsx   # Redirects unauthenticated users
│   │   │   ├── RoleRoute.jsx        # Role-based access guard
│   │   │   └── DevCorpsRoute.jsx    # DevCorps portal access guard
│   │   ├── components/
│   │   │   ├── admin/               # Admin panel components (11 modules)
│   │   │   │   ├── Dashboard/
│   │   │   │   ├── ManageAnnouncements/
│   │   │   │   ├── ManageAttendance/
│   │   │   │   ├── ManageCampusHelp/
│   │   │   │   ├── ManageCanteen/
│   │   │   │   ├── ManageEvents/
│   │   │   │   ├── ManageLostFound/
│   │   │   │   ├── ManageResources/
│   │   │   │   ├── ManageSSD/
│   │   │   │   ├── ManageTimetable/
│   │   │   │   └── ManageUsers/
│   │   │   ├── common/              # Shared components
│   │   │   │   ├── AIChatWidget.jsx       # Floating AI assistant chat
│   │   │   │   ├── ChatButton.jsx
│   │   │   │   ├── ChatPanel.jsx
│   │   │   │   ├── ConfirmDeleteModal.jsx
│   │   │   │   ├── ImageCropModal.jsx
│   │   │   │   ├── ImageUploadField.jsx
│   │   │   │   ├── NotificationBell.jsx
│   │   │   │   └── Sidebar.jsx
│   │   │   └── student/             # Student dashboard sections
│   │   │       ├── canteen/
│   │   │       │   ├── CanteenCartDrawer.jsx
│   │   │       │   ├── CanteenCheckoutModal.jsx  # 3-step checkout (table→payment→confirm)
│   │   │       │   ├── CanteenTableMap.jsx       # Interactive aerial photo table selector
│   │   │       │   └── MyOrdersPanel.jsx
│   │   │       ├── Dashboard/
│   │   │       ├── LostFound/
│   │   │       ├── modals/
│   │   │       ├── coursework/
│   │   │       ├── CampusHelpSection.jsx
│   │   │       ├── CanteenSection.jsx
│   │   │       ├── ChatSection.jsx
│   │   │       ├── EventsSection.jsx
│   │   │       ├── LostFoundSection.jsx
│   │   │       ├── ProfileSection.jsx
│   │   │       ├── ResourcesSection.jsx
│   │   │       ├── SSDHelpSection.jsx
│   │   │       ├── TimetableSection.jsx
│   │   │       └── VacantClassesSection.jsx
│   │   ├── context/
│   │   │   ├── AuthContext.jsx        # User auth state, login/logout
│   │   │   ├── ChatContext.jsx        # Real-time chat state
│   │   │   ├── NotificationContext.jsx # Notification state
│   │   │   ├── AIChatContext.jsx      # AI chat history
│   │   │   └── ThemeContext.jsx       # Dark/light theme
│   │   ├── hooks/
│   │   │   └── usePushNotifications.js # Web Push subscription hook
│   │   ├── pages/
│   │   │   ├── Login.jsx
│   │   │   ├── Signup.jsx
│   │   │   ├── StudentDashBoard.jsx
│   │   │   ├── TeacherDashboard.jsx
│   │   │   ├── StaffDashboard.jsx
│   │   │   ├── AdminDashboard.jsx
│   │   │   ├── AdminDepartmentPicker.jsx  # Dept card selector (/admin/dept)
│   │   │   ├── AdminDeptSection.jsx       # Per-dept panel with own login
│   │   │   └── DevCorpsDashboard.jsx
│   │   ├── socket/
│   │   │   └── socket.js              # Socket.IO client singleton
│   │   ├── App.jsx                    # Root routing (React Router 7)
│   │   ├── main.jsx                   # React entry point
│   │   └── index.css                  # Global styles
│   ├── index.html                     # Chautari favicon + meta
│   ├── vite.config.js
│   └── package.json
│
├── server/                            # Backend (Express 5 + Mongoose 9)
│   ├── config/
│   │   ├── db.js                      # MongoDB Atlas connection + health check
│   │   └── imagekit.js                # ImageKit SDK configuration
│   ├── controllers/                   # Business logic (22+ files)
│   │   ├── authController.js
│   │   ├── adminUserController.js
│   │   ├── aiChatController.js        # RAG pipeline + Groq LLM
│   │   ├── announcementController.js
│   │   ├── attendanceController.js
│   │   ├── canteenController.js       # Menu, orders, credits
│   │   ├── chatController.js
│   │   ├── classroomController.js
│   │   ├── classroomRequestController.js
│   │   ├── eventController.js
│   │   ├── friendController.js
│   │   ├── groupController.js
│   │   ├── helpController.js
│   │   ├── lostFoundController.js
│   │   ├── moduleController.js
│   │   ├── notificationController.js
│   │   ├── resourceController.js
│   │   ├── timetableController.js
│   │   ├── uploadController.js
│   │   ├── userController.js
│   │   ├── volunteerController.js
│   │   └── volunteerOpportunityController.js
│   ├── middleware/
│   │   ├── authMiddleware.js          # JWT verification + user injection
│   │   ├── errorHandler.js            # Global 404 + error handler
│   │   ├── optionalAuthMiddleware.js  # Auth when token present, optional otherwise
│   │   ├── roleMiddleware.js          # Role-based access control
│   │   └── upload.js                  # Multer file upload config
│   ├── models/                        # Mongoose schemas (45 models)
│   │   ├── User.js
│   │   ├── Announcement.js
│   │   ├── Attendance.js
│   │   ├── AttendanceReportRequest.js
│   │   ├── Book.js
│   │   ├── BorrowRequest.js
│   │   ├── CanteenCredit.js
│   │   ├── CanteenCreditRequest.js
│   │   ├── CanteenMenu.js
│   │   ├── CanteenOrder.js
│   │   ├── CctvRequest.js
│   │   ├── Classroom.js
│   │   ├── ClassroomRequest.js
│   │   ├── CommunityConstitution.js
│   │   ├── CommunityDocumentation.js
│   │   ├── CommunityFile.js
│   │   ├── CommunityMembership.js
│   │   ├── CommunityProfile.js
│   │   ├── CommunityWorkshop.js
│   │   ├── Conversation.js
│   │   ├── Coursework.js
│   │   ├── CourseworkSubmission.js
│   │   ├── DepartmentContact.js
│   │   ├── Event.js
│   │   ├── EventRegistration.js
│   │   ├── EventRequest.js
│   │   ├── Exam.js
│   │   ├── FriendRequest.js
│   │   ├── Group.js
│   │   ├── GroupInvite.js
│   │   ├── HelpRequest.js
│   │   ├── LostFoundItem.js
│   │   ├── Message.js
│   │   ├── Module.js
│   │   ├── Notification.js
│   │   ├── PushSubscription.js
│   │   ├── ScheduleChange.js
│   │   ├── SemesterConfig.js
│   │   ├── SportsItem.js
│   │   ├── SportsRequest.js
│   │   ├── Timetable.js
│   │   ├── VacantClassroom.js
│   │   ├── VolunteerApplication.js
│   │   ├── VolunteerOpportunity.js
│   │   └── VolunteerRecord.js
│   ├── routes/                        # Express route definitions (30 files)
│   │   ├── auth.routes.js
│   │   ├── adminUsers.routes.js
│   │   ├── aiChat.routes.js
│   │   ├── announcement.routes.js
│   │   ├── attendance.routes.js
│   │   ├── canteen.routes.js
│   │   ├── chat.routes.js
│   │   ├── classrooms.routes.js
│   │   ├── classroomRequests.routes.js
│   │   ├── communityPortal.routes.js
│   │   ├── coursework.routes.js
│   │   ├── devcorps.routes.js
│   │   ├── event.routes.js
│   │   ├── exam.routes.js
│   │   ├── friend.routes.js
│   │   ├── groups.routes.js
│   │   ├── help.routes.js
│   │   ├── lostFound.routes.js
│   │   ├── modules.routes.js
│   │   ├── notification.routes.js
│   │   ├── push.routes.js
│   │   ├── resource.routes.js
│   │   ├── timetable.routes.js
│   │   ├── upload.routes.js
│   │   ├── user.routes.js
│   │   ├── volunteerOpportunity.routes.js
│   │   └── volunteerRecords.routes.js
│   ├── scripts/
│   │   ├── createAdminAccount.js      # CLI script to create admin users
│   │   └── backfillCanteenCredits.js  # Backfill CanteenCredit for existing users
│   ├── socket/
│   │   └── socketHandler.js           # Socket.IO server with JWT cookie auth
│   ├── utils/
│   │   ├── corsOrigin.js              # Dynamic CORS origin check
│   │   ├── createNotification.js      # Notification helper + real-time push
│   │   └── generateToken.js           # JWT token generation + cookie setting
│   ├── .env
│   ├── package.json
│   └── server.js                      # Express app entry, middleware, routes, port 3000
│
├── .gitignore
└── README.md
```

---

## ⚙️ Installation & Setup

### Prerequisites

- **Node.js** v20+ and npm
- **MongoDB Atlas** account (or local MongoDB)
- **ImageKit** account — [imagekit.io](https://imagekit.io)
- **Groq** API key (free) — [console.groq.com](https://console.groq.com)

### 1. Clone the Repository

```bash
git clone https://github.com/frankuard/MERN-SEP-PROJECT.git
cd MERN-SEP-PROJECT
```

### 2. Backend Setup

```bash
cd server
npm install
```

Create `server/.env`:

```env
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/chautari
JWT_SECRET=your_jwt_secret_here
JWT_EXPIRES_IN=7d

IMAGEKIT_PUBLIC_KEY=your_imagekit_public_key
IMAGEKIT_PRIVATE_KEY=your_imagekit_private_key
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/your_endpoint

GROQ_API_KEY=your_groq_api_key

VAPID_PUBLIC_KEY=your_vapid_public_key
VAPID_PRIVATE_KEY=your_vapid_private_key
VAPID_EMAIL=mailto:admin@yourdomain.com
```

Start the backend:

```bash
npm run dev       # development (nodemon)
npm start         # production
```

> Server runs on **port 3000**.

### 3. Frontend Setup

```bash
cd client
npm install
npm run dev
```

> Client runs on **port 5173** (Vite default) or as configured in `vite.config.js`.

### 4. Create Admin Account

```bash
cd server
node scripts/createAdminAccount.js
```

Follow the CLI prompts to create the initial admin user.

### 5. Environment Variables Reference

| Variable | Location | Description |
|---|---|---|
| `MONGO_URI` | server | MongoDB Atlas connection string |
| `JWT_SECRET` | server | Secret key for JWT signing |
| `JWT_EXPIRES_IN` | server | Token expiry (default: `7d`) |
| `IMAGEKIT_PUBLIC_KEY` | server | ImageKit public API key |
| `IMAGEKIT_PRIVATE_KEY` | server | ImageKit private API key |
| `IMAGEKIT_URL_ENDPOINT` | server | ImageKit CDN URL |
| `GROQ_API_KEY` | server | Groq LLM API key for Chautari AI |
| `VAPID_PUBLIC_KEY` | server | Web Push VAPID public key |
| `VAPID_PRIVATE_KEY` | server | Web Push VAPID private key |
| `VAPID_EMAIL` | server | Contact email for push notifications |
| `VITE_API_URL` | client | (Optional) Override API base URL |
| `VITE_SOCKET_URL` | client | (Optional) Override Socket.IO URL |

---

## 🔐 Authentication & Security

- **JWT in httpOnly Cookies**: Tokens stored in `httpOnly`, `secure`, `SameSite` cookies — never accessible via JavaScript
- **Password Hashing**: bcryptjs with salt rounds
- **Role-Based Access Control**: `authMiddleware` + `roleMiddleware` on every protected route
- **Account Approval System**: Teachers and staff require admin approval (`status: pending`) before accessing the platform; students are auto-approved
- **Rejected Account Handling**: Rejected accounts are blocked from login with a clear error message
- **Socket.IO Authentication**: WebSocket connections authenticated by parsing the raw `Cookie` header and verifying the JWT — no unauthenticated socket connections allowed
- **CORS**: Dynamic origin checking against configured client URL
- **Session Duration**: 7-day token expiry; auto-restored on page load via `GET /api/auth/me`

---

## 💬 Real-Time Communication

### Socket.IO Events

| Direction | Event | Description |
|---|---|---|
| Client → Server | `conversation:join` | Join a conversation room |
| Client → Server | `conversation:leave` | Leave a conversation room |
| Server → Client | `message:new` | New message in a joined conversation |
| Server → Client | `conversation:bump` | Conversation list update (unread badge) |
| Server → Client | `conversation:updated` | Group membership or info changed |
| Server → Client | `conversation:new` | New conversation appeared (group invite accepted) |
| Server → Client | `conversation:deleted` | Group deleted by creator |
| Server → Client | `messages:deleted` | Messages removed by sender |
| Server → Client | `notification:new` | Real-time notification pushed to user's room |
| Server → Client | `friend:request` | Incoming friend request |
| Server → Client | `group:invite` | Incoming group invite |
| Server → Client | `canteen:menu:updated` | Admin created/updated/deleted a menu item |
| Server → Client | `canteen:credit:updated` | Admin adjusted a student's canteen credit |

### Chat Features

- 1-on-1 direct messaging (requires accepted friendship)
- Group conversations with invite system
- Message read receipts (`readBy` array)
- File/image attachments via ImageKit upload
- Message deletion (own messages only)
- Conversation deletion (DM: hide-for-me; Group: creator deletes for all)
- Paginated message loading

---

## 👥 User Roles & Permissions

| Role | Status on Register | Route | Key Access |
|---|---|---|---|
| **Student** | Auto-approved | `/student/:tab` | All student modules: attendance, timetable, canteen, chat, events, lost & found, campus help, SSD help, resources, profile |
| **Teacher** | Pending admin approval | `/teacher/:tab` | Timetable view, coursework management, attendance view |
| **Staff** | Pending admin approval | `/staff/dashboard` | Staff-specific dashboard |
| **Admin** | Created via CLI script | `/admin/:tab` | Full platform management |
| **DevCorps** | Special account | `/devcorps/:tab` | Community portal management |

### Admin Department Sections (`/admin/dept/:section`)

| Section | Scope |
|---|---|
| `super` | Main admin dashboard — all management tabs |
| `canteen` | Canteen menu, orders, credits |
| `ssd` | Student Support Division — CCTV requests, sports, help |
| `rte` | Registry & Timetabling — timetable, modules, classrooms, schedule changes |
| `resources` | Library books, borrow requests, department contacts |

---

## 🗄️ Database Structure

### Core Models (45 total)

| Model | Key Fields | Purpose |
|---|---|---|
| **User** | username, email, password, role, status, department, semester, adminSection, profileImage, coverPhoto, bio | All platform users |
| **Attendance** | student, date, time, room, status (Present/Absent), markedBy | Daily attendance records |
| **AttendanceReportRequest** | student, reason, status (pending/fulfilled/rejected), adminNote | Attendance correction requests |
| **Timetable** | day, startTime, endTime, classType, module, moduleName, moduleCode, lecturer, group, room, roomName | Weekly class schedule |
| **ScheduleChange** | period, originalDay/Time/Room, newDay/Time/Room, reason, effectiveDate | Timetable modification notices |
| **Module** | code, name | Academic module master list |
| **Group** | name | Section groups |
| **Classroom** | name, capacity, facilities, manualBlocks | Room inventory |
| **ClassroomRequest** | classroom, requestedBy, day, startTime, endTime, reason, status | Room booking requests |
| **VacantClassroom** | roomName, block, day, capacity, availableFrom, availableTo | Available room finder |
| **SemesterConfig** | semester, startDate, endDate | Semester configuration |

### Communication Models

| Model | Key Fields | Purpose |
|---|---|---|
| **Conversation** | isGroup, groupName, participants, lastMessage, deletedBy | Chat containers |
| **Message** | conversation, sender, text, readBy, attachment | Chat messages |
| **FriendRequest** | requester, recipient, status | Friendship system |
| **GroupInvite** | conversation, invitedUser, invitedBy, status | Group membership invites |
| **Notification** | recipient, type, title, message, link, read, meta | 20+ notification types |
| **PushSubscription** | user, endpoint, keys | Web Push subscriptions |

### Campus Operations Models

| Model | Key Fields | Purpose |
|---|---|---|
| **Announcement** | title, message, priority (Low/Medium/High/Urgent), department | Campus announcements |
| **Event** | title, description, type (college/community), category, date, venue, capacity, status | Campus events |
| **EventRegistration** | event, user, status | Event sign-ups |
| **EventRequest** | title, requestedBy, description, status | Event submission requests |
| **CanteenMenu** | name, price, category, image, availability, isSpecialOfTheDay, isPopular | Food menu items |
| **CanteenOrder** | items, tableNumber, paymentMethod, status, student | Canteen food orders |
| **CanteenCredit** | user, amountDue, amountPaid, remainingBalance, paymentStatus, paymentHistory, dueHistory | Student credit tracking |
| **CanteenCreditRequest** | user, amount, reason, status | Credit adjustment requests |
| **LostFoundItem** | title, type (lost/found), category, location, status, claims | Lost & found posts |
| **HelpRequest** | requester, request, attachments, responses | Peer help requests |
| **CctvRequest** | user, location, date, timeFrom, timeTo, reason, status | CCTV footage requests |
| **Book** | name, author, shelf, category, cover | Library catalog |
| **BorrowRequest** | book, requestedBy, studentIdNumber, returnBy, status | Borrow workflow |
| **SportsItem** | name, icon, totalQuantity | Sports equipment inventory |
| **SportsRequest** | item, requestedBy, quantity, slot, status | Equipment requests |
| **DepartmentContact** | key, title, phone, email, icon | Contact directory |
| **Coursework** | title, description, dueDate, createdBy, attachments | Teacher-created assignments |
| **CourseworkSubmission** | coursework, student, fileUrl, submittedAt, grade | Student submissions |
| **Exam** | title, date, module, venue, group | Exam schedule |
| **VolunteerOpportunity** | event, role, date, slotsAvailable, isOpen | Volunteer openings |
| **VolunteerApplication** | opportunity, student, status | Volunteer applications |
| **VolunteerRecord** | student, event, role, hours, verifiedBy | Verified volunteer hours |

### Community/DevCorps Models

| Model | Purpose |
|---|---|
| **CommunityProfile** | DevCorps organization profile |
| **CommunityMembership** | Member management |
| **CommunityWorkshop** | Workshop events |
| **CommunityDocumentation** | Technical documentation |
| **CommunityConstitution** | Organization rules/constitution |
| **CommunityFile** | Uploaded community files |

---

## 🔌 API Reference

All endpoints are prefixed with `/api`.

### Authentication
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/auth/register` | None | Register (student auto-approved; teacher/staff pending) |
| POST | `/auth/login` | None | Login → sets httpOnly JWT cookie |
| POST | `/auth/logout` | None | Clear cookie |
| GET | `/auth/me` | Cookie | Get current user (session restore) |

### Canteen
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/canteen/menu` | Any | Get menu (filter by category/search) |
| POST | `/canteen/menu` | Admin | Add menu item |
| PATCH | `/canteen/menu/:id` | Admin | Update menu item |
| DELETE | `/canteen/menu/:id` | Admin | Delete menu item |
| POST | `/canteen/orders` | Student | Place canteen order (items, tableNumber, paymentMethod) |
| GET | `/canteen/orders/my` | Student | Get own orders |
| GET | `/canteen/orders` | Admin | Get all orders |
| GET | `/canteen/credits/my` | Student | Get own credit balance |
| GET | `/canteen/credits` | Admin | Get all credit records |
| PATCH | `/canteen/credits/:id` | Admin | Adjust student credit |

### Attendance
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/attendance` | Student | Get own attendance |
| POST | `/attendance` | Admin | Mark attendance |
| GET | `/attendance/report-requests` | Student | Own report requests |
| POST | `/attendance/report-requests` | Student | Submit report request |
| PATCH | `/attendance/report-requests/:id` | Admin | Fulfill/reject request |

### Timetable & Academics
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/timetable` | Any | Get weekly timetable |
| POST | `/timetable` | Admin | Create timetable entry |
| PATCH | `/timetable/:id` | Admin | Update entry |
| DELETE | `/timetable/:id` | Admin | Delete entry |
| GET | `/modules` | Any | List all modules |
| POST | `/modules` | Admin | Create module |
| GET | `/groups` | Any | List all groups |
| POST | `/groups` | Admin | Create group |
| GET | `/classrooms` | Any | List classrooms |
| GET | `/classrooms/vacant` | Any | Find vacant classrooms |
| GET | `/classroom-requests` | Any | Get classroom requests |
| POST | `/classroom-requests` | Student | Submit room request |

### Events & Announcements
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/events` | Any | List events |
| POST | `/events` | Admin | Create event |
| POST | `/events/:id/register` | Student | Register for event |
| GET | `/announcements` | Any | List announcements |
| POST | `/announcements` | Admin | Create announcement |
| DELETE | `/announcements/:id` | Admin | Delete announcement |

### Lost & Found
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/lost-found` | Any | List items (search/filter) |
| POST | `/lost-found` | Auth | Post lost/found item |
| POST | `/lost-found/:id/claim` | Student | Claim an item |
| PATCH | `/lost-found/:id` | Admin | Update item status |

### Campus Help & SSD
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/campus-help` | Auth | List help requests |
| POST | `/campus-help` | Student | Submit help request |
| POST | `/campus-help/:id/respond` | Auth | Respond to request |

### Resources (Library & Sports)
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/resources/books` | Any | List library books |
| POST | `/resources/books` | Admin | Add book |
| POST | `/resources/borrow` | Student | Request book borrow |
| PATCH | `/resources/borrow/:id` | Admin | Approve/reject/mark returned |
| GET | `/resources/sports` | Any | List sports items |
| POST | `/resources/sports/request` | Student | Request equipment |
| PATCH | `/resources/sports/request/:id` | Admin | Approve/reject request |

### Chat
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/chat/users/search?q=` | Auth | Search users |
| GET | `/chat/conversations` | Auth | List conversations |
| POST | `/chat/conversations/dm` | Auth | Start DM (requires friendship) |
| POST | `/chat/conversations/group` | Auth | Create group |
| GET | `/chat/conversations/:id/messages` | Auth | Get messages (paginated) |
| POST | `/chat/conversations/:id/messages` | Auth | Send message |
| PATCH | `/chat/conversations/:id/read` | Auth | Mark as read |
| DELETE | `/chat/conversations/:id` | Auth | Delete/hide conversation |

### Friends
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/friends` | Auth | Friends & pending requests |
| POST | `/friends/request` | Auth | Send friend request |
| PATCH | `/friends/:id/accept` | Auth | Accept request |
| PATCH | `/friends/:id/reject` | Auth | Reject request |

### Notifications
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/notifications` | Auth | List notifications |
| PATCH | `/notifications/:id/read` | Auth | Mark one read |
| PATCH | `/notifications/read-all` | Auth | Mark all read |

### Admin Users
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/admin/users` | Admin | List all users |
| PATCH | `/admin/users/:id` | Admin | Update user (role, status, etc.) |
| DELETE | `/admin/users/:id` | Admin | Delete user |

### AI
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/ai/chat` | Auth | Chat with Chautari AI (RAG-powered) |

### Coursework
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/coursework` | Auth | List coursework |
| POST | `/coursework` | Teacher | Create assignment |
| POST | `/coursework/:id/submit` | Student | Submit assignment |
| PATCH | `/coursework/submissions/:id/grade` | Teacher | Grade submission |

### Volunteer
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/volunteer-opportunities` | Any | List opportunities |
| POST | `/volunteer-opportunities` | Admin | Create opportunity |
| POST | `/volunteer-opportunities/:id/apply` | Student | Apply |
| GET | `/volunteer-records` | Auth | Volunteer records |
| POST | `/volunteer-records` | Admin | Create verified record |

### Upload
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/upload/image` | Auth | Upload image → ImageKit |
| POST | `/upload/document` | Auth | Upload document → ImageKit |

---

## 🍽️ Canteen — Interactive Table Map

The canteen ordering flow uses a **real aerial photo of the canteen** as an interactive SVG table map:

1. Student adds food items to cart from the menu grid
2. On checkout (Step 1), the canteen aerial photo is displayed with transparent SVG click areas positioned over each physical table
3. Clicking any table (1–9) selects it — a green ring appears around the selected table; the number label stays fixed-size
4. Step 2: payment method (Credit Due / Pay at Counter)
5. Step 3: order confirmation with table number, items, total
6. Order is placed via `POST /api/canteen/orders` with `{ items, tableNumber, paymentMethod }`
7. Real-time socket event `canteen:menu:updated` keeps the menu in sync across all connected students

**Table map technical details:**
- Component: `CanteenTableMap.jsx` — SVG overlay on `canteen-map.jpg`
- 9 percentage-based hit areas mapped to actual tables in the image
- Fully responsive via padding-bottom aspect-ratio trick
- Keyboard accessible (Enter/Space to select)
- Zero background on number labels — transparent SVG text with drop-shadow only

---

## 📱 Responsive Design

Mobile-first with Tailwind CSS 4, tested across:

- 📱 **Mobile** — Collapsible sidebar, scrollable tab pills, full-screen chat overlay
- 💻 **Tablet** — Adapted grid layouts
- 🖥️ **Desktop** — Full sidebar, expanded panels, multi-column grids

Theme support: **Dark** and **Light** mode throughout (controlled via `ThemeContext`).

---

## 🧪 Testing Status

> Automated test suites are not yet implemented. `npm test` is a placeholder in both packages.

Manual testing performed across all modules:

| Area | Status |
|---|---|
| Authentication (register, login, logout, session restore) | ✅ Tested |
| Role-based routing and access control | ✅ Tested |
| Admin CRUD (attendance, events, announcements, canteen, resources) | ✅ Tested |
| Student dashboard — all sections | ✅ Tested |
| Canteen ordering with interactive table map | ✅ Tested |
| Real-time chat (DMs, groups, Socket.IO) | ✅ Tested |
| Friend and group invite system | ✅ Tested |
| Notification system (in-app + real-time) | ✅ Tested |
| Chautari AI responses (RAG pipeline) | ✅ Tested |
| Image upload and cropping | ✅ Tested |
| Coursework creation and submission | ✅ Tested |
| Responsive design (mobile/tablet/desktop) | ✅ Tested |

---

## 🌐 Deployment

> Update with actual URLs once deployed.

| Service | URL |
|---|---|
| Frontend | Local — `http://localhost:5173` |
| Backend | Local — `http://localhost:3000` |
| Database | MongoDB Atlas |
| Images | ImageKit CDN |

---

## 🧭 Future Improvements

- [ ] Automated unit and integration tests (Jest + React Testing Library)
- [ ] Email notification system for important updates
- [ ] Google OAuth 2.0 login (client ID configured but not yet wired)
- [ ] WebSocket reconnection handling and offline message queue
- [ ] Advanced timetable conflict detection
- [ ] Multi-language support (English + Nepali)
- [ ] Admin analytics dashboard with usage statistics
- [ ] Rate limiting and brute-force protection
- [ ] API documentation with Swagger/OpenAPI
- [ ] Two-factor authentication (2FA)

---

## 🤝 Contributors

| Name | Role |
|---|---|
| **Diya Khadka** | UI/UX Designer |
| **Rojika Thapa** | UI/UX Designer |
| **Aayush Pradhan** | Frontend Developer |
| **Kailash Prasad Shah** | Frontend Developer |
| **Roshan Karki** | Backend Developer |
| **Suraj Poddar** | Backend Developer |

### Branches
- `main` — Main project branch
- `frontend` — Frontend development branch
- `suraj` — Suraj's development branch

---

## 📜 License

ISC License

---

## 🙏 Acknowledgements

- [MongoDB Atlas](https://www.mongodb.com/atlas) — Cloud database
- [ImageKit](https://imagekit.io) — Image CDN
- [Groq](https://groq.com) — Fast LLM inference for Chautari AI
- [Lucide Icons](https://lucide.dev) — Icons
- [Tailwind CSS](https://tailwindcss.com) — Styling
- [Socket.IO](https://socket.io) — Real-time communication
- [Express.js](https://expressjs.com) — Web framework
- [Mongoose](https://mongoosejs.com) — MongoDB ODM
- [React](https://react.dev) — UI library
- [Vite](https://vitejs.dev) — Build tool

---

<div align="center">

*Chautari — Where your campus comes together.*

</div>
