---

copyright:
  years: 2023
lastupdated: "2023-03-26"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the environment
{: #powervs-automation-solution-access}

After successful deployment, {{site.data.keyword.bplong_notm}} provides an output log that lists all IP addresses of created VPC instances. These IP addresses include:
    - An access host IP address that is the entry point to the whole landscape.
    - NFS, DNS, NTP server IP addresses.

The Power Virtual Server with VPC landing zone deployable architecture creates secure and isolated environment. Network communication with the public internet and other landscapes sitting outside of the configured environment is prohibited. Opening the management network channel, for example, for the access with administrator laptop, is the step that must be done manually. In general, there a couple of options for such configuration:

1. Open the VPN connection to the management VPC where access to the host is located.
2. Add an additional IP address to the network access control list of the management VPC where access host is located. You can configure the {{site.data.keyword.vpc_full}} (VPC) by using the {{site.data.keyword.cloud_notm}} console.

1. Open [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](/login).
1. Click **Menu icon ![Menu icon](../../icons/icon_hamburger.svg) > VPC Infrastructure > Network > VPCs**
1. In the navigation pane, click **Network > Subnets**.
1. Click the subnet that you created.
1. In the **Subnet details** area, click the name of the ACL.
1. Select the region where you completed the deployment and the access control list named '[prefix]-management-acl', where [prefix] corresponds to the one specified by deployment. 
1. Insert following rules:
    - Inbound rule: Type - 'Allow', Protocol - 'TCP', Source IP/CIDR - 'your IP address or CIDR range', Source port range - 'any port', Destination CIDR - '10.10.10.0/24', Destination port range - '22-22'.
    - Outbound rule: Type - 'Allow', Protocol - 'TCP', Source CIDR - '10.10.10.0/24', Source port range - '22-22', Destination IP/CIDR - 'your IP address or CIDR range', Destination port range - 'any port'.

After the configuration, you can connect to the landscape by using following SSH command:

```sh
ssh -A -o ServerAliveInterval=60 -o ServerAliveCountMax=600 -o ProxyCommand=\"ssh -W %h:%p root@\<access_host_or_ip\>\" root@\<vpc_instance_ip\>
```
