# Terraform constraint with `!=` makes Renovate skip the dependency

Discussion: <DISCUSSION-URL>

## Current behavior

Renovate 44.256.1 (`--platform=local`) gives these results for `hashicorp/aws`:

| Path | Constraint | Result |
|---|---|---|
| `tilde-with-exclusion/main.tf` | `~> 5.0, != 5.71.0` | `skipReason: invalid-value`, no updates |
| `tilde-without-exclusion/main.tf` | `~> 5.0` | major update to `6.74.0`, `newValue: ~> 6.0` |
| `range-with-exclusion/main.tf` | `>= 5.0, < 6.0, != 5.71.0` | `skipReason: invalid-value`, no updates |
| `range-without-exclusion/main.tf` | `>= 5.0, < 6.0` | major update to `6.74.0`, `newValue: < 6.75` |

For each constraint with `!=`, Renovate also logs `WARN: Unsupported hashicorp constraint`.

The `newValue: < 6.75` of the range control drops the lower bound. That is a separate, known problem: #17973.

## Expected behavior

`!=` is a valid Terraform version constraint operator ([docs](https://developer.hashicorp.com/terraform/language/expressions/version-constraints#-1)). A constraint with `!=` should get the same `6.x` major update as its control without `!=`, instead of being skipped.
