# Ci Workflow Node

Build and deploy node project to SFTP (optionally).

Usage in your repo:

```yml
# .github/workflows/deploy-project.yml

name: Deploy Project via SFTP

on:
  push:
    branches: [main]

jobs:
  deploy-to-sftp:
    uses: miguelms95/ci-workflow--node/.github/workflows/ci-node-deploy.yml@main
    secrets:
      sftp_host: ${{ secrets.SFTP_HOST }}
      sftp_user: ${{ secrets.SFTP_USER }}
      sftp_pass: ${{ secrets.SFTP_PASS }}
    with:
      target_path: "my-folder-name"
      deploy_sftp: true
```