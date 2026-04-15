# test_jenkins_trigger

Minimal Jenkins test repository for triggering the `k8s-dlt` Jenkins job.

## Behavior

- Does not build any Docker image itself.
- Runs a dummy upstream stage.
- Triggers plain `k8s-dlt` without waiting for it to finish.
- Passes `DLT_GIT_BRANCH`, `DLT_IMAGE_VERSION`, and `BASE_IMAGE_VERSION` to the downstream build.

## Jenkins variables

- `DLT_JOB_NAME`
  - Defaults to `k8s-dlt`
- `DLT_GIT_BRANCH`
  - Defaults to `BRANCH_NAME`
- `DLT_IMAGE_VERSION`
  - Defaults to `test`
- `BASE_IMAGE_VERSION`
  - Defaults to `DLT_IMAGE_VERSION`

## Example

If this job runs with `BRANCH_NAME=branch-4.8`, it triggers:

`k8s-dlt`

and passes:

`DLT_GIT_BRANCH=branch-4.8`
