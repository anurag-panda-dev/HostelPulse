# HostelPulse — React Native (Expo) App Development Prompt

> **Use this prompt with any AI coding assistant (Claude, Cursor, ChatGPT, Copilot, etc.) to scaffold and build the HostelPulse mobile app.**

---

## 🧭 Project Overview

Build **HostelPulse** — a production-grade React Native mobile application using **Expo (SDK 51+)** for smart hostel management. The app serves **four distinct user roles**: Student, Warden (Admin), Staff, and Guard. Each role has its own navigation stack, screens, and permissions.

The app must be fully functional, visually polished, and production-ready with real API integration capability. Use **TypeScript** throughout.

---

## 🛠️ Tech Stack & Dependencies

```bash
# Initialize project
npx create-expo-app HostelPulse --template expo-template-blank-typescript

# Core navigation
npx expo install @react-navigation/native @react-navigation/native-stack @react-navigation/bottom-tabs
npx expo install react-native-screens react-native-safe-area-context

# UI & Styling
npx expo install react-native-paper
npx expo install @expo/vector-icons

# QR Code
npx expo install expo-camera
npx expo install expo-barcode-scanner
npx expo install react-native-qrcode-svg

# Location & Device
npx expo install expo-location
npx expo install expo-device
npx expo install expo-bluetooth  # For BLE proximity (optional)

# Notifications
npx expo install expo-notifications
npx expo install expo-constants

# Secure Storage & Auth
npx expo install expo-secure-store
npx expo install expo-crypto

# File & Image
npx expo install expo-image-picker
npx expo install expo-document-picker
npx expo install expo-file-system

# Payments (WebView-based Razorpay/Stripe)
npx expo install react-native-webview

# Networking & State
npm install axios
npm install zustand
npm install @tanstack/react-query

# Forms
npm install react-hook-form zod @hookform/resolvers

# Utilities
npm install date-fns
npm install react-native-toast-message
```

---

## 📁 Project Structure

