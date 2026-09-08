<!-- llm-readme-management spec=1 commit=d03441b1cb0c71457b765593404735989069079d template=default model=qwen3.6-35b-a3b digest=598d66067ca0 generated=2026-09-08T23:43:46Z -->
<a href="https://hauke.cloud" target="_blank"><img src="https://img.shields.io/badge/home-hauke.cloud-brightgreen" alt="hauke.cloud" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud" target="_blank"><img src="https://img.shields.io/badge/github-hauke.cloud-blue" alt="hauke.cloud Github Organisation" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud/llm-readme-management" target="_blank"><img src="https://img.shields.io/badge/template-default-orange" alt="Repository type - default" style="display: block;" /></a>


# Template repository for Packer


<img src="https://raw.githubusercontent.com/hauke-cloud/.github/main/resources/img/organisation-logo-small.png" alt="hauke.cloud logo" width="109" height="123" align="right">


<llm header>

This GitHub template repository provides CI workflows and reusable actions for building Linux machine images with a Packer template on Hetzner Cloud. It supplies the complete pipeline scaffolding, including automated image builds, snapshot pruning, and resource cleanup, so you can quickly bootstrap new image-building projects as an internal infrastructure engineer within the hauke.cloud organisation.

</llm>


## :book: Description

<llm description>

Setting up continuous integration for cloud machine images requires boilerplate CI configuration, environment routing, and lifecycle management. This repository solves that by providing a GitHub template pre-configured with Packer workflows and reusable actions for Hetzner Cloud. You fork it to bootstrap new infrastructure projects within the hauke.cloud organisation, gaining automated image compilation, snapshot retention, and cleanup of temporary build resources without writing pipeline code from scratch.

It standardises image-building operations across multiple environments by providing:
- Three environment-specific CI workflows (lab, home, public) triggered on schedule, branch pushes, or repository dispatches
- Composite actions that initialise Packer, validate HCL templates, and execute builds against Hetzner Cloud
- Automated cleanup routines that remove orphaned servers, SSH keys, and outdated image snapshots
- Built-in repository maintenance for semantic PR titles and stale issue handling

</llm>


## 🚀 Getting started

<llm getting_started hint="Assume nothing about the ecosystem beyond what the analysis names. If the repository has no build step, say what a reader does with it instead.">

1. Clone the repository and navigate into the directory.
```bash
git clone https://github.com/hauke-cloud/template-packer-repository.git
cd template-packer-repository
```

2. Install the local pre-commit hooks to enforce code standards.
```bash
pre-commit install
```

3. Run all configured checks against the current files.
```bash
pre-commit run --all-files
```

</llm>


## :airplane: Usage

<llm usage>

After forking this template into a new project, you must adapt the CI configuration and provide your own Packer definition before pipelines can run. Rename the workflow templates to remove the `.template` suffix so GitHub Actions recognises them:
```bash
mv .github/workflows/build-lab.yaml.template .github/workflows/build-lab.yaml
mv .github/workflows/build-home.yaml.template .github/workflows/build-home.yaml
mv .github/workflows/build-public.yaml.template .github/workflows/build-public.yaml
```

Next, create the machine image definition at `template.pkr.hcl` in your repository root. The composite actions expect specific variables to be declared so they can pass runtime values during validation and build steps:
```hcl
variable "hcloud_token" { type = string }
variable "build_identifier" { type = string }
variable "snapshot_name" { type = string }
variable "github_branch" { type = string }
variable "version" { default = "latest" }
```

You must also configure three GitHub environments (`lab`, `home`, `public`) and store your API token as a secret named `HCLOUD_TOKEN` in each. Builds trigger automatically when you push to `dev`, `main`, or `home` branches, or manually via a repository dispatch. For local development, install and run the configured hooks before committing:
```bash
pre-commit install
pre-commit run --all-files
```

</llm>


## 📄 License

This Project is licensed under the GNU General Public License v3.0

- see the [LICENSE](LICENSE) file for details.


## :coffee: Contributing

To become a contributor, please check out the [CONTRIBUTING](CONTRIBUTING.md) file.


## :email: Contact

For any inquiries or support requests, please open an issue in this
repository or contact us at [contact@hauke.cloud](mailto:contact@hauke.cloud).
