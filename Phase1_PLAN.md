# Phase 1 - Backend foundation plan (Spring Boot + MySQL + Firebase Auth)

## Goal
Get the backend compiling and running with:
- MySQL datasource (instead of H2)
- Firebase Authentication verification via Firebase Admin SDK
- Role enforcement (admin vs employee)
- Existing Employee endpoints guarded by role

## Steps
1. Update `backend/pom.xml`
   - Remove/replace H2 runtime dependency
   - Add MySQL connector
   - Add Spring Security dependencies
   - Add Firebase Admin SDK

2. Update `backend/application.properties`
   - Configure MySQL JDBC URL, username, password
   - Enable JPA ddl-auto=update

3. Implement Firebase token verification
   - Add `security/FirebaseAuthFilter`:
     - Read `Authorization: Bearer <idToken>`
     - Verify token using Firebase Admin SDK
     - Extract uid and store in SecurityContext (custom principal)

4. Implement role checks
   - Add `User` table/entity (`users`) with columns:
     - `id` (PK)
     - `firebase_uid` (unique)
     - `email`
     - `role` (admin/employee)
   - Add `security/RoleBasedAccess` (method-level security or request matcher)
   - Ensure admin endpoints (e.g. employee CRUD) require role=admin

5. Seed initial admin user (developer-friendly)
   - Add a `data/DatabaseSeeder` that inserts an admin row if missing.
   - (Option: read admin email from env var or config)

6. Validate
   - `mvn test` and `mvn package`
   - Ensure endpoints return 401/403 without/with wrong token/role.

