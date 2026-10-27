# Test Cases – Restful-Booker API

Base URL: `https://restful-booker.herokuapp.com`

All tests also check that the response time is below 5000 ms.

**Execution:** 2026-10-27 – Postman Runner – 14 cases: **11 passed, 3 failed** (3 defects reported).

## Summary

| ID | Title | Method | Endpoint | Expected | Actual | Status |
| --- | --- | --- | --- | --- | --- | --- |
| HC-01 | API is up | GET | /ping | 201 | 201 | Passed |
| AUTH-01 | Login with valid credentials | POST | /auth | 200 + token | 200 + token | Passed |
| AUTH-02 | Login with invalid credentials | POST | /auth | 401, no token | 200, no token | Failed – [BUG-01](bugs/BUG-01.md) |
| E2E-01 | Create booking | POST | /booking | 200 + booking ID | 200 + booking ID | Passed |
| E2E-02 | Get created booking | GET | /booking/{id} | 200 + same data | 200 + same data | Passed |
| E2E-03 | Update booking | PUT | /booking/{id} | 200 + new data | 200 + new data | Passed |
| E2E-04 | Partial update | PATCH | /booking/{id} | 200 + only price changed | 200 + only price changed | Passed |
| E2E-05 | Delete booking | DELETE | /booking/{id} | 201 | 201 | Passed |
| E2E-06 | Get deleted booking | GET | /booking/{id} | 404 | 404 | Passed |
| NEG-01 | Booking that does not exist | GET | /booking/999999999 | 404 | 404 | Passed |
| NEG-02 | Create without firstname | POST | /booking | 400 | 500 | Failed – [BUG-02](bugs/BUG-02.md) |
| NEG-03 | Checkout before checkin | POST | /booking | 400, not created | 200, booking created | Failed – [BUG-03](bugs/BUG-03.md) |
| NEG-04 | Update without token | PUT | /booking/{id} | 403 | 403 | Passed |
| NEG-05 | Delete without token | DELETE | /booking/{id} | 403 | 403 | Passed |

---

## 01 – Health check

### HC-01 – API is up

- **Request:** `GET /ping`
- **Expected result:** status 201 (as defined in the API documentation)
- **Actual result:** As expected.
- **Status:** Passed

## 02 – Authentication

### AUTH-01 – Login with valid credentials

- **Request:** `POST /auth` with the valid username and password
- **Expected result:** status 200 and a token in the body. The token is saved for the next tests.
- **Actual result:** As expected.
- **Status:** Passed

### AUTH-02 – Login with invalid credentials

- **Request:** `POST /auth` with a wrong password
- **Expected result:** status 401 Unauthorized and no token in the body
- **Actual result:** Status 200 OK. No token is returned, so access is denied, but the status code is wrong.
- **Status:** Failed – [BUG-01](bugs/BUG-01.md)

## 03 – Booking E2E flow

These tests run in order. Each one uses the booking ID created in E2E-01.

### E2E-01 – Create booking

- **Request:** `POST /booking` with all fields
- **Expected result:** status 200, a numeric booking ID, and saved data equal to sent data
- **Actual result:** As expected.
- **Status:** Passed

### E2E-02 – Get created booking

- **Request:** `GET /booking/{id}`
- **Expected result:** status 200, the same values sent in E2E-01, and correct data types
- **Actual result:** As expected.
- **Status:** Passed

### E2E-03 – Update booking (PUT)

- **Request:** `PUT /booking/{id}` with token and new values for all fields
- **Expected result:** status 200 and all fields updated
- **Actual result:** As expected.
- **Status:** Passed

### E2E-04 – Partial update (PATCH)

- **Request:** `PATCH /booking/{id}` with token, changing only `totalprice`
- **Expected result:** status 200, price updated, other fields not changed
- **Actual result:** As expected.
- **Status:** Passed

### E2E-05 – Delete booking

- **Request:** `DELETE /booking/{id}` with token
- **Expected result:** status 201 (as defined in the API documentation)
- **Actual result:** As expected.
- **Status:** Passed

### E2E-06 – Get deleted booking

- **Request:** `GET /booking/{id}`
- **Expected result:** status 404 Not Found
- **Actual result:** As expected.
- **Status:** Passed

## 04 – Negative tests

### NEG-01 – Get booking that does not exist

- **Request:** `GET /booking/999999999`
- **Expected result:** status 404 Not Found
- **Actual result:** As expected.
- **Status:** Passed

### NEG-02 – Create booking without firstname

- **Request:** `POST /booking` without the `firstname` field
- **Expected result:** status 400 Bad Request
- **Actual result:** Status 500 Internal Server Error. The API does not validate the missing field.
- **Status:** Failed – [BUG-02](bugs/BUG-02.md)

### NEG-03 – Create booking with checkout before checkin

- **Request:** `POST /booking` with checkin 2026-12-10 and checkout 2026-12-01
- **Expected result:** status 400 Bad Request and the booking is not created
- **Actual result:** Status 200 OK. The booking was created with invalid dates (booking ID 722).
- **Status:** Failed – [BUG-03](bugs/BUG-03.md)

### NEG-04 – Update booking without token

- **Request:** `PUT /booking/{id}` without the token. The test creates its own booking first.
- **Expected result:** status 403 Forbidden and the booking does not change
- **Actual result:** As expected.
- **Status:** Passed

### NEG-05 – Delete booking without token

- **Request:** `DELETE /booking/{id}` without the token. The test creates its own booking first.
- **Expected result:** status 403 Forbidden and the booking is not deleted
- **Actual result:** As expected.
- **Status:** Passed
