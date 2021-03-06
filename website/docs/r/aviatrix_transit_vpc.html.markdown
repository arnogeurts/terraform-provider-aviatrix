---
layout: "aviatrix"
page_title: "Aviatrix: aviatrix_transit_vpc"
sidebar_current: "docs-aviatrix-resource-transit_vpc"
description: |-
  Manages the Aviatrix Transit Network Gateways
---

# aviatrix_transit_vpc

The AviatrixTransitVpc resource manages the Aviatrix Transit Network Gateways

## Example Usage

```hcl
# Manage Aviatrix Transit Network Gateways
resource "aviatrix_transit_vpc" "test_transit_gw" {
  cloud_type = 1
  account_name = "devops"
  gw_name = "transit"
  vpc_id = "vpc-abcd1234"
  vpc_reg = "us-east-1"
  vpc_size = "t2.micro"
  subnet = "10.1.0.0/24"
  ha_subnet = "10.1.0.0/24"
  ha_gw_size = "t2.micro"
  tag_list = ["name:value", "name1:value1", "name2:value2"]
  enable_hybrid_connection = true
  connected_transit = "yes"
}
```

## Argument Reference

The following arguments are supported:

* `cloud_type` - (Required) Type of cloud service provider, requires an integer value. Use 1 for AWS
* `account_name` - (Required) This parameter represents the name of a Cloud-Account in Aviatrix controller.
* `gw_name` - (Required) Name of the gateway which is going to be created.
* `vpc_id` - (Required) VPC-ID/VNet-Name of cloud provider.  Example: AWS: "vpc-abcd1234", ARM: "VNet_Name:Resource_Group_Name", GCP: "mygooglecloudvpcname", etc...
* `vpc_reg` - (Required) Region of cloud provider. Example: AWS: "us-east-1", ARM: "East US 2", etc...
* `vpc_size` - (Required) Size of the gateway instance.  Example: AWS: "t2.large", etc...
* `subnet` - (Required) Public Subnet Name.  Example: AWS: "10.0.0.0/16\~\~us-east1c\~\~subnet1". Copy/paste from AWS Console to get the right subnet name.
* `dns_server` - (Optional) Specify the DNS IP, only required while using a custom private DNS for the VPC.
* `ha_subnet` - (Optional) HA Subnet. Setting to empty/unset will disable HA. Setting to a valid subnet (Example: 10.12.0.0/24) will create an HA gateway on the subnet
* `ha_gw_size` - (Optional) HA Gateway Size. Mandatory if HA is enabled (ha_subnet is set)(Example: "t2.micro")
* `enable_nat` - (Optional) Enable NAT for this container. (Supported values: "yes", "no")
* `tag_list` - (Optional) Instance tag of cloud provider. Example: ["key1:value1","key002:value002"]
* `enable_hybrid_connection` - (Optional) Sign of readiness for TGW connection.( Example : false)
* `connected_transit` - (Optional) Specify Connected Transit status. (Supported values: "yes", "no")

## Import

Instance transit_vpc can be imported using the gw_name, e.g.

```hcl
$ terraform import aviatrix_transit_vpc.test gw_name
```