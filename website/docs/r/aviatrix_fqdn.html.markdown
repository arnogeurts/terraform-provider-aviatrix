---
layout: "aviatrix"
page_title: "Aviatrix: aviatrix_fqdn"
sidebar_current: "docs-aviatrix-resource-fqdn"
description: |-
  Manages Aviatrix FQDN filtering for Gateway
---

# aviatrix_fqdn

The FQDN resource manages FQDN filtering for Aviatrix Gateway

## Example Usage

```hcl
# Set Aviatrix Gateway FQDN filter
resource "aviatrix_fqdn" "test_fqdn" {
  fqdn_tag = "my_tag"
  fqdn_status = "enabled"
  fqdn_mode = "white"
  gw_list = ["gw1", "gw2"]
  domain_names = [
  {
   fqdn = "facebook.com"
   proto = "tcp"
   port = "443"
  },
  {
   fqdn = "reddit.com"
   proto = "tcp"
   port = "443"
  }
]

```

## Argument Reference

The following arguments are supported:

* `fqdn_tag` - (Required) FQDN Filter Tag Name
* `fqdn_status` - (Optional) FQDN Filter Tag Status. Valid values: "enabled", "disabled"
* `fqdn_mode` - (Optional) Specify the tag color to be a white-list tag or black-list tag. Valid Values: "white", "black"
* `gw_list` - (Optional) Name of the gateway. One or more gateways as list ["gw1", "gw2"]
* `domain_names` - (Optional) One or more domain names in a list with details as listed below
    * `fqdn` - (Optional) FQDN. Example: "facebook.com" 
    * `proto` - (Optional) Protocol. Valid values: "all", "tcp", "udp", "icmp" 
    * `port` - (Optional) Port. Example "25" 
        * protocol 'all' will default to 'all' regardless of input
        * icmp type/code is expected as 0-39/0-19 or None or "ping" in the port field

## Import

Instance fqdn can be imported using the fqdn_tag, e.g.

```hcl
$ terraform import aviatrix_fqdn.test fqdn_tag
```