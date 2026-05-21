# Lab7 - Full-Stack Authentication System (Angular 21)

A complete authentication boilerplate built with Angular 21, featuring JWT authentication, role-based access control (RBAC), email verification, and an Admin management panel.

## Live Links
* **Frontend Application:** https://lab7-peterjohn18.onrender.com
* **Backend API (Swagger):** https://lab7-backend-peterjohn18.onrender.com/api-docs
* **Backend Repository:** https://github.com/PeterJohn18/Lab7-backend

## Features
- Email sign up + email verification
- Login / Logout
- JWT auth header for API requests
- Refresh tokens (cookie-based) + auto-refresh before access token expiry
- Forgot password + reset password
- Role-based authorization (User & Admin)
- Admin area for account management
- Profile area for viewing/updating your own account

## Setup Instructions

### Prerequisites
- Node.js (LTS recommended)
- npm (comes with Node.js)

### 1. Clone the repository
```bash
git clone https://github.com/PeterJohn18/lab7.git
cd lab7
```

### 2. Install dependencies
```bash
npm install
```

### 3. Run with Fake Backend (Stage A - No API needed)
Enable the fake backend in `src/app/app.module.ts` by uncommenting the `fakeBackendProvider` line:
```ts
providers: [
    { provide: APP_INITIALIZER, useFactory: appInitializer, multi: true, deps: [AccountService] },
    { provide: HTTP_INTERCEPTORS, useClass: JwtInterceptor, multi: true },
    { provide: HTTP_INTERCEPTORS, useClass: ErrorInterceptor, multi: true },
    // Uncomment below for Stage A (Fake Backend):
    fakeBackendProvider
],
```
Then run:
```bash
npm start
```

### 4. Run with Live API (Stage B - Real Backend)
Make sure `fakeBackendProvider` is **commented out** in `app.module.ts`, then update the API URL in:
- `src/environments/environment.ts` (development)
- `src/environments/environment.prod.ts` (production)

Then run:
```bash
npm start
```

### 5. Production Build
```bash
ng build --configuration production
```

## Routing Fix (for Render deployment)
A `_redirects` file is included in `src/` and referenced in `angular.json` to handle SPA deep links on Render:
```
/* /index.html 200
```

## Security Notes
- No sensitive data is hardcoded
- JWT secrets and database credentials are stored in `.env` (ignored by git)
- CORS is configured via environment variables on the backend
