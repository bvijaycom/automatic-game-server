
# Automatic Games Server - Counter Strike: Global Offensive server

[Counter Strike: Global Offensive](https://blog.counter-strike.net/)

This repository contains the required code to be able to spin up a game server, in a DevOps way.

At the end you will got an ec2 instance in your configured AWS account with an installed Counter Strike: Global Offensive server, in automatic way. This code was used to create a virtual team-building.

# Table of contents

- [Automatic Games Server - Counter Strike: Global Offensive server](#automatic-games-server---counter-strike-global-offensive-server)
- [Table of contents](#table-of-contents)
  - [First usage](#first-usage)
    - [HowTo - Create and configure SSH-key](#howto---create-and-configure-ssh-key)
    - [Terraform binary](#terraform-binary)
    - [Configured GSLT code for server](#configured-gslt-code-for-server)
  - [Used technologies & Software](#used-technologies--software)
    - [Terraform](#terraform)
    - [Terraform providers](#terraform-providers)
    - [Ansible](#ansible)
    - [Visual Studio Code](#visual-studio-code)
  - [vagrant folder](#vagrant-folder)
    - [Purpose](#purpose)
    - [Usage](#usage)
  - [Describe files](#describe-files)
    - [connection.tf](#connectiontf)
    - [network.tf](#networktf)
    - [outputs.tf](#outputstf)
    - [servers.tf](#serverstf)
    - [variables.tf](#variablestf)
  - [Inputs](#inputs)
  - [Outputs](#outputs)
  - [Custom Counter Strike: Global Offensive settings](#custom-counter-strike-global-offensive-settings)
  - [How-To play your in your new server](#how-to-play-your-in-your-new-server)
  - [Common issues](#common-issues)
  - [License](#license)
  - [Author Information](#author-information)

## First usage

**[AWS account](https://aws.amazon.com/free/) (has free tier - credit card required) is a requirement**, as this terraform code will create resources on it. Please pay attention for **PRE-REQUIRED!** section at the end of this readme (Inputs), especially:

- key_name
- shared_credentials_file
- private_key

### HowTo - Create and configure SSH-key

Check the following [markdown documentation](Documentation/ssh_key/ssh_key.md).

### Terraform binary

Before you start to use this code, **terraform must to be installed**. Please follow official guides about [how to install it](https://learn.hashicorp.com/terraform/getting-started/install.html). If it was done, please apply **"terraform init"** command (in this repository's folder) to initialize required providers.

As a result you will got a plan what you can apply with **"terraform apply"** command. When you finished the game, you can destroy all created resource with **"terraform destroy"** command.

### Configured GSLT code for server

To be able to build a CS:GO server provided by steam, you need a GSLT code. For more information, please visit [this page](https://docs.linuxgsm.com/steamcmd/gslt).

After it please add you personaized GSLT code to [csgoserver.cfg](\vagrant\provision\csgoserver.cfg).

## Used technologies & Software

### Terraform

Terraform creates infrastructure under applications. In this example AWS provider is in use.

### Terraform providers

Terraform code was tested and use with following versions:

- Terraform                 = v0.12.26
- provider.aws: version     = v2.10.0
- provider.null: version    = v2.1.2

### Ansible

Ansible installs automatically applications / adjust OS settings.

### Visual Studio Code

This IDE was used to prepare and handle all of the code.

## vagrant folder

[Vagrant](https://www.vagrantup.com/) is a hashicorp tool which provides you a way to spin up a virtual machine in your local computer (via virtualbox). It is ideal to reproduce the server in your local computer, without any cloud provider.

### Purpose

Try / Check / Adjust and fine-tune the game server without any additional price.

### Usage

Change your directory to the vagrant folder (in IDE / terminal) and execute `vagrant up` command which will create a virtual machine based on configured "Vagrantfile".
After that you can connect to your dedicated Counter Strike: Global Offensive server in `192.168.56.56` address, port 27015 (default).

## Describe files

### connection.tf

Store provider(s) like AWS. This is a terraform plugin which "provide" classes.

### network.tf

Adjust network settings, required to create any instance within in. Most of the parameters are variables to use them during instance creation (servers.tf)

### outputs.tf

Define output values, displayed at the end of terraform's running.

### servers.tf

Describe instances & bootstrap code.

### variables.tf

Definition of variables, created / used in code for terraform.

***
**The text below was generated by an automatic document mechanism.**

## Inputs

| Name | Description | Type | Default |
|------|-------------|:----:|:-----:|
| readme | **NOT PART OF CODE** Readme information. This readme was generated with terraform-docs. terraform-docs --with-aggregate-type-defaults --no-required --no-sort markdown . | string | `"terraform-docs"` |
| key\_name | **PRE-REQUIRED!** SSH key name, used for linux instances. Must to be exist on AWS account before apply terraform code. | string | `"csgo"` |
| shared\_credentials\_file | **PRE-REQUIRED!** Path of your AWS credentials file. Do NOT store it under version control system! | string | `"./secrets/credentials"` |
| private\_key | **PRE-REQUIRED!** Path of your private SSH key. Required to connect target instance via SSH. | string | `"./secrets/csgo_priv.key"` |
| region | AWS region. Where to deploy with this Infrastructure-As-A-Code - terraform. | string | `"eu-west-1"` |
| profile | AWS Credential(s) profile. Define the name of the profile as defined in your aws credentials file. | string | `"default"` |
| instance\_type | AWS instance type. Define size of machine. <https://aws.amazon.com/ec2/instance-types/> | string | `"t3a.medium"` |
| ami\_user | SSH user, used for login to linux instance. Depends on used AMI. | string | `"ec2-user"` |

## Outputs

| Name | Description |
|------|-------------|
| Counter\_Strike\_Global\_Offensive\_server\_address | IP address of created cs go server. |

## Custom Counter Strike: Global Offensive settings

All fine-tune and modifications are in:

- [csgoserver.cfg](vagrant/provision/csgoserver.cfg)
- [server_config](/vagrant/provision/server_config)
- [gamemode_competitive.cfg](/vagrant/provision/gamemode_competitive.cfg)

## How-To play your in your new server

You have multiple way, how to connect to your customer server. Here is an [example](https://nodecraft.com/support/games/csgo/how-to-quickly-find-and-join-your-cs-go-server).

## Common issues

Check the following [markdown documentation](Documentation/common_issues/common_issues.mdDocumentation).


## License

MIT

## Author Information

Peter Mikaczo - <petermikaczo@gmail.com>
