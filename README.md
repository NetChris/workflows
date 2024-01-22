# Reusable GitHub workflows for NetChris

## `dotnet-build-test-pack-push-default.yml`

This is a simple build, test, pack and NuGet push for .NET projects.  "Default" in that it assumes the `dotnet` SDK commands `build`, `test`, `pack` and `nuget push` can be run and all required information is defaulted (e.g. solutions, projects, tests).  It also assumes that all NuGet packages that are packes with the `dotnet pack` SDK command will be pushed to the NuGet registry.

- If the `nuget_source` input isn't supplied, the organizational [GitHub NuGet registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry) (`https://nuget.pkg.github.com/${{ github.repository_owner }}/index.json`) is assumed.
