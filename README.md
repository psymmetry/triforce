# :recycle: Make, Docker-Compose and Terraform

<br />

![image](docs/triforce.png)<br />
<br />
A skeleton repo that uses `make`, `docker-compose` and `terraform` to deploy an S3 Bucket in AWS. The idea is that this "template" can be modified or extended to include extra steps to build/pack application code as well. This pattern is used to minimise the dependencies and reliance on **cicd** tools/agents/systems so that steps used in **cicd** environments can be replicated exactly the same way locally, decreasing complexity as a result.

---

## :heavy_check_mark: Prerequisites

_Make is native to MacOS and all the different flavours of linux so no installation is required._

**MacOS/Linux:**
* [Docker + docker-compose](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)

**Windows:**
* [GNU Make](http://gnuwin32.sourceforge.net/packages/make.htm)
* [Docker + docker-compose](https://hub.docker.com/editions/community/docker-ce-desktop-windows/)

---
## :computer: Setup

1. Before running `make` commands, you will first need to **authenticate** to the cloud provider you're using when running commands locally. AWS is being used in this example to build an S3 bucket. There are a few open source tools such as [awsume](https://awsu.me/) that can perform this task quite well, especially when switching between multiple accounts.

2. The `./infra/config/dev/dev.tfvars` file and  `./infra/config/dev/dev.backend` file both need to be updated before running `make` commands. Below is an example of `dev` environment variables being used. The same pattern can be applied for other environments.

`./infra/config/dev/dev.backend` Terraform state bucket and region:
```hcl
bucket = "my-terraform-state-bucket-dev"
region = "ap-southeast-2"
```
`./infra/config/dev/dev.tfvars` Terraform infrastructure variables:
```hcl
environment = "dev"
region = "ap-southeast-2"
bucket = "my-example-bucket-dev"
```
---

## :mega: Usage

_All `make` commands can be found within the `Makeile` if required to run certain functions individually. Below is an example of building a terraform plan, running compliance tests against that plan and then deploying to a "dev" AWS environment. The default value for `$ENVIRONMENT` is "dev" so this variable would need updating when deploying to other environments._

* Run a step that performs a `terraform init` to the backend and `terraform plan` :
```makefile
make plan
```
* Run a step that performs a [terraform-compliance](https://terraform-compliance.com/) test against the `terraform plan` :
```makefile
make comply
```
* Run a step that performs a `terraform apply` step to deploy `terraform plan` to AWS:
```makefile
make apply
```

### :rocket: Example:
![image](docs/example.gif)

---

## :bookmark_tabs: References:

* [3 Musketeers](https://3musketeers.io/)
* [Make](https://opensource.com/article/18/8/what-how-makefile/)
* [Docker](https://www.docker.com/)
* [Terraform](https://www.terraform.io/)
* [Terraform Compliance](https://terraform-compliance.com/)
