---

copyright:
  years: 2023, 2024
lastupdated: "2024-06-27"

keywords:
subcollection: powervs-vpc
content-type: tutorial
services: ssh
completion-time: 10 mins

---

{{site.data.keyword.attribute-definition-list}}

# Connect to a VPC VSIs or Power Virtual Server Instances by using floating IP
{: #solution-ssh}

After deployment, connect to the landscape via SSH proxy using the jump box's floating IP to access the private IPs of Intel and PowerVS instances.
{: shortdesc}

## Before you begin
{: #solution-ssh-prereqs}

1. Ensure you deployed the landscape by entering a value in the `external_access_ip` field. Only this IP is allowed to login to the environment as it is allowed in the management-sg group.
1. Review the outputs from the deployable architecture.

## Connect to the landscape
{: #solution-ssh-connect}

1. Make sure you have the right private SSH key.
1. Use the following SSH commands to access the hosts.

```sh
ssh root@<access_host_or_ip> -i <path_to_private_key>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip> -i <path_to_private_key>" root@<ansible_host_or_ip> -i <path_to_private_key>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip> -i <path_to_private_key>" root@<ntp_host_or_ip> -i <path_to_private_key>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip> -i <path_to_private_key>" root@<dns_host_or_ip> -i <path_to_private_key>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip> -i <path_to_private_key>" root@powervs_instance_management_ip> -i <path_to_private_key>
```
