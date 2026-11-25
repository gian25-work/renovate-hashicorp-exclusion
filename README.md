# Terraform constraint with `!=` makes Renovate skip the dependency

Discussion: <DISCUSSION-URL>

## Current behavior

Renovate skips `hashicorp/aws` in every `*-with-exclusion/main.tf` with `skipReason: invalid-value` and logs `WARN: Unsupported hashicorp constraint`. No update is proposed, including the `6.x` major.

The same provider in each `*-without-exclusion/main.tf` gets the `6.x` major update.

## Expected behavior

`!=` is a valid Terraform version constraint operator ([docs](https://developer.hashicorp.com/terraform/language/expressions/version-constraints#-1)). Renovate should treat each `*-with-exclusion/main.tf` like its `*-without-exclusion/main.tf` control and propose the `6.x` major update.

## Files

| Path | Constraint |
|---|---|
| `tilde-with-exclusion/main.tf` | `~> 5.0, != 5.71.0` |
| `tilde-without-exclusion/main.tf` | `~> 5.0` |
| `range-with-exclusion/main.tf` | `>= 5.0, < 6.0, != 5.71.0` |
| `range-without-exclusion/main.tf` | `>= 5.0, < 6.0` |
