---

copyright:
  years: 2024
lastupdated: "2024-07-02"

keywords: Power Virtual Server, Security and Compliance Center Workload Protection
subcollection: powervs-vpc
content-type: tutorial
services: power-iaas, security-compliance, vpc, virtual-servers
account-plan: paid
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.sysdigsecure_full_notm}} on {{site.data.keyword.powerSys_notm}}
{: #solution-scc-wp-on-powervs}
{: toc-content-type="tutorial"}
{: toc-services="power-iaas, security-compliance, vpc, virtual-servers"}
{: toc-completion-time="2h"}

This tutorial shows how to set up {{site.data.keyword.sysdigsecure_full_notm}} on {{site.data.keyword.powerSys_notm}} and {{site.data.keyword.vsi_is_short}}.
{: shortdesc}


## Objectives
{: #solution-scc-wp-on-powervs-objectives}

[{{site.data.keyword.sysdigsecure_full_notm}}](/docs/workload-protection?topic=workload-protection-getting-started) can be used to find and prioritize software vulnerabilities, detect and respond to threats, manage configurations, permissions, and compliance from source to run. It can be used to secure containers, Kubernetes, {{site.data.keyword.redhat_openshift_notm}}, and hosts with rapidly integrated runtime security, container forensics and incident response, so you can better understand security breaches and your compliance needs.

{{site.data.keyword.IBM}} Power is a family of high-performance servers that are designed for running large-scale data-driven and mission-critical workloads. They are known for their scalability, reliability, sustainability, and performance. {{site.data.keyword.powerSys_notm}} is a Power Systems offering in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.powerSysShort}}s are located in the {{site.data.keyword.IBM_notm}} data centers, distinct from the {{site.data.keyword.cloud_notm}} servers with separate networks and direct-attached storage. The internal networks are fenced but offer connectivity options to {{site.data.keyword.cloud_notm}} infrastructure or on-premises environments. This infrastructure design enables {{site.data.keyword.powerSysShort}}s to maintain key enterprise software certification and support as the {{site.data.keyword.powerSysShort}} architecture is identical to certified on-premises infrastructure.

[{{site.data.keyword.vsi_is_full}}](/docs/vpc?topic=vpc-about-advanced-virtual-servers) is an Infrastructure-as-a-Service (IaaS) offering that gives you access to the benefits of {{site.data.keyword.vpc_short}}, including network isolation, security, and flexibility.

This tutorial documents the steps to set up {{site.data.keyword.sysdigsecure_full_notm}} on {{site.data.keyword.powerSys_notm}} and {{site.data.keyword.vsi_is_short}}.

![Architecture](images/scc-wp-on-powervs-flow.svg){: caption="Architecture diagram of the tutorial" caption-side="bottom"}
{: style="text-align: center;"}


This tutorial covers the following aspects:
   1. The user provisions a {{site.data.keyword.powerSys_notm}} environment by using a deployable architecture that's offered in {{site.data.keyword.cloud_notm}}.
   2. The user creates {{site.data.keyword.sysdigsecure_full_notm}} instance.
   3. The user sets up {{site.data.keyword.powerSys_notm}} agents on {{site.data.keyword.vsi_is_short}}.
   4. The user set up {{site.data.keyword.powerSys_notm}} agents on {{site.data.keyword.powerSys_notm}}.
   5. The user monitors the environment by using {{site.data.keyword.powerSys_notm}}. The user can also monitor the environment with {{site.data.keyword.cloud_notm}} monitor, which integrates with {{site.data.keyword.sysdigsecure_full_notm}}


