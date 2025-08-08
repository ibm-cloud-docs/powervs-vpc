---

copyright:
   years: 2023, 2025
lastupdated: "2025-08-08"

keywords:

subcollection: powervs-vpc

---

{{site.data.keyword.attribute-definition-list}}

# VPC landing zone architecture for {{site.data.keyword.powerSys_notm}}
{: #landing-zone-preset}

The {{site.data.keyword.powerSys_notm}} with VPC landing zone makes use of [Terraform IBM Module - VPC Landing Zone](https://github.com/terraform-ibm-modules/terraform-ibm-landing-zone){: external}.


As part of the automation an [override json preset](https://github.com/terraform-ibm-modules/terraform-ibm-powervs-infrastructure/blob/main/modules/powervs-vpc-landing-zone/presets/slz-preset.json.tftpl) is passed to this module. The JSON preset defines which VPC components are created.


| Resource Type | Optional | Description |
|---|---|---|
|  VPC |  |  Edge VPC: ACL, SGs, SSH Key and 4 Subnets |
|  Intel VSI |  | Jump box with 2 cores, 4GB memory running RHEL 9.4 with floating IP attached |
|  Intel VSI |  | Network Services running RHEL 9.4 configured as squid proxy, NTP and DNS servers(using Ansible Galaxy collection roles [IBM Power Linux for SAP](https://galaxy.ansible.com/ui/repo/published/ibm/power_linux_sap/)). Also configured as central ansible execution node. Default size is 2 cores and 4 GB memory. Can be customized. |
| Intel VSI | Yes | Monitoring Host running SLES 15SP5 to collect metrics and forward it to IBM Monitoring Instance |
| Virtual Private Endpoint Gateway|  | A [Virtual Private Endpoint Gateway](/docs/vpc?topic=vpc-about-vpe) to reach the Cloud Object Storage bucket |
| Flow Logs for VPC|  | [Flow Logs for VPC](/docs/vpc?topic=vpc-flow-logs) enables the collection, storage, and presentation of information about the Internet Protocol (IP) traffic going to and from network interfaces within your VPC|
{: class="landing-zone-table"}
{: tab-group="landing-zone"}
{: #landing-zone-1}
{: tab-title="VPC"}
{: caption="VPC Landing Zone Components" caption-side="bottom"}

| Resource Type | Optional | Description |
|---|---|---|
| Key Protect |  | [Key Protect](/docs/key-protect) provides key management by integrating the IBM Key Protect for IBM Cloud service. These key management services help you create, manage, and use encryption keys to protect your sensitive data |
| Transit Gateway |  | Global or local [Transit Gateway](/docs/transit-gateway) to interconnect VPC and {{site.data.keyword.powerSys_notm}} workspace |
| Cloud Object Storage | |  [Cloud Object Storage](/docs/cloud-object-storage) instance, buckets and credentials are created |
{: class="landing-zone-table"}
{: tab-group="landing-zone"}
{: #landing-zone-2}
{: tab-title="Cloud Service"}
{: caption="VPC Landing Zone Components" caption-side="bottom"}

## ACL
{: #landing-zone-acl}

The ACL rules for the Edge VPC allow all traffic.

### Inbound rules
{: #landing-zone-acl-inbound}

| Priority | Allow or deny | Protocol | Source | Destination |
|----------|------------|----------|--------|-------------|
| 1 | Allow | ALL | ANY IP | ANY IP  |
{: caption="Inbound ACL rules" caption-side="bottom"}

### Outbound rules
{: #landing-zone-acl-outbound}

| Priority | Allow or deny | Protocol | Source | Destination |
|----------|------------|----------|--------|-------------|
| 1 | Allow | ALL | ANY IP | ANY IP  |
{: caption="Outbound ACL rules" caption-side="bottom"}

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
{: caption="SG rules" caption-side="bottom"}

## Private networks
{: #landing-zone-private-networks}

The following table lists the private networks that are created in Edge VPC that are created by the deployment automation with corresponding default values.

| Subnet Name | Private network | IP address ranges |
| ---| --- | --- |
| prefix-edge-vpn-zone-1 | Private network for VPN server | 10.30.10.0/24 |
| prefix-edge-vsi-management-zone-1| Management network for Bastion virtual server instance | 10.30.20.0/24 |
| prefix-edge-vpe-zone-1| Private network for Cloud Object storage VPE | 10.30.30.0/24 |
| prefix-edge-vsi-edge-zone-1| Private network for Network services VSI. This subnet has public gateway enabled. | 10.30.40.0/24 |
{: caption="Private networks IP address ranges" caption-side="bottom"}

## Additional Resources
{: #landing-zone-additional-resources}

The following table provides an overview over cloud services which are created in addition to those handled by the VPC landing zone module.

| Resource Type | Optional | Description |
|---|---|---|
| {{site.data.keyword.monitoringfull_notm}} | Yes | [{{site.data.keyword.monitoringshort}}](/docs/monitoring?topic=monitoring-about-monitor) collects metrics to provide a web UI to monitor the performance and overall system health of the deployment. Interconnects with {{site.data.keyword.sysdigsecure_full_notm}} if used. |
| {{site.data.keyword.sysdigsecure_full_notm}} | Yes | [{{site.data.keyword.sysdigsecure_short}}](/docs/workload-protection?topic=workload-protection-key-features#feature_1) can be used to find and prioritize software vulnerabilities, detect and respond to threats, manage configurations, permissions, and compliance from source to run. Interconnects with {{site.data.keyword.monitoringshort}} if used. |
| Client to site VPN Server,\nSecrets Manager | Yes | [Client to site VPN Server](/docs/vpc?topic=vpc-vpn-client-to-site-overview) provides client-to-site connectivity, which allows remote devices to securely connect to the VPC network using an OpenVPN software client.\n [Secrets Manager](/docs/secrets-manager) Instance is deployed along with VPN to store the VPN Certificate |
| File storage share,\n Network load balancer | Yes | [NFS as a Service](/docs/vpc?topic=vpc-file-storage-create&interface=ui)\n [Network Load Balancer](/docs/vpc?group=network-load-balancer) is deployed along with File storage share to access the share IP from Power Virtual Server |
{: caption="Additional Cloud Services" caption-side="bottom"}
