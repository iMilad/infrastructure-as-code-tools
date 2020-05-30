![stability-wip](https://img.shields.io/badge/stability-work_in_progress-lightgrey.svg)
![last-commit](https://img.shields.io/github/last-commit/imilad/infrastructure-as-code-tools)

## Tools can be used as Infrastructure as Code
Try out some IaC tools to provision EC2 instance on AWS.

**Table of Contents**
- [Workflow](#workflow)
- [Create SSH Key](#create-ssh-key)
    - [Generate SSH key](#ssh-keygen)
    - [SSH to ec2](#connect-to-ec2)
- [Terraform](#terraform)
    - [Installation](#terraform-installtion)
    - [Usage](#usage)
- [Ansible](#ansible)
    - [Installation](#ansible-installation)
    - [Usage](#usage)

# Workflow
* Create EC2 instance
* Create Security Group and attach to EC2
* Generate ssh public key locally
* Upload ssh public key to AWS and attach it to EC2
* Install Docker on EC2
* Run Ngnix

# Create SSH Key 
### ssh-keygen
Generate ssh key for SSH connection, after that update `terraform.tfvars` with the correct key name and path to public key.
```shell script
$ ssh-keygen
```

### connect to ec2
```shell script
$ ssh -i ~/.ssh/terraformKey ec2-user@<EC2-IP>
```


# Terraform
### Terraform Installtion
See the official page for how to install terraform: [Install terraform](https://learn.hashicorp.com/terraform/getting-started/install.html)

#### usage
```shell script
$ terraform plan
$ terraform apply
```

# Ansible
### Ansible Installation
* first create a file `keys.yml` and store your AWS credentials in `YAML` format.

### usage
```shell script
$ ansible-playbook -i hosts ec2.yml # without tag will run just _info_ task
$ ansible-playbook -i hosts ec2.yml --tags create_ec2,configure_ec2 
```
* First command will run ansible to get info about the running EC2.
* Second command uses tags to `create` or/and `config` EC2.
