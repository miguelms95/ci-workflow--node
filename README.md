# Ci Workflow Node

Build and deploy node project to SFTP (optionally).

![](https://github.com/miguelms95/ci-workflow--node/actions/workflows/test.yml/badge.svg)

## Inputs

The workflow accepts the following inputs:

* **`node_version` (Optional, String, Default: `'20'`):** The Node.js version to use for the build process.
* **`build_script` (Optional, String, Default: `'npm run build'`):** The command to execute for building the application.
* **`source_path` (Optional, String, Default: `'dist/*'`):** The path to the files to upload to the SFTP server.
* **`target_path` (Optional, String):** The target directory on the SFTP server.
* **`deploy_sftp` (Optional, Boolean, Default: `false`):** A flag to enable or disable SFTP deployment.
* **`sftp_host` (Optional, String):** The SFTP server hostname or IP address.
* **`sftp_user` (Optional, String):** The SFTP username.
* **`sftp_pass` (Optional, String):** The SFTP password.

## Jobs

* **`deploy`:** This job performs the following steps:
  * Checks out the repository.
  * Sets up the specified Node.js version.
  * Installs dependencies using `npm ci`.
  * Builds the application using the provided `build_script`.
  * Conditionally uploads the build artifacts to the SFTP server if `deploy_sftp` is `true`.

## Usage

To use this workflow template, create a workflow file in your repository that calls this reusable workflow.

Usage in your repo:

```yml
name: Node build

on:
  push:
    branches: [main]

jobs:
  deploy-to-sftp:
    uses: miguelms95/ci-workflow--node/.github/workflows/ci-node-deploy.yml@main
    with:
      node_version: '20'
      deploy_sftp: false
```

with deploy:
```yml
name: Node build & Deploy via SFTP

on:
  push:
    branches: [main]

jobs:
  deploy-to-sftp:
    uses: miguelms95/ci-workflow--node/.github/workflows/ci-node-deploy.yml@main
    with:
      node_version: '20'
      target_path: "my-app"
      deploy_sftp: true
    secrets:
      sftp_host: ${{ secrets.SFTP_HOST }}
      sftp_user: ${{ secrets.SFTP_USER }}
      sftp_pass: ${{ secrets.SFTP_PASS }}
```