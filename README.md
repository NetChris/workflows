# Reusable GitHub workflows for NetChris

## `dotnet-build-test-pack-push-default.yml`

This is a simple build, test, pack and NuGet push for .NET projects.  "Default" in that it assumes the `dotnet` SDK commands `build`, `test`, `pack` and `nuget push` can be run and all required information is defaulted (e.g. solutions, projects, tests).  It also assumes that all NuGet packages that are packes with the `dotnet pack` SDK command will be pushed to the NuGet registry.

- If the `nuget_source` input isn't supplied, the organizational [GitHub NuGet registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry) (`https://nuget.pkg.github.com/${{ github.repository_owner }}/index.json`) is assumed.

## `push-dotnet-build-test-pack-push-default.yml`

This workflow leverages `dotnet-build-test-pack-push-default.yml` and allows a simple configuration for push actions, with packages being pushed to the GitHub NuGet registry:

``` yaml
name: Push

on: [push]

jobs:
  push:
    permissions:
      contents: read
      packages: write
    uses: NetChris/workflows/.github/workflows/push-dotnet-build-test-pack-push-default.yml@SHA
```

Note the `permissions` requirement.

## `pre-release-dotnet-build-test-pack-push-default.yml`

This workflow leverages `dotnet-build-test-pack-push-default.yml` and allows a simple configuration for pre-release actions, with packages being pushed to the GitHub NuGet registry and NuGet.org:

``` yaml
name: Pre-Release

on:
  release:
    types: [prereleased]

jobs:
  push:
    permissions:
      contents: read
      packages: write
    uses: NetChris/workflows/.github/workflows/pre-release-dotnet-build-test-pack-push-default.yml@SHA
    secrets: inherit
```

- Note the `permissions` requirement
- Note the `secrets: inherit` requirement

## `release-dotnet-build-test-pack-push-default.yml`

This workflow leverages `dotnet-build-test-pack-push-default.yml` and allows a simple configuration for release actions, with packages being pushed to the GitHub NuGet registry and NuGet.org:

``` yaml
name: Release

on:
  release:
    types: [released]

jobs:
  push:
    permissions:
      contents: read
      packages: write
    uses: NetChris/workflows/.github/workflows/release-dotnet-build-test-pack-push-default.yml@SHA
    secrets: inherit
```

- Note the `permissions` requirement
- Note the `secrets: inherit` requirement