```
HostelPulse/
├── app/                          # Expo Router (file-based routing) OR
├── src/
│   ├── api/                      # API clients and service functions
│   │   ├── client.ts             # Axios instance with interceptors
│   │   ├── auth.api.ts
│   │   ├── attendance.api.ts
│   │   ├── leave.api.ts
│   │   ├── grievance.api.ts
│   │   ├── payment.api.ts
│   │   └── messaging.api.ts
│   │
│   ├── components/               # Shared reusable components
│   │   ├── common/
│   │   │   ├── AppButton.tsx
│   │   │   ├── AppInput.tsx
│   │   │   ├── AppCard.tsx
│   │   │   ├── StatusBadge.tsx
│   │   │   ├── LoadingOverlay.tsx
│   │   │   ├── EmptyState.tsx
│   │   │   └── Avatar.tsx
│   │   ├── attendance/
│   │   │   ├── QRScanner.tsx
│   │   │   ├── QRDisplay.tsx
│   │   │   └── AttendanceCard.tsx
│   │   ├── leave/
│   │   │   ├── LeaveCard.tsx
│   │   │   └── LeaveStatusChip.tsx
│   │   ├── grievance/
│   │   │   ├── TicketCard.tsx
│   │   │   └── PriorityBadge.tsx
│   │   └── payment/
│   │       ├── PaymentCard.tsx
│   │       └── ReceiptModal.tsx
│   │
│   ├── navigation/
│   │   ├── RootNavigator.tsx     # Auth guard + role-based routing
│   │   ├── StudentNavigator.tsx
│   │   ├── WardenNavigator.tsx
│   │   ├── StaffNavigator.tsx
│   │   └── GuardNavigator.tsx
│   │
│   ├── screens/
│   │   ├── auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   └── ForgotPasswordScreen.tsx
│   │   ├── student/
│   │   │   ├── DashboardScreen.tsx
│   │   │   ├── ProfileScreen.tsx
│   │   │   ├── PaymentScreen.tsx
│   │   │   ├── PaymentHistoryScreen.tsx
│   │   │   ├── LeaveRequestScreen.tsx
│   │   │   ├── LeaveHistoryScreen.tsx
│   │   │   ├── GrievanceScreen.tsx
│   │   │   ├── GrievanceDetailScreen.tsx
│   │   │   ├── NewGrievanceScreen.tsx
│   │   │   ├── MessagingScreen.tsx
│   │   │   ├── RoomChangeScreen.tsx
│   │   │   └── QRAttendanceScreen.tsx
│   │   ├── warden/
│   │   │   ├── WardenDashboardScreen.tsx
│   │   │   ├── StudentListScreen.tsx
│   │   │   ├── StudentDetailScreen.tsx
│   │   │   ├── LeaveApprovalsScreen.tsx
│   │   │   ├── GrievanceManagementScreen.tsx
│   │   │   ├── PaymentVerificationScreen.tsx
│   │   │   ├── RoomAllocationScreen.tsx
│   │   │   └── BroadcastScreen.tsx
│   │   ├── staff/
│   │   │   ├── StaffDashboardScreen.tsx
│   │   │   ├── TaskDetailScreen.tsx
│   │   │   └── CompletionProofScreen.tsx
│   │   └── guard/
│   │       ├── GuardDashboardScreen.tsx
│   │       ├── AttendanceSessionScreen.tsx
│   │       ├── QRGeneratorScreen.tsx
│   │       ├── LeaveValidationScreen.tsx
│   │       └── MissingStudentsScreen.tsx
│   │
│   ├── store/                    # Zustand state stores
│   │   ├── authStore.ts
│   │   ├── attendanceStore.ts
│   │   └── notificationStore.ts
│   │
│   ├── hooks/                    # Custom hooks
│   │   ├── useAuth.ts
│   │   ├── useQRScanner.ts
│   │   ├── useLocation.ts
│   │   ├── useNotifications.ts
│   │   └── usePermissions.ts
│   │
│   ├── types/                    # TypeScript type definitions
│   │   ├── auth.types.ts
│   │   ├── student.types.ts
│   │   ├── attendance.types.ts
│   │   ├── leave.types.ts
│   │   ├── grievance.types.ts
│   │   ├── payment.types.ts
│   │   └── navigation.types.ts
│   │
│   ├── utils/
│   │   ├── tokenStorage.ts       # expo-secure-store helpers
│   │   ├── dateHelpers.ts
│   │   ├── validators.ts
│   │   └── constants.ts
│   │
│   └── theme/
│       ├── colors.ts
│       ├── typography.ts
│       ├── spacing.ts
│       └── theme.ts
│
├── assets/
│   ├── images/
│   └── fonts/
├── app.json
├── app.config.ts
└── tsconfig.json
```

---

## 🔐 Authentication Module

### `src/store/authStore.ts`
```typescript
// Implement using Zustand
// Store: user object, role, JWT access token, refresh token
// Actions: login, logout, refreshToken, setUser
// Persist tokens in expo-secure-store (NOT AsyncStorage)

interface AuthState {
  user: User | null;
  role: 'student' | 'warden' | 'staff' | 'guard' | null;
  accessToken: string | null;
  isAuthenticated: boolean;
  isLoading: boolean;
  login: (credentials: LoginCredentials) => Promise<void>;
  logout: () => Promise<void>;
  refreshSession: () => Promise<void>;
}
```

### `src/api/client.ts`
```typescript
// Axios instance with:
// - Base URL from environment variable (EXPO_PUBLIC_API_URL)
// - Request interceptor: attach Bearer token from secure store
// - Response interceptor: handle 401 → auto refresh token → retry
// - Handle network errors gracefully
// - Timeout: 15000ms
```

