# Restful-Booker – API Testing (Postman + Newman + GitHub Actions)

![API Tests](https://github.com/richardtripodi15-cmyk/booker-api-testing/actions/workflows/api-tests.yml/badge.svg)

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

**With Newman (command line)**

```bash
npm install -g newman newman-reporter-htmlextra
newman run collection/restful-booker.postman_collection.json \
  -e collection/restful-booker.postman_environment.json \
  -r cli,htmlextra --reporter-htmlextra-export reports/api-test-report.html
```

**In GitHub Actions**

The pipeline runs on every push to `main`. The HTML report is available in the **Artifacts** section of each run.

## Results

_To be completed after execution._

## Related projects

- [Manual testing on ParaBank](https://github.com/richardtripodi15-cmyk/manual_test_case)
- E2E automation with Playwright + Python (in progress)

## Author

Richard Tripodi – Manual QA | Functional Analyst | richardtripodi15@gmail.com
