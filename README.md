# github-self-hosted-runners-test
This is a test implementation for github self-hosted runners using Docker containers.

# Requirements
 - Docker Desktop
 - docker compose
 - A github personal access token (repo or organization scoped)

# Running the runners

`docker-compose build gha_runner`

`GITHUB_PERSONAL_TOKEN=<repo scoped token> GITHUB_ORG=<github usrname or github org> GITHUB_REPOSITORY=<The repository> docker-compose up`

