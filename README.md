# C# app using a Devcontainer

Demonstrates running a .NET C# API server leveraging docker-compose and devcontainers for full stack local development workflow.

Requires:

- VSCode
- VSCode Dev Container Extension

Running:

- Clone repo
- Open in vscode
- Choose "Reopen in Container" when prompted
- Open terminal
- cd backend
- dotnet ef database update
- dotnet watch
- Open https://localhost:8080/ in a browser

## Notes

`.devcontainer/devcontainer.json` is the devcontainer configuration, read by VSCode or anything else supporting the devcontainer spec. In this repo, it's expecting you to be using VSCode.

`backend/` is where the C# app source lives. It could also be at the root. It's placed here in this example to hint on how a monorepo with a separate frontend might be structured. This subproject owns its own `Dockerfile`. This also means the whole project root is mounted in the backend container. The alternative is to only mount `backend/`

`docker-compose.yml` is at the root as it is intended to tie together the entire dev workflow, which is mostly there to support `backend/` but could include other things in a larger project.

