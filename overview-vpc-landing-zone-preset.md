---

copyright:
   years: 2023, 2024
lastupdated: "2024-09-09"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# VPC landing zone architecture for PowerVS
{: #landing-zone-preset}

The {{site.data.keyword.powerSys_notm}} with VPC landing zone makes use of [Terraform IBM Module - VPC Landing Zone](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone){: external}.


As part of the automation an [override json preset](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/modules/powervs-vpc-landing-zone/presets/slz-preset.json.tftpl) is passed to this module. The JSON preset defines which VPC components are created.


- A **Edge VPC Infrastructure** with the following components:
    - 4 subnets
    - One VSI for one management (jump/bastion) VSI,
    - One VSI for network-services configured as squid proxy, NTP and DNS servers(using Ansible Galaxy collection roles [ibm.power_linux_sap collection](https://galaxy.ansible.com/ui/repo/published/ibm/power_linux_sap/). This VSI also acts as central ansible execution node.
    - Optional [Client to site VPN server](https://cloud.ibm.com/docs/vpc?topic=vpc-vpn-client-to-site-overview)
    - Optional [File storage share](https://cloud.ibm.com/docs/vpc?topic=vpc-file-storage-create&interface=ui)
    - Optional [Application load balancer](https://cloud.ibm.com/docs/vpc?topic=vpc-load-balancers&interface=ui)
    - IBM Cloud Object storage(COS) Virtual Private endpoint gateway(VPE)
    - IBM Cloud Object storage(COS) Instance and buckets
    - VPC flow logs
    - KMS keys
    - Activity tracker
    - Optional Secrets Manager Instance with private certificate.

- A local or global **transit gateway**


## ACL
{: #landing-zone-acl}

The ACL rules for the Edge VPC allow all traffic.

### Inbound rules
{: #landing-zone-acl-inbound}

| Priority | Allow or deny | Protocol | Source | Destination |
|----------|------------|----------|--------|-------------|
| 1 | Allow | ALL | ANY IP | ANY IP  |
{: caption="Table 1. Inbound ACL rules" caption-side="bottom"}

### Outbound rules
{: #landing-zone-acl-outbound}

| Priority | Allow or deny | Protocol | Source | Destination |
|----------|------------|----------|--------|-------------|
| 1 | Allow | ALL | ANY IP | ANY IP  |
{: caption="Table 2. Outbound ACL rules" caption-side="bottom"}

## Security Groups
{: #landing-zone-sg}

The security groups are created and attached to correct subnets/VPE/VPN. For the management security group, 25 [Schematics IP addresses](/docs/schematics?topic=schematics-allowed-ipaddresses&interface=ui#ipaddresses) are added to inbound rules. This is required to allow ssh login access from schematics to the intel VSIs to perform OS configuration using ansible playbooks.

### Security Group Rules
{: #landing-zone-sg-rules}

| Name | Source |  Protocol: Value | Attached resources
|----------|------------|----------|--------|
| management-sg | * [Schematics IP addresses](/docs/schematics?topic=schematics-allowed-ipaddresses&interface=ui#ipaddresses) \n * IBM Inbound `161.26.0.0/16` \n * `10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16` \n * Optional user provided IP address/CIDR   | * TCP: 22 \n * ALL: - \n * TCP: 22 \n * TCP: 22   | prefix-jump-box-001 VSI  |
| network-services-sg | * IBM Inbound `161.26.0.0/16` \n * `10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16`  | * ALL: - \n * ALL: -   | prefix-network-services-001 VSI, load balancer, mount share targets  |
| vpe-sg | * IBM Inbound 161.26.0.0/16 \n * `10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16`   | * ALL: - \n * ALL: -   | Cloud Object storage  |
{: caption="Table 3. SG rules" caption-side="bottom"}

## Private networks
{: #landing-zone-private-networks}

The following table lists the private networks that are created in Edge VPC that are created by the deployment automation with corresponding default values. 

| Subnet Name | Private network | IP address ranges |
| ---| --- | --- |
| prefix-edge-vpn-zone-1 | Private network for VPN server | 10.30.10.0/24 |
| prefix-edge-vsi-management-zone-1| Management network for Bastion virtual server instance | 10.30.20.0/24 |
| prefix-edge-vpe-zone-1| Private network for Cloud Object storage VPE | 10.30.30.0/24 |
| prefix-edge-vsi-edge-zone-1| Private network for Network services VSI. This subnet has public gateway enabled. | 10.30.40.0/24 |
{: caption="Table 4. Private networks IP address ranges" caption-side="bottom"}
