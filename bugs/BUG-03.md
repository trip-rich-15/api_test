# BUG-03 – A booking is created with a checkout date before the checkin date

| Field | Value |
| --- | --- |
| ID | BUG-03 |
| Related test case | NEG-03 |
| Severity | Major |
| Priority | High |
| Endpoint | `POST /booking` |
| Environment | restful-booker.herokuapp.com – Postman – 2026-10-27 |
| Reported by | Richard Tripodi |

## Steps to reproduce

1. Send `POST /booking` with the headers `Content-Type: application/json` and `Accept: application/json`, and these dates:

```json
{
  "firstname": "Ana",
  "lastname": "Lopez",
  "totalprice": 150,
  "depositpaid": true,
  "bookingdates": { "checkin": "2026-12-10", "checkout": "2026-12-01" },
  "additionalneeds": "Breakfast"
}
```

## Expected result

Status `400 Bad Request`. The booking is not created.

## Actual result

Status `200 OK`. The booking is created and saved with the invalid dates (example: booking ID 722).

## Impact

The API does not apply a basic business rule. Bookings with impossible dates are saved in the system. This can cause wrong availability, wrong prices for the stay, and problems in every process that uses booking dates (invoices, reports, room assignment).

## Evidence

- Newman / Postman result: `expected response to have status code 400 but got 200` and `expected '{"bookingid":722, ...' to not include 'bookingid'`
- Screenshot: [images/BUG-03.png](../images/BUG-03.png)
