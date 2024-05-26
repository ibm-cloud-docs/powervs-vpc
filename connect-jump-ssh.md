---

copyright:
  years: 2023, 2024
lastupdated: "2024-05-24"

keywords:
subcollection: powervs-vpc
content-type: tutorial
services: ssh
completion-time: 10 mins

---

{{site.data.keyword.attribute-definition-list}}

# Connect to a VPC VSIs or Power Virtual Server Instances using floating IP
{: #solution-ssh}

After the deployment has been completed you can connect to the landscape by using ssh proxy command to connect to the private ip of both Intel and PowerVS instances over floating IP of jump box.
{: shortdesc}

## Before you begin
{: #solution-ssh-prereqs}

1. Make sure you have deployed the landscape by entering a value in the `external_access_ip` field. Only this IP will be allowed to login to the environment as it is allowed in the management-sg group.
1. Review the outputs from the deployable architecture.

## Connect to the landscape
{: #solution-ssh-connect}

1. Make sure you have the right private SSH key.
1. Use the following SSH commands to access the hosts.

```sh
ssh root@<access_host_or_ip>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip>" root@<ansible_host_or_ip>

ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand="ssh -W %h:%p root@<access_host_or_ip>" root@<ntp_host_or_ip>
```
