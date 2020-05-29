![stability-wip](https://img.shields.io/badge/stability-work_in_progress-lightgrey.svg)
![last-commit](https://img.shields.io/github/last-commit/imilad/infrastructure-as-code-tools)

## Tools can be used as Infrastructure as Code

Try out some IaC tools to provision EC2 instance on AWS.

### Terraform
* [Install terraform](https://learn.hashicorp.com/terraform/getting-started/install.html)

* Generate ssh key for SSH connection, after that update `terraform.tfvars` with the correct key name and path to public key.
```shell script
$ ssh-keygen
```

* run terraform
```shell script
$ terraform plan
$ terraform apply
```

* ssh to ec2
```shell script
$ ssh -i ~/.ssh/ec2key ec2-user@<EC2-IP>
```

