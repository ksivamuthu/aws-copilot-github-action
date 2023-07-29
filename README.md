# AWS Copilot GitHub Action

This repo contains the github actions for installing [AWS Copilot cli](https://github.com/aws/copilot-cli) and deploying app. The AWS Copilot CLI is a tool for developers to build, release and operate production ready containerized applications on AWS App Runner, Amazon ECS, and AWS Fargate.

## Usage

1. To install copilot-cli in your github actions.

```
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          role-to-assume: arn:aws:iam::111111111111:role/my-github-actions-role-test
          aws-region: us-east-1
      - uses: ksivamuthu/aws-copilot-github-action@v0.0.1
        with:
          command: install
      - run: |
          copilot --version
```

2. To deploy the app

```
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          role-to-assume: arn:aws:iam::111111111111:role/my-github-actions-role-test
          aws-region: us-east-1
      - uses: ksivamuthu/aws-copilot-github-action@v0.0.1
        with:
          command: deploy
          app: your-awesome-app
          env: prod
          force: false # optional
```


## Optional parameters

### Name

In the with attribute, the name value can be used to define the name of the job to be published

```
  deploy:
    steps:
      - uses: ksivamuthu/aws-copilot-github-action@v0.0.5
        with:
          command: deploy
          app: your-awesome-app
          env: prod
          name: job-name
```

### Tag

In the with attribute, the tag value can be used to define the tag image name

```
  deploy:
    steps:
      - uses: ksivamuthu/aws-copilot-github-action@v0.0.5
        with:
          command: deploy
          app: your-awesome-app
          env: prod
          tag: image-name
```