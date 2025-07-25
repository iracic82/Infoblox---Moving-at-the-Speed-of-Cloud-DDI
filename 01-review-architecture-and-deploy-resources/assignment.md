---
slug: review-architecture-and-deploy-resources
id: it0azjuzt7ns
type: challenge
title: Review Architecture and Deploy Resources
teaser: Review Architecture and Deploy Resources
notes:
- type: video
  url: https://cdn.instruqt.com/assets/instruqt/2024-036%20Instruqt%20101_Version%203.0.mp4
tabs:
- id: 2ojdtqeja38h
  title: Shell
  type: terminal
  hostname: shell
- id: 7fcaonvk6sph
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: 5ddgbuv56am5
  title: AWS Console
  type: browser
  hostname: aws
- id: wkwumnvqzn7y
  title: Infoblox Portal
  type: browser
  hostname: infoblox
- id: znoyhjpjes3e
  title: Lab Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
# Overview

CloudOps and NetOps teams today are under constant pressure to deliver core network services DNS, DHCP, and IPAM (DDI)  at the same  pace of cloud and application teams.Providing DNS manually via virtual appliances no longer scales — especially in environments where cost optimization and operational simplicity are paramount.

Enter Infoblox NIOS X-as-a-Service: a fully managed DNS and security service that plugs directly into cloud networks — no VMs, no patching, no operational overhead. Just fast, scalable, policy-aligned DNS as a service.

> [!IMPORTANT]
> NOTE: We offer DDI full package but in this lab the focus stays on core components relvant to the scenario at hand.



# Use Case Story: CloudOps at Speed

Meet Jenna, a CloudOps engineer at a global enterprise. Her team is deploying a new application in  AWS region as part of a global product expansion. This region includes:
- A newly provisioned VPC and VPN
- EC2 workloads requiring immediate name resolution
- DNS and DNS security policies already defined in Infoblox Universal DDI

The networking team — led by Max — is aligned on one principle: no more spinning up virtual appliances just to deliver DNS. The operational burden, patching schedules, and cloud cost models have forced them to look for a SaaS solution that just plugs in and works.


Here’s the challenge:
- The landing zone needs to go live today
- DNS must be secured and compliant — immediately
- The solution must be cloud-native, cost-efficient, and ops-free

That’s exactly what NIOS X-as-a-Service delivers.

# DDI in Minutes — Without the Baggage

Using the Infoblox SaaS control plane, the  Infoblox Portal,  Jenna:
- Instantiates a new deploy of NIOS-XaaS service using existing DNS and security profiles
- Connects it to the AWS VPC in minutes — no agents, no appliances
- Validates DNS resolution and security policy enforcement directly from a test EC2 instance

Infoblox Universal DDI and  Threat Defense provides:
- ✅ Enterprise-grade DNS in the cloud — without running infrastructure
- ✅ Real-time enforcement using[RPZs](https://www.infoblox.com/dns-security-resource-center/dns-security-solutions/dns-security-solutions-response-policy-zones-rpz/) and curated threat intel
- ✅ Operational consistency across on-prem, Azure, GCP and AWS — all from a single SaaS control plane



# Business Value

Without a SaaS-based DNS and security model:
- Teams are stuck managing virtual appliances and patching cycles
- Cloud environments inherit fragmented, inconsistent DNS policies
- DNS becomes a silo — not a security control point

With Infoblox NIOS X-as-a-Service:
- DNS and security services are delivered at cloud speed — ops-free
- CloudOps and  NetOps converge around a single, managed DDI platform
- Centralized visibility, unified policy, and consistent enforcement just work — **with zero infrastructure burden**

⸻




> [!IMPORTANT]
> **NOTE:** This environment is *real*! AWS Cloud Accounts have been created for each student. No bitcoin mining, please! :)

In this section we will:
1) Review the cloud architecture
2) Login to your cloud account console's
3) Deploy resources onto your cloud regions
4) Create your Infoblox Portal user




---

## 1) Review Cloud Architecture
===