### `src/screens/auth/LoginScreen.tsx`
```typescript
// Fields: Email/Phone, Password
// Validation with react-hook-form + zod
// Show loading state during API call
// On success: store tokens, navigate to role-appropriate navigator
// On failure: show toast with error message
// Design: Clean, branded screen with HostelPulse logo
// Include "Forgot Password" link
```

---

## 👤 Student Module

### `src/screens/student/DashboardScreen.tsx`
```typescript
// Display:
// - Greeting with student name
// - Room info card: Block, Floor, Room Number
// - Roommate names (privacy-respecting)
// - Quick action cards: Pay Fees, Request Leave, Raise Grievance, Attendance
// - Notification bell with unread count
// - Upcoming leave status chip (if any pending/approved)
// - Payment due reminder banner (if dues exist)
```

### `src/screens/student/QRAttendanceScreen.tsx`
```typescript
// IMPORTANT: This is the most critical screen

// Flow:
// 1. Request camera permission using expo-camera
// 2. Request location permission using expo-location
// 3. Show camera view with QR scanner overlay (expo-barcode-scanner)
// 4. On QR detected:
//    a. Extract signed token from QR data
//    b. Get current GPS coordinates (expo-location)
//    c. POST to /api/attendance/scan with:
//       { token, latitude, longitude, deviceId, timestamp }
//    d. Handle responses:
//       - 200: Show success animation + "Attendance Marked!" message
//       - 400 (expired): Show "QR has expired. Ask guard to regenerate."
//       - 400 (outside geofence): Show "You appear to be outside hostel."
//       - 409 (already marked): Show "Attendance already recorded."
//       - 422 (wrong block/year): Show error message
// 5. Prevent duplicate scans: disable scanner for 5s after successful scan
// 6. Show attendance confirmation card with timestamp

// Anti-cheat: 
// - Do not allow mock location (check expo-device for emulator)
// - Include device fingerprint in request headers
// - One-time nonce per scan attempt
```

### `src/screens/student/LeaveRequestScreen.tsx`
```typescript
// Form fields (all required unless noted):
// - Name (pre-filled from profile, read-only)
// - Address (pre-filled, editable)
// - Hostel Name (pre-filled, read-only)
// - Room Number (pre-filled, read-only)
// - Year & Semester (pre-filled, read-only)
// - Registration Number (pre-filled, read-only)
// - Phone Number (pre-filled, editable)
// - Parent Phone Number
// - Type of Leave: Picker with options [Weekend, Medical, Emergency, Academic, Personal]
// - Place of Visit
// - Extra Details (multiline text input)
// - Leave From Date (DateTimePicker)
// - Leave To Date (DateTimePicker)
// - Upload Mentor Approval Document (expo-document-picker, PDF/image)
//
// Validation: 
// - From date cannot be in the past
// - To date must be after From date
// - Document upload required
//
// On submit: POST to /api/leave/request
// Show confirmation screen with leave ID
```

### `src/screens/student/GrievanceScreen.tsx`
```typescript
// Two tabs: "My Tickets" | "New Ticket"

// My Tickets tab:
// - List of grievance tickets with status chips
// - Statuses: Open (red), In Progress (yellow), Resolved (green), Closed (gray)
// - Tap ticket → GrievanceDetailScreen

// New Ticket tab (NewGrievanceScreen):
// Fields:
// - Related To: Picker [Housekeeping, Maintenance, Security, Food, Other]
// - Priority: Segmented control [High, Medium, Low]
// - Category: Dynamic picker based on "Related To":
//   Housekeeping → [Room Cleaning, Washroom, Corridor, Garbage, Pest Control]
//   Electrical → [Power Outage, Socket Fault, Fan, Light Fixture, MCB Trip]
//   Plumbing → [Leakage, Clogged Drain, Low Pressure, Flush Issue, Geyser]
//   Carpentry → [Door Latch, Cupboard Hinge, Bed Repair, Window Lock]
//   Connectivity → [Wi-Fi Down, Weak Signal, LAN Port, Router Issue]
//   Electronics → [Refrigerator, Water Cooler, Washing Machine, CCTV]
//   Food → [Quality, Hygiene, Timing, Menu Issue, Shortage]
//   Safety → [Broken Lock, Suspicious Activity, Corridor Lighting, Hazard]
//   Emergency → [Medical, Fire Hazard, Gas Leak, Flooding, Electrical Short]
// - Description: Multiline text (min 20 chars)
// - Image Upload: expo-image-picker (up to 3 images)
// - Submit button
```

