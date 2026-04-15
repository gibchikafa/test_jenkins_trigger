# test_jenkins_trigger

Minimal Jenkins test repository for triggering the `k8s-dlt` Jenkins job.

## Behavior

- Does not build any Docker image itself.
- Runs a dummy upstream stage.
- Triggers `k8s-dlt/${BRANCH_NAME}` by default without waiting for it to finish.
- `DLT_JOB_BRANCH` can override the downstream branch explicitly.
- Passes `DLT_IMAGE_VERSION` and `BASE_IMAGE_VERSION` to the downstream build.

## Jenkins variables

- `DLT_JOB_NAME`
  - Defaults to `k8s-dlt`
- `DLT_JOB_BRANCH`
  - Optional
  - Overrides the downstream branch name
- `DLT_IMAGE_VERSION`
  - Defaults to `test`
- `BASE_IMAGE_VERSION`
  - Defaults to `DLT_IMAGE_VERSION`

## Example

If this job runs with `BRANCH_NAME=branch-4.8`, it triggers:

`k8s-dlt/branch-4.8`

If you set `DLT_JOB_BRANCH=feature-x`, it triggers:

`k8s-dlt/feature-x`
