# Test Cases – Restful-Booker API

Base URL: `https://restful-booker.herokuapp.com`

All tests also check that the response time is below 5000 ms.

## Summary

| ID | Title | Method | Endpoint | Expected | Actual | Status |
| --- | --- | --- | --- | --- | --- | --- |
| HC-01 | API is up | GET | /ping | 201 | | |
| AUTH-01 | Login with valid credentials | POST | /auth | 200 + token | | |
| AUTH-02 | Login with invalid credentials | POST | /auth | 401, no token | | |
| E2E-01 | Create booking | POST | /booking | 200 + booking ID | | |
| E2E-02 | Get created booking | GET | /booking/{id} | 200 + same data | | |
| E2E-03 | Update booking | PUT | /booking/{id} | 200 + new data | | |
| E2E-04 | Partial update | PATCH | /booking/{id} | 200 + only price changed | | |
| E2E-05 | Delete booking | DELETE | /booking/{id} | 201 | | |
| E2E-06 | Get deleted booking | GET | /booking/{id} | 404 | | |
| NEG-01 | Booking that does not exist | GET | /booking/999999999 | 404 | | |
| NEG-02 | Create without firstname | POST | /booking | 400 | | |
| NEG-03 | Checkout before checkin | POST | /booking | 400, not created | | |
| NEG-04 | Update without token | PUT | /booking/{id} | 403 | | |
| NEG-05 | Delete without token | DELETE | /booking/{id} | 403 | | |

---

## 01 – Health check

### HC-01 – API is up

- **Request:** `GET /ping`
- **Expected result:** status 201 (as defined in the API documentation)
- **Actual result:** _To be completed_
- **Status:** _Not executed_

## 02 – Authentication

### AUTH-01 – Login with valid credentials

- **Request:** `POST /auth` with the valid username and password
- **Expected result:** status 200 and a token in the body. The token is saved for the next tests.
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### AUTH-02 – Login with invalid credentials

- **Request:** `POST /auth` with a wrong password
- **Expected result:** status 401 Unauthorized and no token in the body
- **Actual result:** _To be completed_
- **Status:** _Not executed_

## 03 – Booking E2E flow

These tests run in order. Each one uses the booking ID created in E2E-01.

### E2E-01 – Create booking

- **Request:** `POST /booking` with all fields
- **Expected result:** status 200, a numeric booking ID, and saved data equal to sent data
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### E2E-02 – Get created booking

- **Request:** `GET /booking/{id}`
- **Expected result:** status 200, the same values sent in E2E-01, and correct data types
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### E2E-03 – Update booking (PUT)

- **Request:** `PUT /booking/{id}` with token and new values for all fields
- **Expected result:** status 200 and all fields updated
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### E2E-04 – Partial update (PATCH)

- **Request:** `PATCH /booking/{id}` with token, changing only `totalprice`
- **Expected result:** status 200, price updated, other fields not changed
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### E2E-05 – Delete booking

- **Request:** `DELETE /booking/{id}` with token
- **Expected result:** status 201 (as defined in the API documentation)
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### E2E-06 – Get deleted booking

- **Request:** `GET /booking/{id}`
- **Expected result:** status 404 Not Found
- **Actual result:** _To be completed_
- **Status:** _Not executed_

## 04 – Negative tests

### NEG-01 – Get booking that does not exist

- **Request:** `GET /booking/999999999`
- **Expected result:** status 404 Not Found
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### NEG-02 – Create booking without firstname

- **Request:** `POST /booking` without the `firstname` field
- **Expected result:** status 400 Bad Request
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### NEG-03 – Create booking with checkout before checkin

- **Request:** `POST /booking` with checkin 2026-12-10 and checkout 2026-12-01
- **Expected result:** status 400 Bad Request and the booking is not created
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### NEG-04 – Update booking without token

- **Request:** `PUT /booking/{id}` without the token. The test creates its own booking first.
- **Expected result:** status 403 Forbidden and the booking does not change
- **Actual result:** _To be completed_
- **Status:** _Not executed_

### NEG-05 – Delete booking without token

- **Request:** `DELETE /booking/{id}` without the token. The test creates its own booking first.
- **Expected result:** status 403 Forbidden and the booking is not deleted
- **Actual result:** _To be completed_
- **Status:** _Not executed_
