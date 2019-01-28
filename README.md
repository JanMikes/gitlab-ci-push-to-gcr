# Push to Google Cloud Registry via Gitlab CI

## Environment variables:
  - GOOGLE_CLOUD_ACCOUNT
  - GITLAB_IMAGE
  - GCR_IMAGE

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