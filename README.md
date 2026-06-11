# MegaLinter Custom Flavor: forge

This custom MegaLinter aims to have an optimized Docker image size.

It is built from official MegaLinter images, but is maintained on https://github.com/ehmd96/megalinter-custom-flavor-ansible-docker-helm-kube-terraform-lint by ElHadji Dieng

## Embedded linters

  - [ANSIBLE_ANSIBLE_LINT](https://megalinter.io/latest/descriptors/ansible_ansible_lint/)
  - [DOCKERFILE_HADOLINT](https://megalinter.io/latest/descriptors/dockerfile_hadolint/)
  - [KUBERNETES_HELM](https://megalinter.io/latest/descriptors/kubernetes_helm/)
  - [KUBERNETES_KUBECONFORM](https://megalinter.io/latest/descriptors/kubernetes_kubeconform/)
  - [KUBERNETES_KUBESCAPE](https://megalinter.io/latest/descriptors/kubernetes_kubescape/)
  - [TERRAFORM_TERRAFORM_FMT](https://megalinter.io/latest/descriptors/terraform_terraform_fmt/)
  - [TERRAFORM_TERRAGRUNT](https://megalinter.io/latest/descriptors/terraform_terragrunt/)
  - [TERRAFORM_TERRASCAN](https://megalinter.io/latest/descriptors/terraform_terrascan/)
  - [TERRAFORM_TFLINT](https://megalinter.io/latest/descriptors/terraform_tflint/)

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- GitHub Action: On MegaLinter step in .github/workflows/mega-linter.yml, define `uses: ehmd96/megalinter-custom-flavor-ansible-docker-helm-kube-terraform-lint@main`
- Docker image: Replace official MegaLinter image with `ghcr.io/ehmd96/megalinter-custom-flavor-ansible-docker-helm-kube-terraform-lint/megalinter-custom-flavor:latest`

## How the flavor is generated and updated

This custom flavor is automatically kept up to date with MegaLinter releases:

1. **Automatic version sync**: The `check-new-megalinter-version` workflow runs daily, checks for new MegaLinter releases, and automatically creates matching releases in this repository.

2. **Automated builds**: Each release triggers the `megalinter-custom-flavor-builder` workflow, which:
   - Builds a Docker image with only the selected linters
   - Publishes to GitHub Container Registry (ghcr.io)
   - Optionally publishes to Docker Hub (if credentials are configured)

3. **Available image tags**:
   - Release tags (e.g., `v9.0.0`): Built from MegaLinter releases
   - `beta` tag: Built from branch pushes for testing
   - `latest` tag: Points to the most recent release

## Configuration requirements

### Required: Personal Access Token

For automatic version checking to work, a `PAT_TOKEN` secret must be configured as a **repository-scoped fine-grained token** with:
- **Repository access**: Only select repositories (select this repository)
- **Repository permissions**:
  - Contents: Read and write
  - Actions: Read and write

See the [Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/) for detailed setup instructions.

### Optional: Docker Hub publishing

To publish to Docker Hub in addition to ghcr.io, configure:
- `DOCKERHUB_REPO` variable (e.g., your Docker Hub username)
- `DOCKERHUB_USERNAME` secret
- `DOCKERHUB_PASSWORD` secret

## How to generate the flavor manually

If you need to manually trigger a build:

1. **Create a GitHub release**: Creates a versioned build matching the tag name (e.g., `v9.0.0`)
2. **Push to any branch**: Builds a `beta` tagged image for testing
3. **Manually run the workflow**: Go to Actions > Build & Push MegaLinter Custom Flavor > Run workflow

See [full Custom Flavors documentation](https://megalinter.io/beta/custom-flavors/).

## How to use the custom flavor

Follow [MegaLinter installation guide](https://megalinter.io/latest/install-assisted/), and replace related elements in the workflow.

- **GitHub Action**: On MegaLinter step in `.github/workflows/mega-linter.yml`, define `uses: ehmd96/megalinter-custom-flavor-ansible-docker-helm-kube-terraform-lint@main`
- **Docker image**: Replace official MegaLinter image with `ghcr.io/ehmd96/megalinter-custom-flavor-ansible-docker-helm-kube-terraform-lint/megalinter-custom-flavor:latest`

[![MegaLinter is graciously provided by OX Security](https://raw.githubusercontent.com/oxsecurity/megalinter/main/docs/assets/images/ox-banner.png)](https://www.ox.security/?ref=megalinter)