### `src/screens/student/PaymentScreen.tsx`
```typescript
// Show current dues with breakdown:
// - Fee type (Hostel Rent, Mess, Other)
// - Amount due
// - Due date
// - Status badge

// Pay Now button → opens Razorpay WebView
// On payment success webhook confirmation:
// - Show receipt modal with transaction ID
// - Update ledger view

// Payment History tab:
// - List of past payments: date, amount, method, status, receipt download button
```

### `src/screens/student/MessagingScreen.tsx`
```typescript
// Chat interface between Student ↔ Warden (frontdesk)
// Thread types: [General Query, Leave Clarification, Payment Issue, Room Change]
// 
// Features:
// - Message bubbles (student right, warden left)
// - Timestamps on messages
// - Thread status: Open | Awaiting Student | Awaiting Warden | Closed
// - New thread button with subject/type selector
// - File attachment support (images, documents)
// - Real-time updates via polling (every 10s) or WebSocket if available
// - Unread message indicator
```

---

## 🛡️ Guard Module

### `src/screens/guard/GuardDashboardScreen.tsx`
```typescript
// Stats overview:
// - Total students in hostel tonight
// - Attendance marked count
// - On approved leave count  
// - Missing / unaccounted count (highlighted in red)
//
// Quick actions:
// - Start Attendance Session
// - View Approved Leaves
// - Missing Students List
// - Generate Late Entry QR
```

### `src/screens/guard/QRGeneratorScreen.tsx`
```typescript
// This is where the guard creates attendance sessions

// Step 1: Select Block (dropdown from API)
// Step 2: Select Year/Semester (1st Year, 2nd Year, etc.)
// Step 3: System shows valid time window:
//   - 1st Year: 7:30 PM – 9:00 PM
//   - 2nd Year: 7:30 PM – 10:00 PM
//   - Warn if outside window, require override PIN for late entry

// Step 4: POST /api/attendance/session/create
// Response: { sessionId, signedToken, expiresAt }

// Step 5: Display QR code using react-native-qrcode-svg
// - QR regenerates every 30 seconds automatically (countdown timer shown)
// - Show session info: Block, Year, Start time, Student count
// - Prominent countdown timer showing seconds until QR refresh

// Step 6: Real-time scan feed — list of students who scanned (live update)
// Step 7: "End Session" button → POST /api/attendance/session/end
```

### `src/screens/guard/LeaveValidationScreen.tsx`
```typescript
// List of students with approved leave TODAY
// For each entry:
//   - Student name, photo, room number
//   - Leave type, destination, return date
//   - Exit Status: [Not Yet Left | Exited | Returned]
//   - "Mark Exit" / "Mark Return" buttons
// On mark exit/return: POST /api/leave/{id}/exit or /return
// with guard device ID + timestamp + GPS
```

### `src/screens/guard/MissingStudentsScreen.tsx`
```typescript
// Students who:
// - Did NOT mark attendance
// - Are NOT on approved leave
// - Are NOT marked as exited
// Show: Name, Room, Phone number, Parent phone
// Action: "Alert Warden" button → sends push notification to warden
// Refresh button + auto-refresh every 2 minutes during attendance window
```

---

## 🏛️ Warden (Admin) Module

