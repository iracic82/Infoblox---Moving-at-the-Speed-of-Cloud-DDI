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

The integration of Generative AI into healthcare workflows is rapidly accelerating. Doctors, clinicians, and researchers are using AI to:
 - Summarize clinical notes
 - Draft care plans
 - Analyze symptoms or diagnostics

However, this also introduces new risk vectors — including uncontrolled DNS traffic, third-party API usage, and exposure to unvetted data sources.

# Use Case Story: Dr. Claire

Meet Dr. Claire, a busy pediatrician. She uses an internal web-based assistant to:
 - Ask medical questions like “What are common asthma triggers in children?”
 - Upload notes for summarization
 - Pull references from drug or symptom databases

Behind the scenes, this app uses AWS Bedrock with Claude to generate intelligent responses.

But there’s a hidden challenge:
 - What happens when the app tries to resolve domains like `ai-medicine-data.info`?
 - Or connects to third-party APIs over DNS?
 - Or leaks sensitive lookup patterns?

This is where Infoblox DNS Security plays a critical role.

# DNS Security for GenAI

Even in secure cloud environments, AI apps and LLMs introduce DNS-layer activity:
 - Flask-based apps resolve endpoints like `bedrock-runtime.amazonaws.com`
 - LLM responses often include external medical URLs
 - Optional third-party lookups may target unapproved or risky domains

Infoblox Threat Defense provides:
 - Allow-lists and domain policy control
 - Detection of suspicious DNS behavior (e.g., entropy, volume, or tunneling)
 - Real-time enforcement (RPZ, TIDE-based blocking)


# Business Value

Without DNS-layer enforcement, GenAI apps are opaque and vulnerable.
 With Infoblox:
 - Security teams gain real-time visibility and control
 - AI access is restricted to approved sources
 - Threats like DNS tunneling, data leaks, or typosquatting are neutralized
 - AI adoption becomes safe and compliant in regulated sectors like healthcare



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

2.	Enter the AWS Account ID, AWS IAM username, and password by copying and pasting the values from the section below.

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

🧱 Deploying the Lab Infrastructure

Now that you’ve logged into both cloud consoles, it’s time to deploy the infrastructure that reflects the architecture shown in the lab diagram.

👉 Switch back to the “>_ Shell” tab in the left-side panel of your Instruqt lab to proceed.

### 1. Deploy AWS resources in EU

Apply the resources:

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform apply --auto-approve  -target=module.aws__instances_eu -target=aws_vpn_gateway.vgw
```

## 4) Enable Amazon Bedrock Model Access in AWS Console
===

☁️ Simulated Bedrock Integration (Lab Setup)

> [!IMPORTANT]
> Note: The steps in this section are titled “Enable Amazon Bedrock Model Access in AWS Console” to mirror real-world configuration. However, in this lab environment, we use a simulated (mock) API endpoint instead of provisioning actual Bedrock access.

The Flask backend is built to integrate with the real AWS Bedrock API (e.g., using boto3 or API Gateway for InvokeModel calls), but for demo purposes:
	•	✅ No AWS credentials or real Bedrock services are required
	•	🧪 Mock responses mimic real GenAI output
	•	🔍 DNS queries simulate real-world behavior for AI-enhanced domains

This approach allows us to effectively demonstrate DNS inspection, threat detection, and policy enforcement via Infoblox, without the overhead of real AWS Bedrock configuration.



## 5) Create Admin User to your Infoblox Portal Dashboard
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


![Screenshot 2025-04-01 at 11.03.20.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/bdbf322902db478154c3fece79237f86/assets/Screenshot%202025-04-01%20at%2011.03.20.png)

---

### Section 2

✅ Existing User

1.	Go to Infoblox Portal TAB on the left.
2.	Login using your existing email address and password.
3.	Once authenticated, the lab tenant will be automatically added to your list of available tenants (you’ll see it in the top-right tenant switcher).

![Screenshot 2025-07-03 at 11.19.07.png](https://play.instruqt.com/assets/tracks/ywozzymyekgv/93f17f66e50b5a58f68e3e3d3953396a/assets/Screenshot%202025-07-03%20at%2011.19.07.png)

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
