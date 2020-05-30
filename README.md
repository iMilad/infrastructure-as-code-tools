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
    - [AWS Access and Secret Keys](#aws-access-and-secret-keys)
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

### Usage
```shell script
$ terraform plan
$ terraform apply
```

# Ansible
### Ansible Installation
See the official page for how to install: [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)

### Ansible Configuration 
* Set EDITOR for Ansible-Vault `export EDITOR=vim` (or any other editor)
* edit ansible.cfg and set `host_key_checking = False` to avoid host key checking otherwise Ansible cannot connect to EC2 via SSH.

### AWS Access and Secret Keys
1. Run command below to create and encrypt content of the file, it will ask you at first for password, remember it as we need it each time we run Ansible playbook.
    ```shell script
    $ ansible-vault create keys.yml
    ```
2. copy & paste keys:
    ```shell script
    aws_access_key_id: <key>
    aws_secret_access_key: <key>
    aws_session_token: <key>
    ansible_ssh_private_key_file: <path-to-private-key>
    ```

### usage

```shell script
$ ansible-playbook -i hosts ec2.yml --tags create_ec2,configure_ec2 --ask-vault-pass
```
* First command will run ansible to get info about the running EC2.
* Second command uses tags to `create` or/and `config` EC2.
