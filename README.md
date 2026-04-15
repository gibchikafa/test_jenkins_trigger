# test_jenkins_trigger

Minimal Jenkins test repository for triggering the `k8s-dlt` Jenkins job.

## Behavior

- Does not build any Docker image itself.
- Runs a dummy upstream stage.
- Triggers `k8s-dlt` by default and waits for it to finish.
- Can trigger a branch-qualified downstream job if you set `DLT_JOB_BRANCH`.
- Passes `BASE_IMAGE` to the downstream build.

## Jenkins variables

- `DLT_JOB_NAME`
  - Defaults to `k8s-dlt`
- `DLT_JOB_BRANCH`
  - Optional
  - If set, the pipeline triggers `${DLT_JOB_NAME}/${DLT_JOB_BRANCH}`
- `BASE_IMAGE`
  - Defaults to `docker.hops.works/hopsworks/hopsworks-base:pandas-training-pipeline-test`

## Example

With default settings, it triggers:

`k8s-dlt`

If you set `DLT_JOB_BRANCH=feature-x`, it triggers:

`k8s-dlt/feature-x`
