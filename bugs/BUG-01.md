# BUG-01 – Login with invalid credentials returns 200 OK instead of 401 Unauthorized

| Field | Value |
| --- | --- |
| ID | BUG-01 |
| Related test case | AUTH-02 |
| Severity | Minor |
| Priority | Medium |
| Endpoint | `POST /auth` |
| Environment | restful-booker.herokuapp.com – Postman – 2026-10-27 |
| Reported by | Richard Tripodi |

## Steps to reproduce

1. Send `POST /auth` with this body:

```json
{
  "username": "admin",
  "password": "wrong_password"
}
```

## Expected result

Status `401 Unauthorized`, and no token in the response.

## Actual result

Status `200 OK`. No token is returned, so access is not granted.

## Impact

Access is correctly denied, but the status code says the request was successful. Any client or monitoring tool that checks only the status code will treat a failed login as a successful one. This makes failed logins harder to detect, including possible brute-force attempts.

## Evidence

- Newman / Postman result: `expected response to have status code 401 but got 200`
- Screenshot: [images/BUG-01.png](../images/BUG-01.png)
