# Overview

- Build an image from docker file
- (Optionally) Runs Healthcheck
- Pushes to ECR

## Configuration

Input             | Default      | Description
----------------- | ------------ | ----------------------------------------------------------------------------------------
access_key_id     | **REQUIRED** | An AWS Access Key ID
secret_access_key | **REQUIRED** | An AWS Secret Access Key
ecr_uri           | **REQUIRED** | The URI of the ECR repository to push to
build_only        | `false`      | Will skip pushing to ECR
env_file          | `""`         | File containing environment variables required for app to run and pass healthcheck
healthcheck       | `/health`    | The path to a healthcheck that will be pulsed and requires passing before pushing to ECR
port              | `3000`       | The port the server listens on

## Example Usage

### Build and Push

```yml
name: Build Image and Push to ECR
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-20.04
    steps:
    - uses: actions/checkout@main
    - uses: bhudgens/build-and-deploy-to-ecr@main
      with:
        ecr_uri: ${{secrets.ECR_URI}}
        access_key_id: ${{secrets.ECR_AWS_ACCESS_KEY_ID}}
        secret_access_key: ${{secrets.ECR_AWS_SECRET_ACCESS_KEY}}
```

### Build Only

```yml
name: Build Image and Do Not Push to ECR
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-20.04
    steps:
    - uses: actions/checkout@main
    - uses: bhudgens/build-and-deploy-to-ecr@main
      with:
        ecr_uri: ${{secrets.ECR_URI}}
        access_key_id: ${{secrets.ECR_AWS_ACCESS_KEY_ID}}
        secret_access_key: ${{secrets.ECR_AWS_SECRET_ACCESS_KEY}}
        build_only: true
```
