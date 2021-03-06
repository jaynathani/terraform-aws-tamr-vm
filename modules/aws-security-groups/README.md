# Tamr VM Security Groups Module
This module creates security groups for the EC2 instance where Tamr is running. These groups will allow port openings, SSH access, and related networking permissions for EC2.

# Examples
## Basic
Inline example implementation of the module.  This is the most basic example of what it would look like to use this module.
```
module "aws-vm-sg" {
  source = "git::https://github.com/Datatamer/terraform-aws-tamr-vm.git//modules/aws-security-groups?ref=0.5.0"
  vpc_id = "vpc-123456789"
  ingress_cidr_blocks = [
    "1.2.3.4/32"
  ]
  egress_cidr_blocks  = [
    "0.0.0.0/0"
  ]
}
```

# Resources Created
This module creates:
* a security group for EC2 allowing access to the Tamr VM.
* additonal security group rules. By default, opens required Tamr ports,
enables HTTP on port `80` and TLS on `443`, and opens egress, which allows Tamr to operate and recreate AWS's default ALLOW ALL egress rules. These ports can be changed if desired. Additional ports for basic monitoring (Kibana and Grafana), as well as SSH, and ping, can be enabled using boolean variables. Additional rules can be added manually.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.12 |
| aws | >= 2.45.0 |

## Providers

| Name | Version |
|------|---------|
| aws | >= 2.45.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| vpc\_id | The ID of the VPC in which to attach the security group | `string` | n/a | yes |
| additional\_tags | Additional tags to be attached to the resources created | `map(string)` | <pre>{<br>  "Author": "Tamr"<br>}</pre> | no |
| egress\_cidr\_blocks | CIDR blocks to attach to security groups for egress | `list(string)` | `[]` | no |
| egress\_security\_groups | Existing security groups to attch to new security groups for egress | `list(string)` | `[]` | no |
| enable\_grafana\_port | If set to true, opens the grafana port for ingress | `bool` | `true` | no |
| enable\_kibana\_port | If set to true, opens the kibana port for ingress | `bool` | `true` | no |
| enable\_ping | If set to true, enables ping | `bool` | `true` | no |
| enable\_ssh | If set to true, enables SSH | `bool` | `true` | no |
| grafana\_port | Default Grafana port | `number` | `31101` | no |
| ingress\_cidr\_blocks | CIDR blocks to attach to security groups for ingress | `list(string)` | `[]` | no |
| ingress\_security\_groups | Existing security groups to attch to new security groups for ingress | `list(string)` | `[]` | no |
| kibana\_port | Default Kibana port | `number` | `5601` | no |
| sg\_name | Security Group to create | `string` | `"tamr-instance-security-group"` | no |
| tamr\_auth\_port | Port for Tamr auth | `number` | `9020` | no |
| tamr\_es\_port | Port for Tamr elasticsearch | `number` | `9200` | no |
| tamr\_persistence\_port | Port for Tamr persistence | `number` | `9080` | no |
| tamr\_ui\_port | Port for Tamr UI and proxying Tamr services | `number` | `9100` | no |
| zk\_port | Port for accessing Zookeeper on the Tamr instance | `number` | `21281` | no |

## Outputs

| Name | Description |
|------|-------------|
| tamr\_security\_group\_id | ID of the security group created |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

# References
This repo is based on:
* [terraform standard module structure](https://www.terraform.io/docs/modules/index.html#standard-module-structure)
* [templated terraform module](https://github.com/tmknom/template-terraform-module)

# License
Apache 2 Licensed. See LICENSE for full details.
