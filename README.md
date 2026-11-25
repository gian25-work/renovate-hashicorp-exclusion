# Terraform constraint with `!=` makes Renovate skip the dependency

Discussion: <DISCUSSION-URL>

## Current behavior

Renovate skips `hashicorp/aws` in `with-exclusion/main.tf` with `skipReason: invalid-value` and logs `WARN: Unsupported hashicorp constraint`. No update is proposed, including the `6.x` major.

The same provider in `without-exclusion/main.tf` gets a major update to `~> 6.0`.

## Expected behavior

`!=` is a valid Terraform version constraint operator ([docs](https://developer.hashicorp.com/terraform/language/expressions/version-constraints#-1)). Renovate should treat `with-exclusion/main.tf` like `without-exclusion/main.tf` and propose the `6.x` major update.

## Files

| Path | Constraint |
|---|---|
| `with-exclusion/main.tf` | `~> 5.0, != 5.71.0` |
| `without-exclusion/main.tf` | `~> 5.0` |