### `src/screens/warden/WardenDashboardScreen.tsx`
```typescript
// Summary cards:
// - Total students
// - Leave requests pending (with alert if >5)
// - Open grievance tickets (with alert for High priority)
// - Payments pending verification
// - Tonight's attendance completion %
//
// Recent activity feed:
// - Last 10 events (leave requests, grievances, payments, messages)
// - Tap to navigate to relevant screen
```

### `src/screens/warden/LeaveApprovalsScreen.tsx`
```typescript
// Tabs: Pending | Approved | Rejected

// Pending tab:
// - Leave request cards with student info
// - Swipe right = Approve, Swipe left = Reject (with confirmation)
// - Tap → full detail view with document preview
// - Bulk select + approve/reject

// On approve: PUT /api/leave/{id}/approve
// On reject: PUT /api/leave/{id}/reject with reason (required text field)
```

### `src/screens/warden/GrievanceManagementScreen.tsx`
```typescript
// Filter bar: All | High Priority | Open | In Progress | Resolved
// Sort by: Date | Priority | Category

// Ticket card shows:
// - Category icon + name
// - Priority badge (color-coded)
// - Student name + room
// - Creation date
// - Current status
// - Assigned staff (or "Unassigned")

// On tap → full detail:
// - Student message + images
// - Assign to Staff (dropdown of available staff members)
// - Set SLA deadline
// - Add internal note
// - View staff updates + completion proof
// - Reopen option if closure unsatisfactory
```

### `src/screens/warden/StudentListScreen.tsx`
```typescript
// Searchable, filterable list of all students
// Filters: Block, Floor, Year, Payment Status
// Each card: Photo, Name, Room, Registration No., Payment status chip
// Tap → StudentDetailScreen:
//   - Full profile with documents (Aadhaar, PAN, etc.) — tap to view
//   - Room allocation history
//   - Payment ledger
//   - Leave history
//   - Grievance history
//   - Room change option
```

---

## 👷 Staff Module

### `src/screens/staff/StaffDashboardScreen.tsx`
```typescript
// My Tasks list:
// - Assigned grievance tickets
// - Status: Assigned | In Progress | Completed
// - Priority badge
// - Room location
// - Due date (SLA timer — show red if overdue)

// Tap ticket → TaskDetailScreen:
// - Full grievance description
// - Student-uploaded images
// - Status update button: Mark In Progress → Mark Complete
// - Upload completion proof (required before marking complete):
//   - expo-image-picker for photo evidence
//   - Optional note/comment
// - Completion auto-notifies student + warden
```

---

## 🔔 Notifications

### `src/hooks/useNotifications.ts`
```typescript
// Setup expo-notifications:
// 1. Request permission on app launch
// 2. Get Expo push token → POST to /api/notifications/register-token
// 3. Handle foreground notifications (show toast)
// 4. Handle background/killed state (navigate on tap)
// 5. Notification types to handle:
//    - leave_approved / leave_rejected
//    - attendance_confirmed
//    - grievance_updated / grievance_resolved
//    - payment_confirmed
//    - new_message
//    - warden_broadcast
//    - guard_alert (missing student)
```

---

## 📐 Design System & Theme

### `src/theme/colors.ts`
```typescript
export const colors = {
  primary: '#1B4FD8',        // Deep institutional blue
  primaryLight: '#3B6EF0',
  primaryDark: '#0F2FA0',
  secondary: '#F59E0B',      // Amber accent for alerts
  success: '#10B981',        // Green for approved/success
  error: '#EF4444',          // Red for rejected/missing/urgent
  warning: '#F97316',        // Orange for pending/medium priority
  
  background: '#F8FAFC',     // Near-white background
  surface: '#FFFFFF',        // Card/sheet background
  surfaceVariant: '#F1F5F9', // Subtle surface
  
  textPrimary: '#0F172A',    // Near-black
  textSecondary: '#64748B',  // Muted gray
  textDisabled: '#CBD5E1',
  
  border: '#E2E8F0',
  divider: '#F1F5F9',
  
  // Role-specific accent colors
  studentAccent: '#6366F1',  // Indigo
  wardenAccent: '#0EA5E9',   // Sky blue  
  guardAccent: '#14B8A6',    // Teal
  staffAccent: '#8B5CF6',    // Purple
};
```

