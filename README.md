# FastAPI Beyond CRUD 

This is the source code for the [FastAPI Beyond CRUD](https://youtube.com/playlist?list=PLEt8Tae2spYnHy378vMlPH--87cfeh33P&si=rl-08ktaRjcm2aIQ) course. The course focuses on FastAPI development concepts that go beyond the basic CRUD operations.

For more details, visit the project's [website](https://jod35.github.io/fastapi-beyond-crud-docs/site/).


## Getting Started
Follow the instructions below to set up and run your FastAPI project.

### Prerequisites
Ensure you have the following installed:

- Python >= 3.10
- PostgreSQL
- Redis


You can run the application using Docker:
```bash
docker compose up -d
```
## Running Tests
Run the tests using this command
```bash
pytest
```


## Environment Variables
Copy `.env.example` to `.env` and fill in the following values:
- `DATABASE_URL` - PostgreSQL connection string
- `JWT_SECRET` and `JWT_ALGORITHM` - JWT configuration
- `MAIL_SERVER`, `MAIL_PORT`, `MAIL_USERNAME`, `MAIL_PASSWORD`, `MAIL_FROM`, `MAIL_FROM_NAME` - SMTP email configuration (use Ethereal for testing)
- `REDIS_URL` - Redis connection string
- `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB` - PostgreSQL credentials
- `DOMAIN` - Application domain (use `localhost` for local development)

## GitHub Secrets Required
Add the following secrets to your GitHub repository settings:
- `DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN` - DockerHub credentials
- `MAIL_SERVER`, `MAIL_PORT`, `MAIL_USERNAME`, `MAIL_PASSWORD` - SMTP credentials
- `MAIL_FROM`, `MAIL_FROM_NAME` - Email sender details
- `DATABASE_URL`, `JWT_SECRET`, `JWT_ALGORITHM` - App configuration
- `DOMAIN` - Application domain
- `NOTIFY_EMAIL` - Email address to receive failure notifications
- `EMAIL_SUBJECT`, `EMAIL_BODY` - Failure notification email content

## Things that I've updated
- Changed the command to run the container in Dockerfile. Instead of using `fastapi` I'm using `uvicorn` to start the application. The FastAPI CLI wrapper around uvicorn was broken in the installed version, so it was replaced with uvicorn directly.

- Added two workflow files — `nightly-build` and `conventional-commit-checker`:
  - **Nightly Build**: Triggered every day at 12:00 AM UTC. Runs tests, builds a Docker image, and pushes it to DockerHub. If the build or tests fail, an email notification is sent.
  - **Conventional Commit Checker**: Checks whether each commit in a PR follows the Conventional Commits specification. If commits are invalid, the PR is automatically closed and the user receives an email notification. This workflow is triggered when a PR is opened or synchronized.

- Added required secrets in GitHub repository settings for DockerHub, email, and application configuration.

