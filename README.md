# DevOps Capstone Project - Customer Accounts microservice

[![Build Status](https://github.com/Avdhut-Dani/devops-capstone-project/actions/workflows/ci-build.yaml/badge.svg)](https://github.com/Avdhut-Dani/devops-capstone-project/actions/workflows/ci-build.yaml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python 3.9](https://img.shields.io/badge/Python-3.9-green.svg)](https://shields.io/)

## Project Overview

The DevOps Capstone Project focuses on developing and managing a RESTful Customer Accounts microservice for an e-commerce application using Python and Flask.

The service supports creating, retrieving, updating, deleting, and listing customer accounts. The project covers Agile planning using GitHub Projects/ZenHub, automated testing with nosetests and 95%+ coverage, continuous integration workflows using GitHub Actions, security enforcement with Flask-Talisman and Flask-CORS, containerization with Docker, and automated deployment with Tekton CI/CD pipelines to Kubernetes/OpenShift.

## Objectives

- Plan development using Agile user stories, estimates, and sprints on Kanban boards.
- Implement RESTful APIs for customer account management (Create, Read, Update, Delete, List).
- Enforce strict test-driven development (TDD) and security practices (CORS and Talisman headers).
- Automate Continuous Integration checks with GitHub Actions.
- Containerize the microservice using Docker.
- Automate Continuous Deployment (CD) using Tekton pipelines to OpenShift/Kubernetes.

## Development Environment

These labs are designed to be executed in the IBM Developer Skills Network Cloud IDE with OpenShift.

Once you are in the lab environment, initialize it with:
```bash
source bin/setup.sh
```

## REST API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Root URL health and service metadata |
| GET | `/health` | Service health status |
| POST | `/accounts` | Create a new customer account |
| GET | `/accounts` | List all customer accounts |
| GET | `/accounts/<id>` | Read a specific customer account |
| PUT | `/accounts/<id>` | Update an existing customer account |
| DELETE | `/accounts/<id>` | Delete an account |

## Project layout

```text
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── user-story.md
│   └── workflows/
│       └── ci-build.yaml
├── deploy/
│   ├── deployment.yaml
│   └── service.yaml
├── service/
│   ├── common/
│   ├── config.py
│   ├── models.py
│   └── routes.py
├── tekton/
│   ├── pipeline.yaml
│   ├── pvc.yaml
│   └── tasks.yaml
├── tests/
│   ├── factories.py
│   ├── test_cli_commands.py
│   ├── test_models.py
│   └── test_routes.py
├── Dockerfile
├── Makefile
├── Procfile
├── README.md
├── requirements.txt
└── setup.cfg
```

## Running Tests

Run unit tests and coverage report:
```bash
nosetests -v --with-spec --spec-color
```

## Author

**Sarthak Pawar** ([SARTH9191](https://github.com/SARTH9191))

## License

Licensed under the Apache License 2.0. See [LICENSE](LICENSE) for details.
