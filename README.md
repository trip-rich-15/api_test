# Restful-Booker – API Testing (Postman + Newman + GitHub Actions)

API testing project for [Restful-Booker](https://restful-booker.herokuapp.com/apidoc/index.html), a public hotel booking API made for testing practice.

The tests are written in Postman and run automatically with Newman in GitHub Actions on every push.

## What this project shows

- Testing of a REST API: HTTP methods, status codes, headers and token authentication
- Validation of the response body: values, data types and response time
- An end-to-end flow at API level, with data passed between requests using variables
- Negative tests based on risk: invalid credentials, missing data, invalid dates, actions without permission
- Continuous integration: the collection runs on every push and creates an HTML report

## Contents

| File | Description |
| --- | --- |
| [TEST_PLAN.md](TEST_PLAN.md) | Scope, approach, risks and criteria |
| [TEST_CASES.md](TEST_CASES.md) | 14 test cases with expected and actual results |
| [collection/](collection) | Postman collection and environment |
| [.github/workflows/api-tests.yml](.github/workflows/api-tests.yml) | GitHub Actions pipeline |
| [bugs/](bugs) | Bug reports for the defects found |
| [images/](images) | Screenshots of key results |

## Test coverage

| Folder | Cases | Description |
| --- | --- | --- |
| 01 - Health check | 1 | The API is available |
| 02 - Authentication | 2 | Login with valid and invalid credentials |
| 03 - Booking E2E flow | 6 | Create, get, update, partial update, delete and verify deletion |
| 04 - Negative tests | 5 | Invalid data and actions without token |

## How to run

**In Postman**

1. Import the two files from the `collection` folder.
2. Select the environment **Restful-Booker**.
3. Open the collection and click **Run**.

## Results

**Execution: 2026-10-27 – 14 test cases – 11 passed, 3 failed.**

| Bug | Title | Severity |
| --- | --- | --- |
| [BUG-01](bugs/BUG-01.md) | Login with invalid credentials returns 200 instead of 401 | Minor |
| [BUG-02](bugs/BUG-02.md) | Missing required field returns 500 instead of 400 | Major |
| [BUG-03](bugs/BUG-03.md) | Booking created with checkout before checkin | Major |

## Why Newman

The same requests could be sent with tools like cURL, but cURL only sends requests: it does not check the responses, share variables between requests or create reports. Newman runs the Postman collection exactly as it is, including all assertions and the E2E flow, so the tests I design in Postman are the same tests that run in the CI pipeline on every push. It also generates an HTML report that is stored as an artifact of each run.

## Author

Richard Tripodi – Manual QA | Functional Analyst | richardtripodi15@gmail.com
