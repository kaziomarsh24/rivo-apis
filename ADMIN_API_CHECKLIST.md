# Rivo Admin Dashboard API Testing & Verification Checklist

**Environment**: `http://10.10.28.53:80/api` or `http://localhost:8000/api`  
**Authentication Header**: `Authorization: Bearer {{adminToken}}`  
**Default Admin**: `admin@rivo.app` / `Password@123`  
**Date**: 2026-11-01  

---

## 📌 Status Summary

- [x] **Database Migration**: Suspension columns (`suspended_at`, `suspension_reason`) on `users` and `stores`.
- [x] **Admin Seeder**: `admin@rivo.app` created with Spatie role `admin`.
- [x] **Role Guard Middleware**: `role:admin` alias registered in `bootstrap/app.php` with clean JSON 403 handling.
- [x] **Suspension Enforcement**: Suspended users/stores blocked at login with custom message.
- [x] **Admin Dashboard Stats**: `GET /api/v1/admin/dashboard/stats` with 8 KPI metrics and 5-bar sparklines.
- [x] **Recent Platform Activity**: `GET /api/v1/admin/dashboard/activity` aggregating real database events.
- [x] **Automated Tests**: 6 Feature tests in `tests/Feature/AdminDashboardTest.php` passing 100% (125 assertions).
- [x] **Bruno Documentation**: Separate `Admin Dashboard/` collection with organized subfolders and `.yml` requests.

---

## 📋 API Checklist & Test Steps

### Module 1: Authentication & Password Recovery (Common / Unified)

> **Note**: Uses the common Auth API in `Rivo-api/Auth/`. Logging in as `admin@rivo.app` automatically saves the token to Bruno's `{{adminToken}}`.

| Method | Endpoint | Bruno Path | Description | Tested |
| :--- | :--- | :--- | :--- | :---: |
| `POST` | `/api/v1/auth/login` | `Auth/Authentication/Login` | Logs in customer, vendor, or administrator (`adminToken`) | [x] |
| `POST` | `/api/v1/auth/forgot-password` | `Auth/Password Management/Forgot Password` | Sends 6-digit verification OTP to email | [x] |
| `POST` | `/api/v1/auth/verify-password-otp` | `Auth/Password Management/Verify Reset OTP` | Verifies code and generates reset token | [x] |
| `POST` | `/api/v1/auth/reset-password-with-token` | `Auth/Password Management/Reset Password with Token` | Resets password using verified token | [x] |

---

### Module 2: Dashboard Overview & Real-Time Telemetry

| Method | Endpoint | Bruno Path | Description | Tested |
| :--- | :--- | :--- | :--- | :---: |
| `GET` | `/api/v1/admin/dashboard/stats` | `Admin Dashboard/Overview/Get Dashboard Stats` | 8 KPIs: Users, Pets, Revenue, Subscriptions, Providers | [x] |
| `GET` | `/api/v1/admin/dashboard/activity` | `Admin Dashboard/Overview/Get Recent Activity` | Real-time audit events feed for the last 24 hours | [x] |

---

## 🧪 Verification Commands

### 1. Run Automated PHPUnit / Pest Test Suite
```bash
docker exec rivo-app php artisan test --filter=AdminDashboardTest
```
**Result**: `PASS Tests\Feature\AdminDashboardTest (6 passed, 125 assertions)`

### 2. cURL Verification

#### Step A: Admin Login
```bash
curl -X POST "http://10.10.28.53:80/api/v1/auth/login" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@rivo.app","password":"Password@123"}'
```

#### Step B: Get Dashboard Statistics (Protected)
```bash
curl -X GET "http://10.10.28.53:80/api/v1/admin/dashboard/stats?range=month" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer <YOUR_ADMIN_TOKEN>"
```

#### Step C: Get Recent Activity Feed
```bash
curl -X GET "http://10.10.28.53:80/api/v1/admin/dashboard/activity?limit=20" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer <YOUR_ADMIN_TOKEN>"
```