* [Set up your {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-account-getting-started).
* Make sure that you have the following access roles to create a project and permission to create the project tool resources within the account:
    - The Editor role on the {{site.data.keyword.cloud_notm}} Projects service.
    - The Editor and Manager role on the {{site.data.keyword.bpfull}}
    - The Viewer role on the resource group for the project
    - For more information about access and permissions, see [Assigning users access to projects](/docs/secure-enterprise?topic=secure-enterprise-access-project).

* Set up an authentication method. You can either use a Secrets Manager to manage API keys, or use Trusted Profiles to manage permission.
    - For more information, see [Using an API key with Secrets Manager to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-authorize-project).
    - For more information, see [Using trusted profiles to authorize a project to deploy an architecture](/docs/secure-enterprise?topic=secure-enterprise-tp-project).


## Provision {{site.data.keyword.powerSys_notm}} environment in {{site.data.keyword.cloud_notm}}
{: #solution-scc-wp-on-powervs-1}
{: step}

First, use a deployable architecture that's offered in {{site.data.keyword.cloud_notm}} is to set up the {{site.data.keyword.powerSys_notm}} environment.

### Provision {{site.data.keyword.powerSys_notm}} with {{site.data.keyword.powerSys_notm}} Quickstart DA
{: #solution-scc-wp-on-powervs-1-1-pvs-da}

1. In the {{site.data.keyword.cloud_notm}} console, go to the [{{site.data.keyword.cloud_notm}} catalog](/catalog) and search for the **Power Virtual Server with VPC landing zone** deployable architecture.
1. Use {{site.data.keyword.powerSys_notm}} quickstart variation to set up environment and {{site.data.keyword.powerSys_notm}} instance. For more information, see [Deploying a Power Virtual Server with VPC landing zone deployable architecture](/docs/powervs-vpc?topic=powervs-vpc-deploy).
1. You need to fill in the parameters exposed by the deployable architecture. On the 'Security' tab, you can either use an [API key](/docs/secure-enterprise?topic=secure-enterprise-authorize-project) or a [trusted profile](/docs/secure-enterprise?topic=secure-enterprise-tp-project).
   1. To create API key: Go to **Manage** > **Access**, and click **API keys**.
   1. To create a trusted profile, Go to **Manage** > **Access**, and click **Trusted profiles**. After the trusted profile is created, make sure that you add the project by going to the {{site.data.keyword.cloud_notm}} services tab.
1. On the 'Required' parameter tab for the deployment architecture, fill in other parameters based on your need. For the 'tshirt_size' field, you can choose the OS type and size based on your need. In this case, since {{site.data.keyword.sysdigsecure_full_notm}} supports Linux, let’s create a Linux virtual server with RHEL 9.2 image. Pick 'Custom' for 'tshirt_size' field, and we need to specify the other details of the VM in fields on the 'Optional' tab. On the 'Optional' tab, choose ‘Linux - RHEL9-SP2’ for ‘custom_profile_instance_boot_image’, and use the following json snippet for the ‘custom_profile’ field. You can adjust the input (for example, the number of cores or size of memory) based on your requirements.

   ```bash
   {
      "sap_profile_id": null,
      "cores": "1",
      "memory": "2",
      "server_type": "s922",
      "proc_type": "shared",
      "storage": {
         "size": "",
         "tier": ""
      }
   }
   ```
   {: da-param}

1. Next, save and validate the configuration.
1. After the configuration passes validation, you can approve and deploy it. The environment is deployed automatically.
   As you can see from the [{{site.data.keyword.powerSys_notm}} deployable architecture](/docs/powervs-vpc?topic=powervs-vpc-deploy-arch-ibm-pvs-inf-standard-plus-vsi), an Edge VPC and {{site.data.keyword.powerSys_notm}} workspace are created. In Edge VPC, it creates bastion host in the management security group, and a proxy server in the network service security group, both with Linux RHEL. It also creates a {{site.data.keyword.powerSys_notm}} instance in the {{site.data.keyword.powerSys_notm}} workspace with RHEL 9.2. Other necessary components to connect {{site.data.keyword.powerSys_notm}} workspace with {{site.data.keyword.cloud_notm}} resources and secure the environment are also created, for example, Transit Gateway, VPN, VPE, and so on.

### {{site.data.keyword.powerSys_notm}} Quickstart post setup
{: #solution-scc-wp-on-powervs-1-2-pvs-post-da}

Make sure to follow the [ Quickstart next steps](/docs/powervs-vpc?topic=powervs-vpc-solution-quickstart-next-steps) to allow the {{site.data.keyword.powerSys_notm}} instance to access the internet and mount nfs drive.
{: note}

1. Add proxy settings in /etc/bashrc. Locate the <proxy_host_or_ip_port> value in the output section of the deployment, and add the following entries at the end of `/etc/bashrc` file:

   ```bash
   export http_proxy=http://<proxy_host_or_ip_port>:3128
   export https_proxy=http://<proxy_host_or_ip_port>:3128
   export HTTP_PROXY=http://<proxy_host_or_ip_port>:3128
   export HTTPS_PROXY=http://<proxy_host_or_ip_port>:3128
   export no_proxy=161.0.0.0/0,10.0.0.0/8
   ```

1. Next, add the following line in `/etc/dnf/dnf.conf`:

   ```bash
   proxy=http://10.30.40.4:3128
   ```
   {: da-post-dnf}

1. Mount the file storage from VPC on the {{site.data.keyword.powerSys_notm}} instance:

   ```bash
   mkdir /nfs
   mount <nfs_host_or_ip_path> /nfs
   ```
   {: da-post-mount-nfs}

1. Configure DNS on the {{site.data.keyword.powerSys_notm}} instance. Add the `dns_host_or_ip_path` value at the top in the /etc/resolv.conf file.

1. Add the port to the Squid proxy configuration.
   1. SSH to the jump server VSI, and then ssh to the network service VSI. You need to make the SSH private key available on the jump server to access the network service VSI. Make sure that the port, 6443, is added to the proxy. Open file /etc/squid/squid.conf, add 6443 to the end of the acl line if it is not there already.

      ```bash
      acl SSL_ports port 443 8443 6443
      ```
      {: da-post-squid-config}

1. Restart the Squid proxy service.

      ```bash
      systemctl restart squid
      ```
      {: da-post-squid-restart}



## {{site.data.keyword.sysdigsecure_full_notm}} setup
{: #solution-scc-wp-on-powervs-2}
{: step}

As mentioned in the last section, the {{site.data.keyword.powerSys_notm}} Quickstart deployable architecture sets up 2 VSI instances in VPC and a {{site.data.keyword.powerSys_notm}} instance in {{site.data.keyword.powerSys_notm}} workspace. We can set up workload protection for all the virtual server instances.

[{{site.data.keyword.sysdigsecure_full_notm}} documentation](/docs/workload-protection?topic=workload-protection-getting-started) described the steps to set up SCC Workload Protection. Let's follow the step 1 and step 2 in this documentation to set up the {{site.data.keyword.sysdigsecure_full_notm}} instance. In the following sections, we will demonstrate how to config an agent on VPC/VSI and {{site.data.keyword.powerSys_notm}} instance.

Once the {{site.data.keyword.sysdigsecure_full_notm}} instance is created, we can collect the configuration information for the instance. We can either follow the instructions in this [document](/docs/workload-protection?topic=workload-protection-protecting-linux-hosts) or get the information from the {{site.data.keyword.sysdigsecure_full_notm}} dashboard. We will briefly describe both methods.

1. To collect the configuration from {{site.data.keyword.sysdigsecure_full_notm}} dashboard, click the **{{site.data.keyword.sysdigsecure_full_notm}}** instance. From the Get Connected section, click **Install the Agent** > **Edit Sources**. From here, the commands to run are listed. It has the access key and endpoint. It's recommended to use the private endpoint.

1. Collect the configuration by using {{site.data.keyword.cloud_notm}} documentation:
   1. To get the access key, click the **{{site.data.keyword.sysdigsecure_full_notm}}** instance. Next, click **Actions** > **Manage key**. Click **show key** to view the key.
   1. Select the ingestion URL from [Collector endpoints](/docs/workload-protection?topic=workload-protection-endpoints#endpoints_ingestion). It's recommended to use the private endpoint URL.
   1. Select the API endpoint URL from the [Workload Protection API](https://cloud.ibm.com/apidocs/workload-protection#endpoint-url){: external}. It's recommended to use the private endpoint.

For this example, the {{site.data.keyword.sysdigsecure_full_notm}} instance is in Dallas. The following configuration information is used for the following sections:

```bash
ACCESS_KEY=your_access_key
COLLECTOR_ENDPOINT=ingest.private.us-south.monitoring.cloud.ibm.com
API_ENDPOINT=private.us-south.security-compliance-secure.cloud.ibm.com
```

## Protecting VSI for VPC
{: #solution-scc-wp-on-powervs-3}
{: step}

The {{site.data.keyword.powerSys_notm}} Quickstart deployable architecture sets up the jump server and network service VSIs for VPC with Linux RHEL in Edge VPC. We can install the agents on both of them.

{{site.data.keyword.sysdigsecure_full_notm}} provides the following features to protect your stand-alone Linux hosts:
* Threat detection: Identify threats and suspicious activity based on application, network, and host activity by processing syscall events and investigate with detailed system captures.
* Posture management: scan host configuration files for compliance and benchmarks such as CIS Linux Benchmark.
* Host scanning: scan host packages, detect the associated vulnerabilities and identify the resolution priority based on available fixed versions and severity.

For more information, see [Protecting Linux hosts](/docs/workload-protection?topic=workload-protection-protecting-linux-hosts).


### Install the threat detection agent
{: #solution-scc-threat-detection}

Next, let's install the agent on the VSI in Edge VPC by installing it on the jump server.

1. In the {{site.data.keyword.cloud_notm}}, go to the **VPC Infrastructure** > **Virtual server instances**. SSH to the jump server. Here is the sample command. Make sure to replace the private key file name and server IP in the command.

   ```bash
   ssh -i YOUR_PRIVATE_KEY_FILE root@YOUR_JUMP_SERVER_IP
   ```

1. Install the kernel headers:

   ```bash
   yum -y install kernel-devel-$(uname -r)
   ```

1. Deploy the Workload Protection agent:

   ```bash
   curl -sL https://ibm.biz/install-sysdig-agent | sudo bash -s -- --access_key $ACCESS_KEY --collector $COLLECTOR_ENDPOINT --collector_port 6443 --secure true --additional_conf 'sysdig_capture_enabled: false\nfeature:\n    mode: monitor_light'
   ```

1. Check that Workload Protection agent is running:

   ```bash
   ps -ef | grep sysdig
   ```

### Identifying vulnerabilities with Host Analyzer
{: #solution-scc-wp-host-analyzer}

Complete the following steps to install the Host on RHEL. For more information, see [Vulnerability Host Scanner installation](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/hosts/packages/vulnerability-host-scanner/#installation){: external}.

1. For RPM-based (Red Hat Package Manager) operating systems such as Red Hat Enterprise Linux or SUSE Linux Enterprise, we need to
configure the RPM repository and Sysdig GPG key:

   ```bash
   sudo rpm --import https://download.sysdig.com/DRAIOS-GPG-KEY.public
   sudo curl -o /etc/yum.repos.d/draios.repo https://download.sysdig.com/stable/rpm/draios.repo
   ```

2. Install the vuln-host-scanner package:

   ```bash
   sudo yum clean expire-cache && sudo yum install vuln-host-scanner -y
   ```

3. Create the vuln-host-scanner configuration file. Make sure the access-key and api-url are set.

   ```bash
   cat << EOF | sudo tee /opt/draios/etc/vuln-host-scanner/env
   SYSDIG_ACCESS_KEY=$ACCESS_KEY
   SYSDIG_API_URL=https://$API_ENDPOINT/api
   # optional
   SCAN_ON_START=true
   EOF
   ```

4. Enable and start the vuln-host-scanner.service service:

   ```bash
   sudo systemctl enable --now vuln-host-scanner.service
   ```

5. Check the logs to see ensure that everything is working:

   ```bash
   sudo journalctl -fu vuln-host-scanner.service
   ```

### Posture management
{: #solution-scc-wp-on-powervs-3-3-posture-management}

To protect linux host, you need to run the Kubernetes Security Posture Management (KSPM) analyzer as a container. Rather than running it using docker, we will use Podman. For more information, see [Protecting Linux hosts](/docs/workload-protection?topic=workload-protection-protecting-linux-hosts).

1. Install Podman:

   ```bash
   dnf install podman
   ```

1. Install the Kubernetes Security Posture Management (KSPM) analyzer in a nonkubernetes environment:

   ```bash
   podman run -d -v /:/host:ro -v /tmp:/host/tmp --privileged --network host --pid host --env ACCESS_KEY=$ACCESS_KEY --env API_ENDPOINT=$API_ENDPOINT quay.io/sysdig/kspm-analyzer:latest
   ```

In this section, the {{site.data.keyword.sysdigsecure_full_notm}} agents have been set up on the Linux jump server. You can repeat the steps on the network service VSI.

## Protecting Linux host on {{site.data.keyword.powerSys_notm}}
{: #solution-scc-wp-on-powervs-4}
{: step}

When we run the {{site.data.keyword.powerSys_notm}} Quickstart deployable architecture, we create a {{site.data.keyword.powerSys_notm}} instance with Linux RHEL 9.2. We can set up the {{site.data.keyword.sysdigsecure_full_notm}} on the {{site.data.keyword.powerSys_notm}} instance. For more information, see [Managing the Workload Protection agent in Linux on PowerVS](/docs/workload-protection?topic=workload-protection-agent-deploy-linux-powervs).


### Install threat detection agent
{: #solution-scc-wp-on-powervs-4-1-scc-wp-threat-detection}

Next, let's install the threat detection agent.

1. Install dkms

   ```bash
   sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
   sudo yum install dkms
   ```

2. Enabled the extended Berkeley Packet Filter (eBPF). Add the following line to the end of the `/etc/sysconfig/dragnet`.

   ```bash
   SYSDIG_AGENT_DRIVER=universal_ebpf
   ```

3. Trust the GPG key and configure the yum repository

   ```bash
   sudo rpm --import https://download.sysdig.com/DRAIOS-GPG-KEY.public && sudo curl -s -o /etc/yum.repos.d/draios.repo https://download.sysdig.com/stable/rpm/draios.repo
   ```

4. Install the agent package

   ```bash
   sudo yum -y install draios-agent
   ```

5. Update the agent yaml file, where `ACCESS_KEY` and `COLLECTOR_ENDPOINT` are the values from section 3.2.1. For this tutorial, the proxy information is added to the agent yaml file. Proxy information can be found in the outputs section of the configuration.

   ```bash
   echo customerid: $ACCESS_KEY >> /opt/draios/etc/dragent.yaml
   echo collector: $COLLECTOR_ENDPOINT >> /opt/draios/etc/dragent.yaml
   ```

   Review the following complete /opt/draios/etc/dragnet.yaml file.

   ```bash
   # cat /opt/draios/etc/dragent.yaml
   customerid: $ACCESS_KEY
   collector: $COLLECTOR_ENDPOINT
   http_proxy:
   proxy_host: 10.30.40.4
   proxy_port: 3128
   ```

6. Enable the agent

   ```bash
   sudo systemctl enable dragnet
   ```

7. Start the agent

   ```bash
   sudo systemctl start dragnet
   ```

8. If the agent does not start correctly, check the log file for errors.

   ```bash
   grep -i error /opt/draios/logs/draios.log
   ```

### Identifying vulnerabilities in Linux host on {{site.data.keyword.powerSys_notm}}
{: #solution-scc-wp-on-powervs-4-2-scc-wp-host-analyzer}

Now, let’s set up the vulnerability scanning component, which can detect all installed packages and associated vulnerabilities that are sorted by severity and prioritizing those with a fix available.

1. Download the binary

   ```bash
   curl -LO https://download.sysdig.com/scanning/bin/sysdig-host-scanner/$(curl -L -s https://download.sysdig.com/scanning/sysdig-host-scanner/latest_version.txt)/linux/ppc64le/sysdig-host-scanner
   ```

2. Set the executable flag on the file

   ```bash
   chmod +x ./sysdig-host-scanner
   ```

3. Start the Host Scanner

   ```bash
   SYSDIG_ACCESS_KEY=$ACCESS_KEY SYSDIG_API_URL=https://$API_ENDPOINT SCAN_ON_START=true ./sysdig-host-scanner
   ```

4. Create an environment file to store the configuration and a systemd unit file to run the binary as a service. Make sure that  <access key> and <api-url> are set.

   ```bash
   sudo mv ./sysdig-host-scanner /usr/local/bin/vuln-host-scanner
   sudo restorecon -Rv /usr/local/bin/vuln-host-scanner
   sudo mkdir -p /opt/draios/etc/vuln-host-scanner/

   cat << EOF | sudo tee /opt/draios/etc/vuln-host-scanner/env
   SYSDIG_ACCESS_KEY=$ACCESS_KEY
   SYSDIG_API_URL=https://$API_ENDPOINT/api
   SCAN_ON_START=true
   EOF

   cat << EOF | sudo tee /etc/systemd/system/vuln-host-scanner.service
   [Unit]
   Description=Sysdig Vuln Host Scanner component

   [Service]
   EnvironmentFile=/opt/draios/etc/vuln-host-scanner/env
   ExecStart=/usr/local/bin/vuln-host-scanner

   [Install]
   WantedBy=multi-user.target
   EOF

   sudo systemctl daemon-reload
   sudo systemctl enable --now vuln-host-scanner.service
   ```

5. Control Host Scanner by using the service vul-host-scanner

   ```bash
   systemctl status vuln-host-scanner
   ```

### Posture management
{: #solution-scc-wp-on-powervs-4-3-scc-wp-posture-management}

Run the Kubernetes Security Posture Management (KSPM) analyzer as a container or posture management. For this tutorial, let's use Podman.

1. Install Podman

   ```bash
   dnf install podman
   ```

2. Install Kubernetes Security Posture Management (KSPM) analyzer in a nonkubernetes environment

   ```bash
   podman run -d -v /:/host:ro -v /tmp:/host/tmp --privileged --network host --pid host --env ACCESS_KEY=$ACCESS_KEY --env API_ENDPOINT=$API_ENDPOINT quay.io/sysdig/kspm-analyzer:latest
   ```

Next, let's set up the {{site.data.keyword.sysdigsecure_full_notm}} in Linux host on {{site.data.keyword.powerSys_notm}}.


## Monitoring with {{site.data.keyword.sysdigsecure_full_notm}}
{: #solution-scc-wp-on-powervs-5}
{: step}

{{site.data.keyword.sysdigsecure_full_notm}} can be used to find and prioritize software vulnerabilities, detect and respond to threats, and manage configurations, permissions, and compliance from source to run.

1. From the {{site.data.keyword.cloud_notm}} console, go to the Resource list. You should be able to see the {{site.data.keyword.sysdigsecure_full_notm}} instance from the Security section.
1. Select the instance name and click **Open dashboard**

{{site.data.keyword.sysdigsecure_full_notm}} is configured for Host Scanning, posture management, and threat detection response.

### Host scanning
{: #solution-scc-wp-on-powervs-5-1-scc-wp-host-scanning}

Host scanning can be used to find and prioritize software vulnerabilities.

1, After you open {{site.data.keyword.sysdigsecure_full_notm}}, click  **Vulnerabilities** >  and then click **Runtime**. You can see the systems that are being scanned.
1. Click the instance name to review the details. From the Vulnerabilities page, you can filter by various criteria, for example, filter by ‘Has fix’.
1. You can download a PDF report, or you can click **Vulnerabilities** > **Reporting** to build the report.

### Posture management
{: #solution-scc-wp-on-powervs-5-2-scc-wp-posture-management}

To explore posture management, click **Posture** > **Compliance**. You can also click
**Inventory** and check the posture for each inventory item.

### Threat detection
{: #solution-scc-wp-on-powervs-5-3-scc-wp-thread-detection}

* For Threat detection, you can look at Integrations -> Sysdig Agents.

* You can also look at Events -> Host and Container Events.


## Monitoring with {{site.data.keyword.monitoringfull_notm}}
{: #solution-scc-wp-on-powervs-6}
{: step}

{{site.data.keyword.monitoringfull_notm}} is also integrated with Sysdig and has information on the dashboard.

* From the Logging and monitoring section in the Resource list, you can find the {{site.data.keyword.cloud_notm}} Monitoring instance if it's enabled. Click the instance to ensure that it's connected with the Workload Protection.

* You can click the ‘Open dashboard’ button and explore the {{site.data.keyword.cloud_notm}} Monitor dashboard. Click ‘All Workloads’ dropdown on the top of the page, and in our case, we can choose ‘Hosts & Containers’. You can see the 3 hosts in the environment and you can explore various information in the environment.

## Remove resources
{: #solution-scc-wp-on-powervs-7}
{: step}

If you want to remove the resources that were created in this tutorial, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}}, go to the **Navigation menu** icon ![Navigation Menu icon](../icons/icon_hamburger.svg "Menu") and select **[Projects](/projects/)**.
1. Clean up any resources created outside the deployable architecture in the same environment before proceeding to the next step, otherwise the undeploy may fail. For example, if you have created a Virtual Private Endpoint (VPE) in the same VPE, you need to make sure it is deleted before you proceed. In this tutorial, we did not create any extra resource, so you can proceed to the next step.
1. Go to the Configurations tab, and click **Undeploy** from the dropdown list. This action removes the resources that are deployed by the deployable architecture.
