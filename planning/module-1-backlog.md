# Module 1: Customer Accounts product backlog and sprint plan

Repository: https://github.com/KaustubhMukdam/devops-capstone-project

This is the broader capstone roadmap based on the overview and starter code. The later-provided Module 1 lab handout requires an initial **seven-story board**, so only CA-01 through CA-05, CA-10, and CA-13 are active on the Module 1 board. The other issues remain in GitHub for later modules and are archived from the active board view. See [module-1-lab.md](module-1-lab.md) for the lab-specific plan and evidence stages. The starter service already implements `POST /accounts` and the Account model; the four missing REST operations are read, update, delete, and list.

## Board and sprint setup

- GitHub Project: **[Customer Accounts Capstone](https://github.com/users/KaustubhMukdam/projects/3)**, public and linked to the repository. It reuses the existing capstone Project instead of adding another board.
- Existing board status choices: **New Issues**, **Icebox**, **Product Backlog**, **Sprint Backlog**, **In Progress**, **Review/QA**, **Done**. The seven lab stories are being moved through the PDF's evidence stages. Close each GitHub issue when its work is complete; the lab's instruction to close stories merely when sprint planning is finished would otherwise misstate implementation progress.
- The board now has three one-week **Iteration** values starting 2026-10-27, 2026-11-03, and 2026-11-10. A separate Sprint select field remains from the broader roadmap.
- Existing **Estimate** number field stores story points. The broader-roadmap estimates below were made before the detailed PDF was supplied; the lab's Sprint 1 estimates use its 3/5/8/13 scale.
- Labels: `user story`, `sprint:1`, `sprint:2`, `sprint:3`, `api`, `ci`, `security`, `deployment`, `cd`. GitHub Project fields are the source of truth for sprint and points.

| ID | Issue title | Sprint | Points | Depends on |
|---|---|---:|---:|---|
| CA-01 | [Set up the development environment and Sprint 1 branch](https://github.com/KaustubhMukdam/devops-capstone-project/issues/1) | 1 | 2 | — |
| CA-02 | [Read a customer account by ID](https://github.com/KaustubhMukdam/devops-capstone-project/issues/3) | 1 | 3 | CA-01 |
| CA-03 | [Update a customer account](https://github.com/KaustubhMukdam/devops-capstone-project/issues/4) | 1 | 3 | CA-02 |
| CA-04 | [Delete a customer account](https://github.com/KaustubhMukdam/devops-capstone-project/issues/5) | 1 | 3 | CA-02 |
| CA-05 | [List and filter customer accounts](https://github.com/KaustubhMukdam/devops-capstone-project/issues/6) | 1 | 3 | CA-01 |
| CA-06 | [Verify Sprint 1 tests and at least 95% coverage](https://github.com/KaustubhMukdam/devops-capstone-project/issues/7) | 1 | 2 | CA-02–05 |
| CA-07 | [Run lint, tests, and coverage in GitHub Actions](https://github.com/KaustubhMukdam/devops-capstone-project/issues/8) | 2 | 5 | CA-06 |
| CA-08 | [Add secure response headers with Flask-Talisman](https://github.com/KaustubhMukdam/devops-capstone-project/issues/9) | 2 | 3 | CA-07 |
| CA-09 | [Configure cross-origin access with Flask-CORS](https://github.com/KaustubhMukdam/devops-capstone-project/issues/10) | 2 | 3 | CA-07 |
| CA-10 | [Package the service in a Docker image](https://github.com/KaustubhMukdam/devops-capstone-project/issues/11) | 3 | 3 | CA-09 |
| CA-11 | [Publish the image to IBM Cloud Container Registry](https://github.com/KaustubhMukdam/devops-capstone-project/issues/12) | 3 | 2 | CA-10 |
| CA-12 | [Provision PostgreSQL in OpenShift](https://github.com/KaustubhMukdam/devops-capstone-project/issues/13) | 3 | 3 | — |
| CA-13 | [Deploy and expose the service on Kubernetes](https://github.com/KaustubhMukdam/devops-capstone-project/issues/14) | 3 | 5 | CA-11, CA-12 |
| CA-14 | [Automate lint, test, build, and deploy with Tekton](https://github.com/KaustubhMukdam/devops-capstone-project/issues/15) | 3 | 5 | CA-13 |

The table below records the original 14-story roadmap, not the seven active lab cards or their final lab estimates. Its future-work estimates can change as implementation reveals work.

## Issue bodies

Each section below is the published GitHub issue body with the matching title. The acceptance criteria describe observable results; screenshots, CI logs, or cluster outputs should be recorded in the evidence index when a story is completed.

### CA-01 — Set up the development environment and Sprint 1 branch

**As a** developer<br>
**I need** a working service environment and a dedicated development branch<br>
**So that** I can implement Sprint 1 using TDD without changing `main` directly.

**Details and Assumptions:** Use the starter repository and its documented dependencies. Use a PostgreSQL test database where required. Do not count an unrun setup command as completion.

**Sprint and Estimate:** Sprint 1; 2 points.

**Acceptance Criteria:** Given a clean checkout, when setup completes, then dependencies install and the existing test command runs. Given Sprint 1 work begins, when code is changed, then commits are made on a development branch and submitted through a pull request.

### CA-02 — Read a customer account by ID

**As an** API consumer<br>
**I need** to retrieve one account by ID<br>
**So that** I can see its current details.

**Details and Assumptions:** Add `GET /accounts/<id>` to the Flask service. Use the existing Account serialization format. Update the `Location` header in the create route to point to the new read URL.

**Sprint and Estimate:** Sprint 1; 3 points.

**Acceptance Criteria:** Given an existing account, when its ID is requested, then the API returns HTTP 200 and its serialized fields. Given an unknown ID, when it is requested, then the API returns HTTP 404. Given a successful create, when the `Location` header is followed, then it resolves to the created account. Write failing tests before implementation.

### CA-03 — Update a customer account

**As an** API consumer<br>
**I need** to update an existing account<br>
**So that** changed customer details are stored.

**Details and Assumptions:** Add `PUT /accounts/<id>` and reuse model deserialization and content-type validation.

**Sprint and Estimate:** Sprint 1; 3 points.

**Acceptance Criteria:** Given an existing account and a valid JSON representation, when it is updated, then the API returns the updated representation and a later read shows the saved values. Given an unknown ID, then the API returns HTTP 404. Given an unsupported content type or invalid body, then the request is rejected consistently with the service's error handling. Write failing tests before implementation.

### CA-04 — Delete a customer account

**As an** API consumer<br>
**I need** to delete an account<br>
**So that** obsolete customer records are removed.

**Details and Assumptions:** Add `DELETE /accounts/<id>` using the existing model delete method.

**Sprint and Estimate:** Sprint 1; 3 points.

**Acceptance Criteria:** Given an existing account, when it is deleted, then the API returns HTTP 204 and a later read returns HTTP 404. Given an unknown ID, when deletion is requested, then the API returns HTTP 204 without creating or changing a record. Write failing tests before implementation.

### CA-05 — List and filter customer accounts

**As an** API consumer<br>
**I need** to list accounts and optionally filter by name<br>
**So that** I can find matching customer records.

**Details and Assumptions:** Add `GET /accounts`. The model already offers `all()` and `find_by_name()`.

**Sprint and Estimate:** Sprint 1; 3 points.

**Acceptance Criteria:** Given accounts exist, when the collection is requested, then the API returns HTTP 200 and a JSON list. Given no accounts, then it returns an empty list. Given a `name` query parameter, then only exact name matches are returned. Write failing tests before implementation.

### CA-06 — Verify Sprint 1 tests and at least 95% coverage

**As a** maintainer<br>
**I need** the API test suite and coverage gate to pass<br>
**So that** changes to account behavior are detected early.

**Details and Assumptions:** Include success and relevant error paths for read, update, delete, and list. The course overview specifies `nosetests` and at least 95% coverage.

**Sprint and Estimate:** Sprint 1; 2 points.

**Acceptance Criteria:** Given Sprint 1 code, when the test suite runs, then all tests pass. When coverage is measured with the repository configuration, then total coverage is at least 95%, and the command output is saved as evidence. Sprint 1 changes are reviewed and merged into `main`.

### CA-07 — Run lint, tests, and coverage in GitHub Actions

**As a** maintainer<br>
**I need** CI on pushes and pull requests to `main`<br>
**So that** code quality is checked before delivery.

**Details and Assumptions:** Use Flake8, the project's test command, and a 95% coverage threshold.

**Sprint and Estimate:** Sprint 2; 5 points.

**Acceptance Criteria:** Given a push to `main` or pull request targeting `main`, when GitHub Actions runs, then lint, tests, and coverage checks execute automatically. Given a lint, test, or coverage failure, then the workflow fails. A successful workflow run URL is saved as evidence.

### CA-08 — Add secure response headers with Flask-Talisman

**As a** security-conscious API consumer<br>
**I need** appropriate response security headers<br>
**So that** common browser-side risks are reduced.

**Details and Assumptions:** Add Flask-Talisman without breaking local tests or the cluster's TLS setup. Avoid enabling forced HTTPS until the deployment path is understood.

**Sprint and Estimate:** Sprint 2; 3 points.

**Acceptance Criteria:** Given a service response, when it is inspected, then the configured Talisman headers are present. Given the test environment, when the security tests run, then they pass without unintended redirects. Tests fail before the feature is added and pass afterward.

### CA-09 — Configure cross-origin access with Flask-CORS

**As a** browser client<br>
**I need** a defined cross-origin policy for the API<br>
**So that** permitted front ends can call it.

**Details and Assumptions:** Configure allowed origins and methods deliberately; do not assume all origins are acceptable in production.

**Sprint and Estimate:** Sprint 2; 3 points.

**Acceptance Criteria:** Given an allowed origin, when a CORS request or preflight is sent, then the expected CORS headers and methods are returned. Given a disallowed origin, then access is not granted by CORS headers. Tests fail before configuration and pass afterward. Sprint 2 changes are merged into `main`.

### CA-10 — Package the service in a Docker image

**As an** operator<br>
**I need** a reproducible Docker image<br>
**So that** the service can run in a container platform.

**Details and Assumptions:** Create a Dockerfile and include only required runtime files. Expose the application port used by the service.

**Sprint and Estimate:** Sprint 3; 3 points.

**Acceptance Criteria:** Given the repository, when the Docker image is built, then the build succeeds. When the image is run with required configuration, then `/health` responds successfully. Record build output and image tag as evidence.

### CA-11 — Publish the image to IBM Cloud Container Registry

**As an** operator<br>
**I need** the built image in IBM Cloud Container Registry<br>
**So that** OpenShift can pull the release artifact.

**Details and Assumptions:** Registry namespace, region, and access depend on the course lab account. Keep credentials out of the repository.

**Sprint and Estimate:** Sprint 3; 2 points.

**Acceptance Criteria:** Given registry access, when the image is tagged and pushed, then the repository/tag is visible in IBM Cloud Container Registry. Save the image reference and redacted push/list output as evidence.

### CA-12 — Provision PostgreSQL in OpenShift

**As an** operator<br>
**I need** a PostgreSQL service in the cluster<br>
**So that** account data persists outside the app container.

**Details and Assumptions:** Use the lab-provided OpenShift namespace and storage options. Store database credentials in a Kubernetes Secret or equivalent cluster mechanism.

**Sprint and Estimate:** Sprint 3; 3 points.

**Acceptance Criteria:** Given cluster access, when PostgreSQL is deployed, then the service and pod become ready. The application can connect using cluster configuration, and credentials do not appear in committed manifests. Save readiness output as evidence.

### CA-13 — Deploy and expose the service on Kubernetes

**As an** operator<br>
**I need** deployment and service manifests<br>
**So that** the containerized API runs and can be reached in OpenShift.

**Details and Assumptions:** Add deployment and service YAML; use the registry image and PostgreSQL configuration. Expose a route if required by the lab.

**Sprint and Estimate:** Sprint 3; 5 points.

**Acceptance Criteria:** Given the pushed image and ready PostgreSQL service, when manifests are applied, then the app pod becomes ready and `/health` succeeds through the exposed service/route. A create followed by read works against the deployed API. Save manifest paths, cluster output, and endpoint evidence.

### CA-14 — Automate lint, test, build, and deploy with Tekton

**As an** operator<br>
**I need** a Tekton CD pipeline<br>
**So that** a trigger deploys a verified version without manual build and apply steps.

**Details and Assumptions:** Complete the starter `tekton/` pipeline and tasks. Supply registry and cluster access through lab-supported credentials and service accounts.

**Sprint and Estimate:** Sprint 3; 5 points.

**Acceptance Criteria:** Given a configured trigger, when the pipeline runs, then it clones the repository, passes Flake8 and tests, builds and pushes the image, and deploys the update. Given a failed quality check, then deployment does not proceed. Save the PipelineRun, task statuses, image reference, and updated deployment output as evidence.
