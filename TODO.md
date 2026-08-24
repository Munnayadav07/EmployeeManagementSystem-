# EMS Project Blueprint - TODO

## Phase 1: Backend foundation (Spring Boot + MySQL + Firebase auth)
- [ ] Update/extend `backend/pom.xml` with dependencies:
  - Spring Web, Spring Data JPA, MySQL connector
  - Firebase Admin SDK (to verify Firebase ID tokens)
  - (Optional) Lombok
- [ ] Update `backend/src/main/resources/application.properties` for MySQL connection + JPA settings.
- [ ] Expand backend model beyond current `Employee`:
  - [ ] Add `Department` entity + repository + service + controller
  - [ ] Add `Attendance` entity + repository + service + controller
  - [ ] Add `Leave` entity + repository + service + controller
  - [ ] Add `User` entity (role + firebaseUid)
- [ ] Add Firebase token verification middleware:
  - [ ] Implement security filter/interceptor to validate `Authorization: Bearer <token>`
  - [ ] Extract firebase uid and load role from `users` table
- [ ] Implement role-based access:
  - [ ] Admin-only endpoints
  - [ ] Employee-only endpoints

## Phase 2: Backend APIs to match blueprint
- [ ] Implement employee CRUD APIs (admin) and self-service APIs (employee)
- [ ] Implement attendance mark/query APIs
- [ ] Implement leave apply/approve/reject/history APIs
- [ ] Implement reports summary endpoints used for charts

## Phase 3: Frontend React wiring (React + Firebase Auth + backend REST)
- [ ] Create frontend API service wrapper (attach Firebase token)
- [ ] Refactor admin pages to use backend REST instead of Firestore:
  - [ ] Admin employees CRUD
  - [ ] Admin department management
  - [ ] Leave approvals
  - [ ] Attendance viewing
  - [ ] Reports
  - [ ] User accounts management
- [ ] Implement employee pages (replace placeholders in `EmployeeModulePages.js`):
  - [ ] View profile
  - [ ] Edit personal details
  - [ ] Apply leave + view status/history
  - [ ] View attendance
  - [ ] View salary (optional) + payslips
  - [ ] Notifications
  - [ ] Settings (change password, etc.)
- [ ] Ensure routing exists for all required public/admin/employee pages

## Phase 4: Dashboard charts
- [ ] Implement chart components (pie/bar/line) on Admin dashboard
- [ ] Connect chart data to backend reports endpoints

## Phase 5: End-to-end validation
- [ ] Run MySQL locally and verify backend migrations/DDL
- [ ] Run backend and confirm all endpoints
- [ ] Run frontend and validate login + role gating
- [ ] Manual test scenarios for admin + employee flows