### `src/theme/typography.ts`
```typescript
// Use expo-font to load:
// - Display: 'Sora' (headings, bold numbers)
// - Body: 'DM Sans' (all body text, labels)
// - Mono: 'JetBrains Mono' (codes, QR token IDs)

export const typography = {
  h1: { fontFamily: 'Sora-Bold', fontSize: 28, lineHeight: 36 },
  h2: { fontFamily: 'Sora-SemiBold', fontSize: 22, lineHeight: 30 },
  h3: { fontFamily: 'Sora-SemiBold', fontSize: 18, lineHeight: 26 },
  body1: { fontFamily: 'DMSans-Regular', fontSize: 16, lineHeight: 24 },
  body2: { fontFamily: 'DMSans-Regular', fontSize: 14, lineHeight: 20 },
  caption: { fontFamily: 'DMSans-Regular', fontSize: 12, lineHeight: 16 },
  label: { fontFamily: 'DMSans-Medium', fontSize: 14, lineHeight: 20 },
  mono: { fontFamily: 'JetBrainsMono-Regular', fontSize: 13 },
};
```

### UI Component Guidelines
```typescript
// AppButton variants: 'primary' | 'secondary' | 'outline' | 'ghost' | 'danger'
// Border radius: 12px (buttons), 16px (cards), 8px (inputs)
// Shadows: Subtle elevation using platform-specific shadows
// Animations: Use Animated API or react-native-reanimated for:
//   - Screen transitions
//   - QR scan success pulse
//   - List item enter animations (staggered)
//   - Loading skeletons
//   - Status change transitions
```

---

## 🌐 API Integration Reference

### Base Configuration
```typescript
// Environment variables (app.config.ts):
// EXPO_PUBLIC_API_URL=https://api.hostelpulse.in/v1
// EXPO_PUBLIC_RAZORPAY_KEY=rzp_live_xxx

// All endpoints require: Authorization: Bearer <access_token>
// Content-Type: application/json (or multipart/form-data for uploads)
```

### Endpoint Reference

```typescript
// AUTH
POST   /auth/login                    // { email, password } → { accessToken, refreshToken, user }
POST   /auth/refresh                  // { refreshToken } → { accessToken }
POST   /auth/logout                   // Invalidate tokens

// STUDENT
GET    /student/profile               // Current student's profile
GET    /student/room                  // Room + roommate info
GET    /student/dashboard             // Dashboard summary data

// ATTENDANCE
POST   /attendance/scan               // { token, lat, lng, deviceId, nonce }
GET    /attendance/history            // Student's attendance records
POST   /attendance/session/create     // [Guard] Create session
GET    /attendance/session/:id/scans  // [Guard] Live scan feed
POST   /attendance/session/:id/end    // [Guard] End session
POST   /attendance/session/:id/late-qr // [Guard] Generate late QR

// LEAVE
GET    /leave/my-requests             // Student's leave history
POST   /leave/request                 // Submit leave (multipart with doc)
GET    /leave/pending                 // [Warden] Pending approvals
PUT    /leave/:id/approve             // [Warden]
PUT    /leave/:id/reject              // [Warden] { reason }
GET    /leave/approved-today          // [Guard] Today's approved leaves
POST   /leave/:id/exit                // [Guard] Mark exit
POST   /leave/:id/return              // [Guard] Mark return

// GRIEVANCE
GET    /grievance/my-tickets          // Student's tickets
POST   /grievance/create              // { category, priority, description } + images
GET    /grievance/all                 // [Warden] All tickets with filters
PUT    /grievance/:id/assign          // [Warden] { staffId, slaDueAt }
GET    /grievance/my-tasks            // [Staff] Assigned tasks
PUT    /grievance/:id/status          // [Staff] { status, note } + proof image
PUT    /grievance/:id/close           // [Warden]
PUT    /grievance/:id/reopen          // [Warden] { reason }

// PAYMENT
GET    /payment/dues                  // Current outstanding dues
GET    /payment/history               // Payment history
POST   /payment/initiate              // { amount } → { orderId, key }
GET    /payment/receipt/:id           // Download receipt URL

// MESSAGING
GET    /messages/threads              // All threads for current user
POST   /messages/threads              // Create thread { type, subject }
GET    /messages/threads/:id          // Messages in thread
POST   /messages/threads/:id/send     // { content } + optional attachment
PUT    /messages/threads/:id/status   // { status }

// NOTIFICATIONS
POST   /notifications/register-token  // { expoPushToken, platform }

// WARDEN
GET    /warden/students               // Student list with filters
GET    /warden/students/:id           // Full student detail
GET    /warden/dashboard/stats        // Summary stats
POST   /warden/broadcast              // { title, message, targetRole }
GET    /rooms/available               // Available rooms for reallocation
PUT    /students/:id/room             // { roomId } Room change
```

