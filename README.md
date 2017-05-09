# labmodules
labmodules
# Description

Template to create:

* VPC
* Internet Gateway
* DHCP Option Set

Support VPC Flow Logs.

# Requierements

Terraform version >= 0.7

# main.tf configuration example
    module "vpc"{
       source = "git::ssh://git@bitbucket.org/claroes-es/terraform.template.vpc.git" //nosotros usamos el repositorio, pero el source puede ser también local o un bucket.
       env = "${var.general.["env"]}"
       client_name = "${var.general.["client_name"]}"
       domain_name = "${var.general.["domain_name"]}"
       domain_name_servers = "${var.general.["domain_name_servers"]}"
       aws_region = "${var.aws_region}"
       cidr = "${var.network.["cidr_vpc"]}"
    }

# variables.tf configuration example

    provider "aws" {
      region = "${var.aws_region}"
      }

    variable "general" {
      description = "General variables"
      default {
         env = "prod"
         client_name = "client1"
         domain_name = "client1.com"
         domain_name_servers = "127.0.0.1,AmazonProvidedDNS"
         }
    }
    variable "network" {
      description = "Network variables"
      default {
        cidr_vpc = "10.200.0.0/16"
        }
    }

# Output variables

* vpc_id = XXXXX     The VPC ID created
* gw_id = XXXXXX     The Gateway ID created
