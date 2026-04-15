# test_jenkins_trigger

Minimal Jenkins test repository for triggering the `hopsworks-dlt` Jenkins job.

## Behavior

- Does not build any Docker image itself.
- Runs a dummy upstream stage.
- Triggers `hopsworks-dlt/<branch>` and waits for it to finish.
- Maps `main` to downstream branch `master`.
- Passes `BASE_IMAGE` to the downstream build.

## Jenkins variables

- `DLT_JOB_NAME`
  - Defaults to `hopsworks-dlt`
- `BASE_IMAGE`
  - Defaults to `docker.hops.works/hopsworks/hopsworks-base:pandas-training-pipeline-test`

## Example

If this job runs on branch `main`, it triggers:

`hopsworks-dlt/master`

If this job runs on branch `feature-x`, it triggers:

`hopsworks-dlt/feature-x`
