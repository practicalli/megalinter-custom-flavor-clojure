# MegaLinter Custom Flavor: Clojure

This custom MegaLinter aims to have an optimized Docker image size.

It is built from official MegaLinter images, but is maintained on https://github.com/practicalli/megalinter-custom-flavor-clojure by Practicalli Engineering

Beta push

## Embedded linters

  - [BASH_SHELLCHECK](https://megalinter.io/latest/descriptors/bash_shellcheck/)
  - [CLOJURE_CLJSTYLE](https://megalinter.io/latest/descriptors/clojure_cljstyle/)
  - [CLOJURE_CLJ_KONDO](https://megalinter.io/latest/descriptors/clojure_clj_kondo/)
  - [DOCKERFILE_HADOLINT](https://megalinter.io/latest/descriptors/dockerfile_hadolint/)
  - [MAKEFILE_CHECKMAKE](https://megalinter.io/latest/descriptors/makefile_checkmake/)
  - [MARKDOWN_MARKDOWN_TABLE_FORMATTER](https://megalinter.io/latest/descriptors/markdown_markdown_table_formatter/)
  - [MARKDOWN_RUMDL](https://megalinter.io/latest/descriptors/markdown_rumdl/)
  - [REPOSITORY_BETTERLEAKS](https://megalinter.io/latest/descriptors/repository_betterleaks/)
  - [SPELL_LYCHEE](https://megalinter.io/latest/descriptors/spell_lychee/)
  - [YAML_V8R](https://megalinter.io/latest/descriptors/yaml_v8r/)

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- GitHub Action: On MegaLinter step in .github/workflows/mega-linter.yml, define `uses: practicalli/megalinter-custom-flavor-clojure@main`
- Docker image: Replace official MegaLinter image with `ghcr.io/practicalli/megalinter-custom-flavor-clojure/megalinter-custom-flavor:latest`

## How the flavor is generated and updated

This custom flavor is automatically kept up to date with MegaLinter releases:

1. **Automatic version sync**: The `check-new-megalinter-version` workflow runs daily, checks for new MegaLinter releases, and automatically creates matching releases in this repository.

2. **Automated builds**: Each release triggers the `megalinter-custom-flavor-builder` workflow, which:
   - Builds a Docker image with only the selected linters
   - Publishes to GitHub Container Registry (ghcr.io)
   - Optionally publishes to Docker Hub (if credentials are configured)

3. **Available image tags**:
   - Release tags (e.g., `v9.0.0`): Built from MegaLinter releases
   - `beta` tag: Built from non-main branch pushes for testing
   - `latest` tag: Points to the most recent release

## Configuration requirements

### Optional: Personal Access Token (use with care)

> **Security warning**: Using a Personal Access Token (PAT) is **not recommended**. Open-source projects have been heavily targeted by supply-chain attacks in recent months, and a leaked or compromised PAT can give attackers broad write access to your repository — better safe than sorry!
> If you do not need fully automatic daily version sync, you can skip the PAT entirely and trigger the `check-new-megalinter-version` workflow manually whenever you want to upgrade.

If you decide automatic daily releases are worth the trade-off, configure a `PAT_TOKEN` secret as a **repository-scoped fine-grained token** with:

- **Repository access**: Only select repositories (select this repository)
- **Repository permissions**:
  - Contents: Read and write
  - Actions: Read and write

Rotate the token regularly.

See the [Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/) for detailed setup instructions.

### Optional: Docker Hub publishing

To publish to Docker Hub in addition to ghcr.io, configure:
- `DOCKERHUB_REPO` variable (e.g., your Docker Hub username)
- `DOCKERHUB_USERNAME` secret
- `DOCKERHUB_PASSWORD` secret

## How to generate the flavor manually

If you need to manually trigger a build:

1. **Create a GitHub release**: Creates a versioned build matching the tag name (e.g., `v9.0.0`)
2. **Push to any branch** (except main): Builds a `beta` tagged image for testing
3. **Manually run the workflow**: Go to Actions > Build & Push MegaLinter Custom Flavor > Run workflow

See [full Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/).

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- **GitHub Action**: On MegaLinter step in `.github/workflows/mega-linter.yml`, define `uses: practicalli/megalinter-custom-flavor-clojure@main`
- **Docker image**: Replace official MegaLinter image with `ghcr.io/practicalli/megalinter-custom-flavor-clojure/megalinter-custom-flavor:latest`

[![MegaLinter is graciously provided by OX Security](https://raw.githubusercontent.com/oxsecurity/megalinter/main/docs/assets/images/ox-banner.png)](https://www.ox.security/?ref=megalinter)
