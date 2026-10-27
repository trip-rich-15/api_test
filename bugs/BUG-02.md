# BUG-02 – Creating a booking without a required field returns 500 instead of 400

| Field | Value |
| --- | --- |
| ID | BUG-02 |
| Related test case | NEG-02 |
| Severity | Major |
| Priority | Medium |
| Endpoint | `POST /booking` |
| Environment | restful-booker.herokuapp.com – Postman – 2026-10-27 |
| Reported by | Richard Tripodi |

## Steps to reproduce

1. Send `POST /booking` with the headers `Content-Type: application/json` and `Accept: application/json`, and this body (without `firstname`):

```json
{
  "lastname": "Lopez",
  "totalprice": 150,
  "depositpaid": true,
  "bookingdates": { "checkin": "2026-12-01", "checkout": "2026-12-05" },
  "additionalneeds": "Breakfast"
}
```

## Expected result

Status `400 Bad Request`, with a message that says which field is missing.

## Actual result

Status `500 Internal Server Error`.

## Impact

The API does not validate the request before processing it, and the missing field causes a server error. The client does not know what was wrong with the request. A 500 error also means that invalid input can break the server logic, and these errors create noise in production monitoring.

## Evidence

- Newman / Postman result: `expected response to have status code 400 but got 500`
- Screenshot: [images/BUG-02.png](../images/BUG-02.png)
