# Push to Google Cloud Registry via Gitlab CI

This repository is to demonstrate workflow:
- Build docker image in CI
- Push it to Gitlab Registry (so we can run tests on it etc)
- If everything is ok then push it to Google Cloud Registry (GCR) so we can use it in Google Cloud etc for Kubernetes


## Environment variables:
  - `GOOGLE_CLOUD_ACCOUNT` - google cloud service account credentials (see below how to get it)
  - `GITLAB_IMAGE` - where we push go Gitlab Registry
  - `GCR_IMAGE` - where we push to Google Cloud Registry

Images variables can be set in Gitlab's settings or in your `.gitlab-ci.yml` file:
```yaml
variables:
  GITLAB_IMAGE: registry.gitlab.com/author-name/my-project
  GCR_IMAGE: eu.gcr.io/my-project/image-name
```

I recommend setting `GOOGLE_CLOUD_ACCOUNT` via protected variables **Settings -> CI/CD -> Environment variables**


## How do I get `GOOGLE_CLOUD_ACCOUNT` variable content?

1. Go to your Google Cloud account
2. Pick a project
3. Create service account with [Storage admin](https://cloud.google.com/container-registry/docs/access-control) role (**IAM & Admin -> Service accounts -> Create service account**)
4. Copy the json key and enter it to gitlab

#### Notes

- If you run into `Error: Cannot perform an interactive login from a non TTY device`, it is because you have mismatch of protected variable and branch (both must have the same state - either protected or unprotected). https://gitlab.com/gitlab-com/support-forum/issues/3524#note_150577883