---

## 🔒 Security Implementation

### Token Management (`src/utils/tokenStorage.ts`)
```typescript
// Use expo-secure-store (NOT AsyncStorage) for:
// - ACCESS_TOKEN
// - REFRESH_TOKEN
// - USER_DATA (encrypted)

// Token refresh logic:
// - Access token expires in 15 minutes
// - Refresh token expires in 7 days
// - Auto-refresh on 401 response with queued request retry
// - On refresh failure → logout and redirect to login
```

### QR Attendance Security
```typescript
// QR Token Structure (JWT-like):
// {
//   sessionId: string,
//   guardId: string,
//   blockId: string,
//   year: number,
//   issuedAt: number,    // Unix timestamp
//   expiresAt: number,   // issuedAt + 30 seconds
//   nonce: string,       // UUID, unique per QR generation
//   signature: string    // HMAC-SHA256 signed by server
// }

// Student scan submission:
// {
//   token: string,       // Raw QR content
//   latitude: number,
//   longitude: number,
//   accuracy: number,    // GPS accuracy in meters
//   deviceId: string,    // expo-device unique ID
//   scanNonce: string,   // Client-generated one-time ID
//   timestamp: number    // Client timestamp (server cross-checks)
// }
```

### Location Permissions
```typescript
// Request foreground location permission before QR scanner loads
// If denied → show explanation modal → link to settings
// Never store location history locally
// Only send during active scan submission
```

---

## ⚙️ App Configuration (`app.config.ts`)

```typescript
export default {
  expo: {
    name: "HostelPulse",
    slug: "hostelpulse",
    version: "1.0.0",
    orientation: "portrait",
    icon: "./assets/images/icon.png",
    scheme: "hostelpulse",
    userInterfaceStyle: "light",
    splash: {
      image: "./assets/images/splash.png",
      resizeMode: "contain",
      backgroundColor: "#1B4FD8"
    },
    ios: {
      supportsTablet: false,
      bundleIdentifier: "com.hostelpulse.app",
      infoPlist: {
        NSCameraUsageDescription: "HostelPulse needs camera access to scan QR codes for attendance.",
        NSLocationWhenInUseUsageDescription: "HostelPulse needs your location to verify you are within the hostel premises during attendance.",
        NSPhotoLibraryUsageDescription: "HostelPulse needs photo library access to upload grievance images."
      }
    },
    android: {
      adaptiveIcon: {
        foregroundImage: "./assets/images/adaptive-icon.png",
        backgroundColor: "#1B4FD8"
      },
      package: "com.hostelpulse.app",
      permissions: [
        "CAMERA",
        "ACCESS_FINE_LOCATION",
        "ACCESS_COARSE_LOCATION",
        "READ_EXTERNAL_STORAGE",
        "WRITE_EXTERNAL_STORAGE",
        "RECEIVE_BOOT_COMPLETED",
        "VIBRATE"
      ]
    },
    plugins: [
      "expo-camera",
      "expo-location",
      "expo-notifications",
      "expo-secure-store",
      [
        "expo-image-picker",
        { "photosPermission": "Allow HostelPulse to upload grievance images." }
      ]
    ],
    extra: {
      eas: { projectId: "YOUR_EAS_PROJECT_ID" }
    }
  }
};
```