First lets review the cloud architecture that has been provision for your Infoblox Lab experience.

Navigate to the *Lab Diagram* tab above and review the diagram. This is what we're building today!




## 2) Login to your cloud account consoles
===

🔐 Access Instructions

Using the credentials below, log in to the AWS  Web Consoles.

---
# AWS Credentials ☁️

🔐 Logging In to the AWS Console.

👉 First, open the “AWS Console” tab on the left-hand side of your Instruqt lab environment. This will launch the AWS login page in a new browser panel.

![Screenshot 2025-07-12 at 11.23.29.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/86d80bec0e3af0161dbb62f6e26e2626/assets/Screenshot%202025-07-12%20at%2011.23.29.png)

Then follow these steps:
1.	Select “IAM Account”.
On the login screen, choose IAM Account (not root).

![Screenshot 2025-07-12 at 11.23.29.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/86d80bec0e3af0161dbb62f6e26e2626/assets/Screenshot%202025-07-12%20at%2011.23.29.png)

2.	Enter the AWS Account ID, AWS IAM username, and password by copying and pasting the values from the section below. Then, log in by clicking Sign In.

📝 Note: Avoid the root account login — this lab is configured for IAM users only.

**AWS Account ID**
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_ACCOUNT_ID" hostname="shell" ]]
```

**AWS Username**
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_USERNAME" hostname="shell" ]]
```

**AWS Password**
```
[[ Instruqt-Var key="INSTRUQT_AWS_ACCOUNT_INFOBLOX_DEMO_PASSWORD" hostname="shell" ]]
```
---


## 3) Deploy resources onto your cloud regions
===

🧱 Deploying the Lab Infrastructure: Your AWS Landing Zone Starts Here

You’ve logged into the AWS console — now it’s time to build out the cloud-side foundation for our lab. This simulates what you’d do when bringing up a new region or VPC that needs to connect into your existing DNS and security architecture.

The goal here isn’t to spin up the kitchen sink — it’s to deploy just enough to simulate real DNS resolution flow through Infoblox NIOS-X as a Service.


👉 Switch back to the “>_ Shell” tab in the left-side panel of your Instruqt lab to proceed.

---
### 1. Deploy AWS resources in EU

This command sets up the essential building blocks of your cloud-side lab environment:
•	A dedicated VPC and subnet to simulate your new region
•	An Internet Gateway to provide outbound connectivity
•	A VPN Gateway to establish a secure tunnel back to Infoblox
•	One EC2 instance that acts as your client — sending real DNS queries into the system


```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform apply --auto-approve  -target=module.aws__instances_eu -target=aws_vpn_gateway.vgw
```

Next, you’ll deploy the DNS infrastructure, including private zones and the necessary A records — exactly as shown in the lab diagram.

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform apply --auto-approve -target=aws_route53_zone.private_zone -target=aws_route53_record.dns_records
```
---

🪣 Deploying S3 for DNS Validation

To simulate DNS resolution and observe policy enforcement against web assets, you’ll deploy an S3 bucket and make it accessible via a custom DNS name.

Split this deployment into two phases to ensure resources are created in the correct order:

### Phase 1: Provision the S3 bucket and apply access restrictions
```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform apply --auto-approve \
  -target=aws_s3_bucket.infoblox_poc \
  -target=aws_s3_bucket_public_access_block.infoblox_poc
```

This creates a secure S3 bucket with public access restrictions — preventing unintended exposure while still allowing access via defined DNS.


### Phase 2: Attach the policy, upload a test object, and map it via DNS

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform apply --auto-approve \
  -target=aws_s3_bucket_policy.public_access \
  -target=aws_s3_object.uploaded_image \
  -target=aws_route53_record.s3_cname
```

🛠️ Terraform will take care of the heavy lifting — no console clicking or manual setup. Just wait for the process to finish.

---
✅ Once Complete

You now have a simulated cloud workload in place — an EC2 instance that will later send DNS queries through the IPsec tunnel to Infoblox NIOS-X as a Service.

