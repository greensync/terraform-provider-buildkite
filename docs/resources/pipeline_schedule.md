# Resource: pipeline_schedule

This resource allows you to create and manage pipeline schedules.

Buildkite Documentation: https://buildkite.com/docs/pipelines/scheduled-builds

## Example Usage

```hcl
resource "buildkite_pipeline_schedule" "repo2_nightly" {
  pipeline_id = buildkite_pipeline.repo2.id
  label       = "Nightly build"
  cronline    = "@midnight"
  branch      = buildkite_pipeline.repo2.default_branch
}
```

## Argument Reference

* `pipeline_id` - (Required) Terraform resource ID of a buildkite pipeline (Buildkite GraphQL ID).
* `label` - (Required) Schedule label.
* `cronline` - (Required) Schedule interval (see [docs](https://buildkite.com/docs/pipelines/scheduled-builds#schedule-intervals)).
* `branch` - (Required) The branch to use for the build.
* `commit` - (Optional, Default: `HEAD`) The commit ref to use for the build.
* `message` - (Optional, Default: `Scheduled build`) The message to use for the build.
* `env` - (Optional) A map of environment variables to use for the build.
* `enabled` - (Optional, Default: `true`) Whether the schedule should run.

## Import

Pipeline schedules can be imported using a slug (which consists of `$BUILDKITE_ORGANIZATION_SLUG/$BUILDKITE_PIPELINE_SLUG/$PIPELINE_SCHEDULE_UUID`), e.g.

```
$ terraform import buildkite_pipeline_schedule.test myorg/test/1be3e7c7-1e03-4011-accf-b2d8eec90222
```