---

## 🚀 Implementation Phases

### Phase 1 — Auth + Navigation Shell (Week 1)
- [ ] Project setup with all dependencies
- [ ] Theme system + base components
- [ ] Login screen with form validation
- [ ] JWT auth flow with secure storage
- [ ] Role-based navigation routing
- [ ] Bottom tab navigators per role

### Phase 2 — Student Core (Week 2–3)
- [ ] Student Dashboard
- [ ] Profile screen
- [ ] Payment screen + Razorpay WebView
- [ ] Payment history
- [ ] Push notification setup

### Phase 3 — Leave & Guard Validation (Week 4)
- [ ] Leave request form (all fields + document upload)
- [ ] Leave history & status tracking
- [ ] Guard: Leave validation screen
- [ ] Guard: Mark exit / return

### Phase 4 — QR Attendance (Week 5)
- [ ] Guard: QR Generator screen with auto-refresh
- [ ] Guard: Live scan feed
- [ ] Student: QR Scanner with anti-cheat checks
- [ ] Guard: Missing students screen

### Phase 5 — Grievances + Messaging (Week 6–7)
- [ ] Student: New grievance form with image upload
- [ ] Student: My tickets list + detail
- [ ] Warden: Grievance management + staff assignment
- [ ] Staff: Task queue + completion proof upload
- [ ] Messaging threads (Student ↔ Warden)

### Phase 6 — Warden Admin (Week 8)
- [ ] Warden dashboard with stats
- [ ] Student list + detail view
- [ ] Leave approval flow (swipe gestures)
- [ ] Payment verification
- [ ] Broadcast notification

---

## ✅ Quality Checklist

Before marking any screen complete:

- [ ] TypeScript types defined for all props and API responses
- [ ] Loading states shown during API calls (skeleton loaders preferred)
- [ ] Error states handled with user-friendly messages
- [ ] Empty states designed with illustration + helpful text
- [ ] Form validation with inline error messages
- [ ] Pull-to-refresh on all list screens
- [ ] Keyboard-aware scroll views on all form screens
- [ ] Safe area insets respected on all screens
- [ ] Works on both iOS and Android (test on both)
- [ ] Accessible (accessibility labels on interactive elements)
- [ ] No hardcoded strings (use constants file)
- [ ] Network failure handled gracefully (offline banner)

---

## 📝 Additional Notes for the AI Coding Assistant

1. **Always use TypeScript** — no `any` types unless absolutely necessary.
2. **Use `expo-secure-store`** for all sensitive data, never `AsyncStorage`.
3. **The QR attendance flow is the most security-sensitive feature** — never skip the geofence check or nonce validation.
4. **Forms** should use `react-hook-form` + `zod` schemas for all validation.
5. **API calls** should be wrapped in `@tanstack/react-query` hooks for caching and loading states.
6. **File uploads** should show progress indicators.
7. **The Guard QR screen** must auto-refresh the QR code every 30 seconds — use `setInterval` with cleanup.
8. **Role-based access** must be enforced in navigation — a student should never be able to reach warden/guard screens even by URL manipulation.
9. **Use react-native-toast-message** for all success/error feedback — not `Alert.alert` for non-critical messages.
10. **Implement skeleton loaders** (not spinners) for list screens using `react-native-paper`'s skeleton or a custom implementation.