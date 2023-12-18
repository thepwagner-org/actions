# actions

These are GitHub Actions reusable workflows:
* `build.yaml` - Build a `Dockerfile`, generate an SBOM and store that SBOM as a cosign attestation. If the SBOM is different from the current `:latest` version, report the difference in a comment. Intended for use on the non-default branch / pull requests.
* `publish.yaml` - Promote an image generated from `build.yaml` to the `:latest` tag and cosign sign it. Intended for use on the default branch / merges.
* `check.yaml` - Build a `Dockerfile`, generate an SBOM and if it is different from the current `:latest` version open a pull request. Intended for use on a cron schedule to refresh packages installed via `apt-get` and other non-deterministic sources.

I'm currently using Trivy to generate SBOMs including vulnerabilty scans, and loving it!

You can see these in use in:
* https://github.com/thepwagner-org/debian - base image
* https://github.com/thepwagner-org/duplicity - consumer image
* https://github.com/thepwagner/github-token-factory-oidc - golang app

This repo is also a demonstration of versioning reusable workflows: changes are staged in the `main` branch, but most users of the workflows follow tagged releases and are pushed updates via RenovateBot pull request - [example](https://github.com/thepwagner-org/debian-bullseye/pull/162).
