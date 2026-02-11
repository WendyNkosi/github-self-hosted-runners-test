## github-self-hosted-runners

This project demonstrates a test implementation of GitHub self-hosted runners using Docker containers. It allows you to spin up runners locally via Docker Desktop and run GitHub Actions workflow jobs on them.

## Features

- Runs GitHub Actions jobs in Docker containers.

- Easy to configure using environment variables.

- Supports repository-scoped or organization-scoped runners.

- Built with Docker Compose for easy setup.

- Requirements

- Docker Desktop

- Docker Compose

- A GitHub personal access token (repo or organization scoped) with **repo** or **admin:org** permissions depending on your setup.

## Setup

- Clone the repository:

```git clone <this-repo-url>```<br>
```cd github-self-hosted-runners-test```<br>


- Build the runner image:<br>

```docker-compose run -e GITHUB_PERSONAL_TOKEN=<your-token> -e GITHUB_ORG=<your-org-or-username> -e GITHUB_REPOSITORY=<your-repo-name> gha_runner``` <br>

**Note: If you want to run an organization-wide runner, omit GITHUB_REPOSITORY and provide GITHUB_ORG.**

## Scaling Runners

You can run multiple self-hosted runners by increasing the service count in docker-compose.yml:

```docker-compose up --scale gha_runner=3```

## Stopping and Cleaning Up

- To stop the runner containers:

```docker-compose down```


- To remove all containers, volumes, and networks created by Docker Compose:

```docker-compose down -v```

## Usage Example

Once the runner is up and connected, you can trigger a GitHub Actions workflow that targets self-hosted runners. Here's an example workflow you could add to .github/workflows/test.yml:

```name: Test Self-Hosted Runner

on:
  workflow_dispatch:

jobs:
  build:
    runs-on: self-hosted   # This ensures the job runs on your self-hosted runner
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Run a test script
        run: echo "Hello from the self-hosted runner!"

