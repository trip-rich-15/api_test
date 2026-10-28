# Test Plan – Restful-Booker API

## 1. Objective

Verify that the Restful-Booker API manages bookings correctly authentication, creation, query, update and deletion. Also verify that the API rejects invalid data and actions without permission.

## 2. Scope

**In scope**

- `GET /ping` – health check
- `POST /auth` – create token
- `POST /booking` – create booking
- `GET /booking/{id}` – get booking
- `PUT /booking/{id}` – update booking
- `PATCH /booking/{id}` – partial update
- `DELETE /booking/{id}` – delete booking

## 3. Test approach

- **Reference:** the official API documentation is the contract. When the documentation defines a status code, the test uses that code.
- **Validation rules:** when the documentation says nothing, the test uses common REST standar.
- **Checks in every test:** status code and response time (below 5000 ms). Where it applies, also body values and data types.
- **E2E flow:** the booking ID and the token are saved in variables and used by the next requests.
- **Independent negative tests:** each negative test creates its own data, so it does not depend on other tests.

## 4. Risks

| Risk | Impact | Covered by |
| --- | --- | --- |
| Invalid credentials are accepted | High – unauthorized access | AUTH-02 |
| A booking is changed or deleted without permission | High – data loss, fraud | NEG-04, NEG-05 |
| Saved data is different from sent data | High – wrong bookings for customers | E2E-01, E2E-02 |
| Bookings with missing or illogical data are created | Medium – wrong data in the system | NEG-02, NEG-03 |
| Deleted bookings can still be found | Medium – inconsistent data | E2E-06 |

## 5. Test environment

- API: https://restful-booker.herokuapp.com (public demo)
- Tools: Postman, Newman, GitHub Actions (with Node.js)
- Test data: created by the tests in each run

## 6. Entry criteria

- The API answers `GET /ping`
- The Postman collection and environment are available

## 7. Exit criteria

- All test cases were executed
- Every failed test has a bug report with request and response as evidence
- Results are documented in TEST_CASES.md

## 8. Defect severity

| Severity | Description |
| --- | --- |
| Critical | Security or data loss: unauthorized access, data changed without permission |
| Major | Business rule not applied, invalid data is saved |
| Minor | Wrong status code or message, but the result is correct |
| Trivial | Cosmetic issue |
