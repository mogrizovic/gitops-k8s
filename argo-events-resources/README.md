# Argo Workflows CICD setup

General Workflow Templates are created for few jobs:
- `_wf-tmpl-build-image-multiplatform.yaml` Build multiplatform image and push them, along with the manifest, to ghe Docker registry
- `_wf-tmpl-commit-helm-image-tag.yaml` Commit docker image tag to helm values
- `_wf-tmpl-github-auth.yaml` Generates Github access token used for authentication via GH App

App specific Workflow Templates are created, that use general templates:
- `_app-wf-tmpl-spring-boot-example.yaml` spring-boot-example specific template. This template is Cluster scoped due to older setup - tech debt.

Two Workflow sensors are created that detect events on the Event Bus:
- `gh-pr-dynamic-workflow-sensor.yaml` Consumes pull_request webhook events and triggers app specific workflow, based on the event data (repo name), providing pr related parameters
- `gh-merge-dynamic-workflow-sensor.yaml` Consumes push events webhook events and triggers app specific workflow, based on the evnet data (repo name), providing merge related parameters

Github Webhook is created to send events for:
- pull_request (opened, edited, reopened, synchronize)
- push