🎯 Next step: Deploy NIOSX-as-a-Service, attach it to the VPC, and test DNS + security enforcement in action.

## 4) Create Admin User to your Infoblox Portal Dashboard
===


> [!NOTE]
> Note: Use your Business Email for User Creation

Your user account and sandbox have already been created. The next step is to set up your password and activate your account.

> [!IMPORTANT]
> NOTE: If your account has already been activated on the Infoblox Portal, please proceed to the password reset steps outlined in Section 2.

### Section 1

1. Please check the inbox of the email account you used to register for the Infoblox Lab.
2. You will receive an email with the subject “Infoblox User Account Activation.” Open this email and click on the “Activate Account” button to proceed.

![Screenshot 2025-04-01 at 11.15.44.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/93d7e021e28c20d105ca34aace35d149/assets/Screenshot%202025-04-01%20at%2011.15.44.png)

4. A new browser window or tab will open, prompting you to create a new password. Please enter your desired password to complete the setup.

![Screenshot 2025-04-01 at 11.19.01.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0fd5315d47a283fce641de81b289ac64/assets/Screenshot%202025-04-01%20at%2011.19.01.png)

5. Once you’ve set your password, close the newly opened tab or window. We’ll be logging in through the Instruqt tab labeled "Infoblox Portal".
6. In the Instruqt tab labeled "Infoblox Portal", log in using the credentials you set up in the previous steps.
7. After logging in, please mark the first window as shown in the example below. This confirms that you have successfully accessed the Infoblox Portal.

![Screenshot 2025-04-01 at 11.01.03.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/a082b5c7276e1c2e27eaaf7bee832089/assets/Screenshot%202025-04-01%20at%2011.01.03.png)

7. In the upper-left corner of the Infoblox Portal, click on the drop-down menu. Use the “Find Account” field to search for your sandbox by entering the "Sandbox-ID" shown below. It is important that you select your specific Sandbox-ID from the list and click on it to proceed.

**Your Sandbox ID**
```
[[ Instruqt-Var key="Sandbox_ID" hostname="shell" ]]
```

---

![Screenshot 2025-07-18 at 09.16.24.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/09e41ec1cf57a6f2cbe5d2c47721a26b/assets/Screenshot%202025-07-18%20at%2009.16.24.png)

---

### Section 2

✅ Existing User

1.	Go to Infoblox Portal TAB on the left.
2.	Login using your existing email address and password.
3.	Once authenticated, the lab tenant will be automatically added to your list of available tenants (you’ll see it in the top-right tenant switcher).

![Screenshot 2025-07-18 at 09.16.24.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/09e41ec1cf57a6f2cbe5d2c47721a26b/assets/Screenshot%202025-07-18%20at%2009.16.24.png)

In order to RESET the password follow the steps below:

1. Please navigate to the Infoblox Portal page by clicking on the Infoblox Portal tab within the Instruqt lab environment. This will direct you to the appropriate login interface.
2. Once you’re on the Infoblox Portal page, click on “Need Assistance” located at the bottom of the login form.

![Screenshot 2025-04-01 at 10.52.47.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/0bacd7dc4193c2770df54b65c7eceb3a/assets/Screenshot%202025-04-01%20at%2010.52.47.png)

3. After clicking on “Need Assistance”, select “Forgot Password” from the available options to initiate the password reset process.

![Screenshot 2025-04-01 at 10.52.57.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/3971464a872c428ee8879f3d7287b201/assets/Screenshot%202025-04-01%20at%2010.52.57.png)

4. You will receive an email with the subject “Account Password Reset.” Open this email and click on the “Reset Password” button to proceed with setting a new password.

![Screenshot 2025-04-01 at 11.42.21.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/263657baa43cefce4e8fc2062d2371f1/assets/Screenshot%202025-04-01%20at%2011.42.21.png)

5. Once you’ve set up your password, please return to "Section 1" of the instructions and continue from Step 4 onward.




## Time for the Next Challenge

Now we've inspected the playing field its game time. Click **NEXT**!
