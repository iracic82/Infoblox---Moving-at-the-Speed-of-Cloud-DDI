---
slug: manage-uddi
id: yqkosgouguty
type: challenge
title: Deploying and Activating Infoblox NIOSX-as-a-Service
teaser: Deploying Infoblox UDDI SaaS offering - DNS and Security Services Enabled
notes:
- type: video
  url: https://videos.infoblox.com/watch/TYegXjnJ2ocSZZyyaVAqTo?
tabs:
- id: ciejqrwmvf14
  title: Shell
  type: terminal
  hostname: shell
- id: bfkeoiybphpn
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: evzqhspieqiu
  title: AWS Console
  type: browser
  hostname: aws
- id: dif4gplkqnhc
  title: Infoblox Portal
  type: browser
  hostname: infoblox
- id: ohxmgt8tiywa
  title: LAB Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
🔧 Challenge Intro: Activating Infoblox NIOS X-as-a-Service

DNS is foundational — but in a multicloud world, managing and securing it across fragmented infrastructure can quickly become a liability.

In this challenge, you’ll activate Infoblox NIOS X-as-a-Service — a fully managed, cloud-delivered DNS platform operated by Infoblox. This is not a virtual appliance you deploy — it’s a zero-footprint SaaS model where Infoblox handles all the heavy lifting:
•	No VM provisioning
•	No patching
•	No scaling headaches

Just plug into it, and go.

![Screenshot 2025-07-03 at 20.28.27.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/b4d88e7b711cf18a0054479f3ecc8bea/assets/Screenshot%202025-07-03%20at%2020.28.27.png)



🚀 What You’ll Do

You’ll walk through the activation steps via the Infoblox Cloud Services Portal using the official guide:
Creating As-a-Service

Key actions include:
- Selecting your cloud region
- Assigning a service name
- Enabling DNS visibility and security services
- Connecting downstream sites or cloud VPCs

Once provisioned, your NIOS-X-as-a-service will act as a cloud-native DNS control plane for enforcing policy, inspecting queries, and managing DDI services globally — no infrastructure required.


![Screenshot 2025-07-03 at 20.29.32.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/e16bccc5da63c7678165476f470dbb07/assets/Screenshot%202025-07-03%20at%2020.29.32.png)

## 1) Login to your cloud account consoles
===

🔐 (Optional) Log in to Your Cloud Account Consoles.

You should already be signed in to the AWS  web console via the embedded tabs on the left-hand side of the Instruqt interface.

⚠️ Only perform this step if you’re logged out or the session has expired.

- Use the credentials provided in the lab instructions to sign in.
- If prompted for account type on AWS, select IAM Account.

---
# AWS Credentials ☁️

Select "IAM Account" and enter the **AWS ID**:
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


## 2) Deploying NIOS-X as a Service
===

# NIOS-X as a Service

NIOS-X-as-a-Service offers advanced cloud delivery for critical network services in hybrid, multi-cloud environments. It ensures operational efficiency and reliability by using public cloud points of presence across multiple regions, eliminating the need for physical or virtual appliances.
The industry’s most advanced DDI deployment model for hybrid, multi-cloud environments.

## Workflow
To enable and use NIOS-X-as-a-Service perform the following workflow:
1. Create a Service Deployment for NIOS-X as a Service.
2. Acquire the Identity string and Cloud Service IP from the Service Deployment.
3. Establish an IPsec tunnel between an AWS VPN and Infoblox(Re-Config).
4. Test/Verify the configuration.


> [!IMPORTANT]
> Note: Ensure all configurations follow the lab topology as shown in the diagram - Lab Tab. Use the AWS region eu-west-2 (London) for all resource deployments.



## 1. Create a Service Deployment on Infoblox CSP for NIOS-X as a Service.


This portion of the guide is intended to guide Infoblox Portal administrators through the creation of a Service
Deployment for NIOS-X-as-a-Service. The Service Deployment acts as the point of access for NIOS-X-as-a-
Service’s DNS, and DNS Security. To create a Service Deployment for NIOS-X-as-a-Service complete the
following steps:
1. Navigate to the As-A-Service page of the Infoblox Portal by highlighting **Configure,** clicking **Service Deployment**, then by clicking **As-A-Service** in the navigation panel.
![Jun-23-2025_at_21.47.25-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/ef250f39faaa4f82a041b5e648d6f017/assets/Jun-23-2025_at_21.47.25-image.png)
2. Click **Add Service** near the bottom left of the As-A-Service page.
![Jun-23-2025_at_21.48.01-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/60883e25c289b6db671ce943806ac912/assets/Jun-23-2025_at_21.48.01-image.png)
3.  Give the new Service a **Name**  : **Instrqt-SaaS**.

> [!IMPORTANT]
> NOTE: Service Name - Instrqt-SaaS

![Jun-23-2025_at_21.55.52-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f8f237f5620096e2b627957810fc001f/assets/Jun-23-2025_at_21.55.52-image.png)
4.  (Optional) Input a **Description**.
![Jun-23-2025_at_21.56.34-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/e36fbd69cfa831608d16bdcfe579951f/assets/Jun-23-2025_at_21.56.34-image.png)
5.  Click **Add** on CAPABILITIES option and select each service that NIOS-X-as-a-Service will be serving. Repeat this step for all desired services **DNS and Security**.
![Jun-23-2025_at_22.02.25-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/93ab9e2e7e0b83e03438ded03cbde983/assets/Jun-23-2025_at_22.02.25-image.png)
6.  Add both, DNS and Security by using the Add dropdown.
![Jun-23-2025_at_22.03.23-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/33f711000fbe493d64381cb68e157d03/assets/Jun-23-2025_at_22.03.23-image.png)
7.  Keep the default settings as they are and click **Add Capability**.
![Jun-23-2025_at_22.04.17-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/b906ab18c269d322d09c2d85b48dc960/assets/Jun-23-2025_at_22.04.17-image.png)
8.  Switch to **Deployment** tab.

> [!IMPORTANT]
> NOTE: We are still on Add Service Wizard Page

![Jun-24-2025_at_00.10.26-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/bcb672c7fb25ba1c4245f008e626c27c/assets/Jun-24-2025_at_00.10.26-image.png)
9.  Select **Add Service Deployment**.
![Jun-23-2025_at_22.06.11-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/9a8efe0efe962857148c6eb8e4f372f9/assets/Jun-23-2025_at_22.06.11-image.png)
10.  Give the new Deployment a **Name**.
![Jun-23-2025_at_22.07.32-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/eef25cf3bd06b9bd601de829f62c78f1/assets/Jun-23-2025_at_22.07.32-image.png)
11.  Configure **Service Location** as given
-  **Size** -  Select **S**
-  **Provider** -  Select **AWS**
-  **Uncheck** Use Recommended Location
-  **Location** -  **Please select Europe/Franfurt** as a location

> [!IMPORTANT]
> In this Lab we will use AWS Europe eu-central-1 Frankfurt Region.

-  **Service IP**- **this will be IP for your NIOS-X-as-a-Service (DNS resolver IP)** (This IP must be in a private IP range try to keep it far away from your AWS VPC network CIDR they should not fall in same CIDR. )

> [!IMPORTANT]
> NOTE: Service IP should be set to 10.10.10.3

Copy the Service IP from below and paste it  into the Infoblox Portal

```
10.10.10.3
```

![Jun-23-2025_at_22.24.50-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a222b212a541874fcb7354759aa81110/assets/Jun-23-2025_at_22.24.50-image.png)
12. Configure **Service Location Routing** as given
- **Routing** -  Select **Dynamic(BGP)**
- **Service Location ASN**  -  Enter **65500** {Note this value will be used while configuring the CGW on AWS side so remember this}
- **Primary Source IP **
- **Secondary Source IP **


> [!IMPORTANT]
> NOTE: Primary and Secondary Source IPs should be set retrospectively to 10.10.10.4 and 10.10.10.5.
> These IPs are used by NIOS-X-as-a-Service for operations such as Zone Transfers and Forwarding. They must also be in a Private IP range.

**Primary Source IP**
```
10.10.10.4
```
**Secondary Source IP**
```
10.10.10.5
```



![Jun-23-2025_at_22.28.53-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/cbfd6575a65414cfe8e907e310f12251/assets/Jun-23-2025_at_22.28.53-image.png)
13.  Configure **Access Location**
- Click **Add**
- **Provider** -  **AWS**
- **Type** - **Cloud VPN**
- **Region** - **Select as Earlier selected Location in Service Deployment**

> [!NOTE]
> 💡 Need global reach?
We’re ready to deploy in nearly every major cloud PoP — from AWS, Azure, to GCP — whether it’s Frankfurt, Virginia, or a coffee shop in Tokyo (okay, maybe not the last one… yet 😉).


- **Name** -  **name your access location**
![Jun-23-2025_at_22.37.16-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/b30ee63ea3d4b78900de98bd228d127f/assets/Jun-23-2025_at_22.37.16-image.png)
14.  Configure **CONNECTION**
14.1 click **Add Primary**
![Jun-23-2025_at_23.18.57-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/6de0d05fa4742d9e6a281a7af4aa4a48/assets/Jun-23-2025_at_23.18.57-image.png)
- give name to your primary connection

> [!IMPORTANT]
> ✅ NOTE:Make the name unique for both the Primary  and the  Secondary Connection.

- configure **PATH**
- click **Add Primary**
![Jun-23-2025_at_23.21.04-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/9c4b41a974989ff6f43432c4180680f6/assets/Jun-23-2025_at_23.21.04-image.png)
- Configure **Add Primary Path**
![Jun-23-2025_at_23.26.16-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f9122b5e626f3b211dea91ee73e5a23c/assets/Jun-23-2025_at_23.26.16-image.png)
- **Access IP Address**  -  Input a placeholder IP as we will return to this panel and configure this.
- Click  **Add Credential**
- Select **New**
![Jun-23-2025_at_23.27.38-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/bebd8949b63de9bc605f58dabbd0dc64/assets/Jun-23-2025_at_23.27.38-image.png)
- **Name** - any string is fine but you cannot repeat them while adding it on an another connection
- **Description**  -  enter your desired description
- **Pre-shared Key**   – Use the Pre-Shared Key below.

> [!NOTE]
> Note: the Pre-Shared key must be at least 16 characters and contain a special character (characters + and & are porhibited), this Pre-Shared Key will be used again in AWS.

Pre-shared key value for the lab you can find below:

```
InfobloxDNSLab2025.
```

- Click **Add Credential**
![Jun-23-2025_at_23.46.30-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/43bdbf13333297d12646d12d39553f83/assets/Jun-23-2025_at_23.46.30-image.png)
- Configure **BGP**
- enter the placeholder values at  **Neighbor IP Address**  and  **Access Location ASN   as it will be reconfigured.
- Click **Add Primary Path**
![Jun-23-2025_at_23.33.24-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/473b4aed0aa79cd469105096fd782c69/assets/Jun-23-2025_at_23.33.24-image.png)
- Click **Add Primary Connection**
![Jun-23-2025_at_23.33.40-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/9a26d9c5857aa778823016db47fca9b8/assets/Jun-23-2025_at_23.33.40-image.png)
14.2 Click **Add Secondary**
![Jun-23-2025_at_23.41.20-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/341cc0537721ae693255e72b7a45a9e5/assets/Jun-23-2025_at_23.41.20-image.png)
- give name to your secondary connection

> [!IMPORTANT]
> ✅ NOTE:Make the name unique for both the Primary  and the  Secondary Connection.

- configure **PATH**
- click **Add Secondary**
![Jun-23-2025_at_23.42.48-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/30268ed660cd4bb79353427fd892c92c/assets/Jun-23-2025_at_23.42.48-image.png)
- **Access IP Address**  -  Input a placeholder IP as we will configure this later again.
- Click  **Add Credential**
- Select **New**
![Jun-23-2025_at_23.44.36-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/de93ac2733f1895567a7d6f612f86f1f/assets/Jun-23-2025_at_23.44.36-image.png)
- **Name** - any string is fine but you cannot repeat them while adding it on an another connection
- **Description**  -  enter your desired description
- **Pre-shared Key**  - Use the Pre-Shared Key below.

> [!NOTE]
> Note: the Pre-Shared key must be at least 16 characters and contain a special character (characters + and & are porhibited), this Pre-Shared Key will be used again in AWS.


Pre-shared key value for the lab you can find below:

```
InfobloxDNSLab2025.
```

- Click **Add Credential**
![Jun-23-2025_at_23.46.30-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/43bdbf13333297d12646d12d39553f83/assets/Jun-23-2025_at_23.46.30-image.png)
- Configure **BGP**
- enter the Dummy values at  **Neighbor IP Address**  and  **Access Location ASN   as it will be reconfigured.
- Click **Add Secondary Path**
![Jun-23-2025_at_23.48.19-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/df4fae96328440b4d55dfa99199929ef/assets/Jun-23-2025_at_23.48.19-image.png)
- Click **Add Secondary Connection**
![Jun-23-2025_at_23.48.39-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/20187257b5fabe28df90fa9b985e8a04/assets/Jun-23-2025_at_23.48.39-image.png)
- Finally click **Add Location**
![Jun-23-2025_at_23.49.59-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/0292d885d013c51a6b63219811845420/assets/Jun-23-2025_at_23.49.59-image.png)
- Click **Add Deployment*
![Jun-23-2025_at_23.50.51-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/3c81136d742b21361dd092d245fcdf53/assets/Jun-23-2025_at_23.50.51-image.png)
15.  Click **Save** to save all changes

> [!NOTE]
> 📝 NOTE:
After editing the instructions, make sure to save your changes. To reveal the “Save Changes” button scroll around the portal using the trackpad or mouse until the button appears.
The button may be hidden by default depending on screen size or browser zoom level.

![Jun-23-2025_at_23.51.38-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/48c0f3e058adfa068d6b08f800a4b348/assets/Jun-23-2025_at_23.51.38-image.png)
16.  Wait approximately 3 minutes, then Refresh the Webpage
17.  Once the NIOS-X-as-a-Service deployment is ready, you will see a Ready Status here
![Jun-24-2025_at_00.03.36-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/925ad34b8029024c613494d7a41feedd/assets/Jun-24-2025_at_00.03.36-image.png)
18.  Click on the hyperlink below Location and notice **SERVICE DEPLOYMENT** details
![Jun-24-2025_at_00.04.40-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/56e6f0c45581dc1c4d9f6ecf2c20263c/assets/Jun-24-2025_at_00.04.40-image.png)
19.  Copy these Cloud Service IPs located in the Service Deployment panel, these { will be used later.}

> [!IMPORTANT]
> Note: Cloud Service IPs may take up to 5 minutes to appear. Please refresh the page periodically and allow time for propagation NIOS-X-as-a-Service’s deployment process to complete.


## 2. Configuring AWS

🔧 Create Customer Gateways (Step 2)

Go to the AWS Web Console. In the left window of the lab environment, click on the AWS Console tab to launch it.

Use the login credentials provided in Section 1 to sign in.

> [!IMPORTANT]
> 📍 Important: Before proceeding, make sure you switch to the correct region:
Select eu-west-2 (London) from the region selector in the top-right corner of the console.
This is required to ensure that the Customer Gateways and subsequent VPN configurations are created in the same region.

Once you’re in the correct region, proceed to create the Customer Gateways as outlined.

1. Now we will create 2 x  **Customer Gateways**.
2. Go to Virtual private network (VPN)>Customer gateways.
3. Create the first gateway. Click on **Create Costumer Gateway**
![Jun-24-2025_at_00.51.52-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/c60386be95ea7d93eedef258630122df/assets/Jun-24-2025_at_00.51.52-image.png)
4. Input the following as mentioned below:
- **Name tag** - input a name for you CGW
> [!NOTE]
> Note: Input an easy to remember name as we will be using this Customer Gateway in future steps
- **BGP ASN** - give the BGP same value as you have given in step 12 at Service Location ASN : **65500**
- **IP Address** -  this will be the value of first IP in Cloud Service IP under Service Deployment.(These are the Public IPs)
- Fill in the option fields if you wish to
![Jun-24-2025_at_10.39.43-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/86f6db94075cc1e20e596f538aba50a6/assets/Jun-24-2025_at_10.39.43-image.png)
5. Click Create customer gateway to finalize the creation of the first Customer Gateway.
6. Create the Second gateway. Click on Create Customer Gateway.
![Jun-24-2025_at_00.51.52-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/c60386be95ea7d93eedef258630122df/assets/Jun-24-2025_at_00.51.52-image.png)
7. Input the following as mentioned below:
- **Name tag** - input a name for your CGW.
> [!NOTE]
> Note input an easy to remember name as we will be using this Customer Gateway in future steps.

- **BGP ASN** - give the BGP same value as you have given in step 12 of 1 at Service Location ASN : **65500**
- **IP Address** -  this will be the value of second IP in Cloud Service IP under Service Deployment.
- Fill in the option fields if you wish to
![Jun-24-2025_at_10.41.58-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/b15aa64ce0606207cb8d4db2101deb79/assets/Jun-24-2025_at_10.41.58-image.png)

8. Select Create Customer Gateway to complete provisioning of the second CGW instance.

9. Now you will be creating two **Site-to-Site VPN connections**

In the AWS Console, use the search bar at the top and type VPC, then click on the VPC service.

🔹 Make sure you are in the eu-west-2 region, as shown in the lab diagram.

10. Go to the Virtual Private Cloud ( VPC ) then scroll down in the left side panel to click  --> Site-to-Site VPN connections under the Virual Private Network (VPN) header.
11. To Create the first Site-to-Site VPN connections complete the following steps:
- Click **Create VPN Connection**
![Jun-24-2025_at_11.09.24-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/887cac81f291c1b356a2ed488118be2d/assets/Jun-24-2025_at_11.09.24-image.png)
- **Name tag - optional** - enter the name for your VPN connection
- **Target gateway type** - keep it as **Virtual private gateway** and select the one available from the drop-down menu

> NOTE: VGW name is VGW-Lab

- **Customer gateway** -  keep it as **Existing** and select first CGW that was created in this lab.
- **Routing options**-  keep it as **Dynamic (requires BGP)**
- **Pre-shared key storage** - keep it as **Standard**
![Jun-24-2025_at_11.18.26-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/26f273e7c0200545603725645567f84a/assets/Jun-24-2025_at_11.18.26-image.png)
- Expand **Tunnel 1 options  - optional **
![Jun-24-2025_at_11.20.27-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/49bb4bfa3db0437166d3d7622a9e1867/assets/Jun-24-2025_at_11.20.27-image.png)
- **Inside IPv4 CIDR for tunnel 1** - A size /30 IPv4 CIDR block from the 169.254.0.0/16 range.(Must be a valid CIDR)

> [!IMPORTANT]
> NOTE:  Subnet should be 169.254.21.0/30


```
169.254.21.0/30
```

- **Pre-shared key for tunnel 1**

```
InfobloxDNSLab2025.
```

- **Advanced options for tunnel 1** -  Select **Edit tunnel 1 options**
- leave all the options as they are
- **Startup Action** -  **Start**
- Click **Create VPN connection**
![Jun-24-2025_at_11.26.07-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/5f84fcebd0715247a709046e527a514e/assets/Jun-24-2025_at_11.26.07-image.png)
12. Creating Second Site-to-Site VPN connections
- Click **Create VPN Connection**
![Jun-24-2025_at_11.09.24-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/887cac81f291c1b356a2ed488118be2d/assets/Jun-24-2025_at_11.09.24-image.png)
- **Name tag - optional** - enter the name for your VPN connection
- **Target gateway type** - keep it as **Virtual private gateway** and select select the one available from the drop-down menu

> NOTE: VGW name is VGW-Lab

- **Customer gateway** -  keep it as **Existing** and select the second CGW that was created in this lab.
- **Routing options**-  keep it as **Dynamic (requires BGP)**
- **Pre-shared key storage** - keep it as **Standard**
![Jun-24-2025_at_11.38.36-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f8638d4a2a56c50366551989c43970a8/assets/Jun-24-2025_at_11.38.36-image.png)
- Expand **Tunnel 1 options  - optional **
![Jun-24-2025_at_11.20.27-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/49bb4bfa3db0437166d3d7622a9e1867/assets/Jun-24-2025_at_11.20.27-image.png)
- **Inside IPv4 CIDR for tunnel 1** - A size /30 IPv4 CIDR block from the 169.254.0.0/16 range. (Must be a valid CIDR)

> [!IMPORTANT]
> NOTE:  Subnet should be 169.254.22.0/30

```
169.254.22.0/30
```

- **Pre-shared key for tunnel 1**

```
InfobloxDNSLab2025.
```


- **Advanced options for tunnel 1** ---->. Select **Edit tunnel 1 options**
-** leave all the options as they are**
- **Startup Action** -  **Start**

> [!IMPORTANT]
> NOTE - Make sure you select START option - AWS initiates the connection

![Screenshot 2025-07-02 at 12.59.35.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/c81caaacf57221c43bbaaa562bacdc5b/assets/Screenshot%202025-07-02%20at%2012.59.35.png)

![Screenshot 2025-07-02 at 12.59.49.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/2e1726f5baf52ce33a919e7714288ee5/assets/Screenshot%202025-07-02%20at%2012.59.49.png)

- Click **Create VPN connection**
![Jun-24-2025_at_11.26.07-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/5f84fcebd0715247a709046e527a514e/assets/Jun-24-2025_at_11.26.07-image.png)


13. Enable the Route Propogation on your VPC
14. Go to VPC
15. Select the section **Route Tables**

![Screenshot 2025-07-01 at 09.21.35.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/15c8a261a0fe9f3066f46ddf9d156ef5/assets/Screenshot%202025-07-01%20at%2009.21.35.png)

16. Go to **Route Propagation** tab
![Jun-24-2025_at_11.55.27-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/ccc94a5ade7ceace6a2a67c48cbaee92/assets/Jun-24-2025_at_11.55.27-image.png)
17. Click **Edit Route Propagation**
![Jun-24-2025_at_11.57.03-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/3ddbbb4a393067f373d1ae9baf77e6a2/assets/Jun-24-2025_at_11.57.03-image.png)
18. Check **Enable** and hit **Save**
![Jun-24-2025_at_11.57.48-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/ae65906796d6f59133ef5e56e9ab6324/assets/Jun-24-2025_at_11.57.48-image.png)


## 3.  Establish an IPsec tunnel between an AWS VPN and Infoblox(Re-Config).

1. In your AWS console go to Site-to-Site VPN connections
2. Go to Tunnel-1 that you configured in step 23 of 2

🌐 Retrieve Tunnel 1 Outside IP (AWS)

To complete the IPsec setup, you’ll need to fetch the outside IP address for Tunnel 1 from your AWS VPN connection:
- Go to the AWS Console (ensure you’re still in eu-west-2 region).
- In the Search bar, type VPN and select Site-to-Site VPN Connections.

![Screenshot 2025-07-18 at 08.59.42.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/28f80cd79e742f2775e381ba05cfc089/assets/Screenshot%202025-07-18%20at%2008.59.42.png)

- Locate your first VPN connection (e.g., vpn-1) in the list.
- Click on the VPN Connection ID to open the details page.

![Screenshot 2025-07-18 at 09.01.24.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/229a1318b0f7a81532cab50d572445a1/assets/Screenshot%202025-07-18%20at%2009.01.24.png)

- Scroll down to the Tunnel Details section.

![Screenshot 2025-07-18 at 09.02.37.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/ab7d82c6cfc8f6b90d68066ae54ce6d3/assets/Screenshot%202025-07-18%20at%2009.02.37.png)

- Under Tunnel 1, look for the field labeled Outside IP Address.

3. Copy **Outside IP address** of Tunnel-1
4. Log in to your Infoblox Portal again and navigate to  Configure >Service Deployment >As-A-Service
5. Click on three dots associated with your NIOS-X-as-a-Service deployment service name and click Edit
![Jun-24-2025_at_12.06.47-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/91cf73f8583026f6103666275ac94d88/assets/Jun-24-2025_at_12.06.47-image.png)
6. Click on three dots in front of your service deployment in the Service Deployments panel and click Edit.
![Jun-24-2025_at_12.07.10-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/adad18ceee12e2a5453f289c6db0477b/assets/Jun-24-2025_at_12.07.10-image.png)
7. In the **Access Location** click on the drop downs and select your Access Location and click on three dots and select Edit.
![Jun-24-2025_at_13.28.08-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a8a1c78ace9b0fe54bb76cb7ae79a60e/assets/Jun-24-2025_at_13.28.08-image.png)
8. On **Edit Access Location window** select **Primary Connection**
![Jun-24-2025_at_13.29.19-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/9a91abda47aedd83ab9f691e81024933/assets/Jun-24-2025_at_13.29.19-image.png)
9. Under the Connection header click Primary.
![Jun-24-2025_at_13.29.59-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/003a521643951450f9ba3d3a5bf78784/assets/Jun-24-2025_at_13.29.59-image.png)
10. Change the Inside IPv4 CIDR to the  **Outside IP address** of Tunnel-1   of VPN-1from step 3 of 3
11. On **BGP** in **Neighbor IP Address**   update the **Inside IPv4 CIDR** of Tunnel-1 on AWS side.

> [!IMPORTANT]
	> NOTE: Neighbor IP is 169.254.21.1

13. For **Access Location ASN** copy paste the value from **Amazon ASN**  **64512**

```
64512
```

14. Click Edit Primary Path
![Jun-24-2025_at_13.35.42-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a967dd664f3562de2106e09d89f926a4/assets/Jun-24-2025_at_13.35.42-image.png)
15. Click Edit Primary Connection
![Jun-24-2025_at_13.35.58-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/4f432f179e2ae47dd1d294d8cf50b54a/assets/Jun-24-2025_at_13.35.58-image.png)
16. On **Edit Access Location window** select **Secondary Connection**
![Jun-24-2025_at_13.37.15-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/cd5fdbf2ce9f6acdada6a4de379e0b8d/assets/Jun-24-2025_at_13.37.15-image.png)
17. Under the Tunnel header, click Secondary
![Jun-24-2025_at_13.37.54-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/7c2a4fceec55690705047d0bcc776f99/assets/Jun-24-2025_at_13.37.54-image.png)
18. Change Access IP Address as **Outside IP address** of Tunnel-1 of VPN-2 from step 3 of 3
19. Under the BGP header change the Inside IPv4 CIDR to the  Inside IPv4 CIDR of Tunnel-1 of VPN-2 on AWS side.

> [!IMPORTANT]
> NOTE: Neighbor IP is 169.254.22.1

20.  Click Edit Secondary Path
![Jun-24-2025_at_13.47.38-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/6eaa5395975a2913394d52224a734657/assets/Jun-24-2025_at_13.47.38-image.png)
21. Click Edit Secondary Connection
![Jun-24-2025_at_13.49.11-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/54e8706e0a06c6ce3a9d9d1d2cb3d9c9/assets/Jun-24-2025_at_13.49.11-image.png)
22. Click Update Location
![Jun-24-2025_at_13.50.15-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/38458b7ba2911d35a03df65b7a6b2dfa/assets/Jun-24-2025_at_13.50.15-image.png)
23. Click Update
![Jun-24-2025_at_13.50.40-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/b7ed57f432cb1517ec75b2b46eecb834/assets/Jun-24-2025_at_13.50.40-image.png)
24. Click Save
![Jun-24-2025_at_13.51.04-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/55d40f83c2d3f76ec00fb089450b31f7/assets/Jun-24-2025_at_13.51.04-image.png)
25. Now you should see a green square and connected as status in front of your Access Location under SERVICE STATUS
![Jun-24-2025_at_14.10.05-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a9b8a0d64a181aea6f7e4ec787c48f15/assets/Jun-24-2025_at_14.10.05-image.png)



## 4. Test/Verify the configuration.

1. On the Infoblox CSP tenant side you will see a green square and connected as status in front of your Access Location under SERVICE STATUS which indicates the service is UP
![Jun-24-2025_at_14.10.05-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a9b8a0d64a181aea6f7e4ec787c48f15/assets/Jun-24-2025_at_14.10.05-image.png)
2. In the AWS Console, go to VPC → Route Tables, then scroll or search to select **WebSvcsProdEu1-RT**.

![Screenshot 2025-07-25 at 10.54.09.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/f3345ccd0afee74a59f68e7187debf61/assets/Screenshot%202025-07-25%20at%2010.54.09.png)

4. In Routes you must see the Service IPs - **Service IP: 10.10.10.3**

> [!NOTE]
> 📝 NOTE:
A page refresh may be required if changes don’t appear immediately. For example, after switching to the route tables, the expected options might not show up until the page is refreshed. Refreshing ensures the UI reflects the latest state.

![Jun-24-2025_at_14.32.04-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/39a9d2ebe179aca2923194d7f89ac9c4/assets/Jun-24-2025_at_14.32.04-image.png)
5. On AWS console go to Site-to-Site VPN connections and then navigate to VPN-1 that you created
6. Notice the Tunnel state in Tunnel details  for Tunnel 1 status should be Up
![Jun-24-2025_at_14.34.39-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/4c3b11b9e18ae30daa9dcefa725c5722/assets/Jun-24-2025_at_14.34.39-image.png)
7. On AWS console go to Site-to-Site VPN connections and then navigate to VPN-2 that you created
8. Notice the Tunnel state in Tunnel details  for Tunnel 1 status should be Up
![Jun-24-2025_at_14.37.05-image.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/e889d9b41101f6f259e2117185fc2700/assets/Jun-24-2025_at_14.37.05-image.png)


## 🧭 Configure AWS DHCP Option Set for Infoblox DNS
==

To automatically direct EC2 instances to use Infoblox DNS resolvers, create a custom DHCP option set and associate it with your target VPC. You can do this from the AWS Web Console — navigate to it via the left-hand side navigation panel.

---

### Step 1: Create a DHCP Option Set

- In the AWS Console, go to the VPC service (you can search “VPC” in the top search bar).
- In the left-hand menu, scroll down and click on DHCP Option Sets.
- Click the “Create DHCP Option Set” button at the top.

![Screenshot 2025-07-01 at 13.27.32.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/067654efb858bc3fb04f6be4d278226d/assets/Screenshot%202025-07-01%20at%2013.27.32.png)

Set the following:

- **Name**: `infoblox-lab`
- **Domain name**: `infolab.com` (or as needed)
- **Domain name servers**: `10.10.10.3` *(replace with your Infoblox DNS IP)*
- *(Optional)* Configure NTP, NetBIOS if needed


> 💡 Tag the DHCP option set for easier identification:
> `Key: Name` → `Value: infoblox-lab`

Click **Create DHCP Option Set**.


---

### Step 2: Associate DHCP Option Set with Your VPC

Navigate to:
`VPC Console > Your VPCs`

1. Select your target VPC (e.g., `WebSvcsProdEu1`)
2. Click **Actions > Edit VPC Settings**
3. In the **DHCP option set** dropdown, select `infoblox-lab`
4. Click **Save**

![Screenshot 2025-07-01 at 13.30.06.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/053f8952a3b2889d94b31dfbc994b2d6/assets/Screenshot%202025-07-01%20at%2013.30.06.png)

---

### ✅ Result

All new EC2 instances in the VPC will now automatically use the DNS server defined in your DHCP option set (e.g., your Infoblox resolver). This ensures DNS queries are visible and controlled by Infoblox Threat Defense.

---

🔍 Step 6: Validate DNS Resolution


### Step 1: Access the EC2 Instance

From the **Shell tab** in your lab, run the following:

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform output
```

This will show you the SSH command to access the EC2 instance - **WebServerProdEu1**

![Screenshot 2025-07-01 at 13.37.20.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f72fb1c74b7fb04e90c2d623448bc434/assets/Screenshot%202025-07-01%20at%2013.37.20.png)


> [!IMPORTANT]
> NOTE:Please use your specific SSH command from the `terraform output` to access the instance.

```
ssh -i 'EU_WEST_WebProd1.pem' ec2-user@35.177.254.177
```

![Screenshot 2025-07-01 at 13.39.13.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/1356e48269998e5d3e923b8fccb1c51a/assets/Screenshot%202025-07-01%20at%2013.39.13.png)


### Step 2: Check DNS Settings

Once inside the EC2 host **WebServerProdEu1** , confirm it’s using the Infoblox DNS server:

```
cat /etc/resolv.conf
```

![Screenshot 2025-07-01 at 13.39.54.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a9bdf0f65c4ad5b23244069f37c8394a/assets/Screenshot%202025-07-01%20at%2013.39.54.png)

> [!IMPORTANT]
> ✅ You should see: 10.10.10.3



If not reboot the instance and login again.

![Screenshot 2025-07-03 at 09.33.14.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a009a9a8c182dea0dc94c41fbaa0d4bd/assets/Screenshot%202025-07-03%20at%2009.33.14.png)

From WebServerProdEu1 run the following command:

```run
dig google.com
```

## 4) Configuring Infoblox NIOS-X-as-a-Service  as Authoritative DNS for AWS Private Zone
===

In this section, we will extend our setup by integrating Infoblox NIOS-X-as-a-Service as the authoritative DNS for the infolab.com AWS Private DNS zone.

After syncing the zone from AWS using API-based synchronization, we will configure the authoritative DNS servers under Infoblox’s “Configure” section to explicitly designate NIOS-X-as-a-Service as the DNS authority for the zone. This enables Infoblox to answer DNS queries for AWS workloads and any other clients resolving *.infolab.com.

> [!IMPORTANT]
> NOTE: Make sure the AWS Discovery Job is fully synced before proceeding. This step has been pre-provisioned in the backend to streamline the lab and save you setup time.

![Screenshot 2025-07-13 at 11.54.16.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/effdad2c585e07432cc4c0dd3f2cb261/assets/Screenshot%202025-07-13%20at%2011.54.16.png)

You’ll also see how to:
- Identify synced zones under the DNS view
- Modify the zone properties to add authoritative DNS instances
- Validate resolution by running dig from an EC2 instance ( from AWS Region ) pointing to the NIOS-X-as-a-Service DNS IP

This is key for hybrid or multicloud deployments where unified visibility, control, and logging over DNS is critical.

🛠 Prerequisites:

- Zone (infolab.com) already created in AWS Private DNS

- API sync already done, visible under DNS View AWS.private-1 or default DNS view - which one is available

- NIOS-X-as-a-Service service instance deployed


✅ Step-by-Step: Configure Infoblox as Authoritative DNS

1. Navigate to DNS Configuration

In the Infoblox Portal, navigate  to Configure → Networking → DNS → Zones. Click the default DNS View.
Make sure to select the correct DNS View  and click on it.

![Screenshot 2025-07-13 at 11.55.44.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/a55dc223ea7ed73c32de9c4df88b1dc4/assets/Screenshot%202025-07-13%20at%2011.55.44.png)

Under default view when you click on it you will see the infolab.com zone.

![Screenshot 2025-07-13 at 11.55.54.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/8fd6ccaf6c402a41cffacbd23ee3753c/assets/Screenshot%202025-07-13%20at%2011.55.54.png)

2. Locate the Synced Zone

You should see  **infolab.com**  listed under the synced zones
Click the hamburger icon next to the zone, then hit Edit


![Screenshot 2025-07-03 at 12.04.46.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/d6e88db2845e7796854ab0582aafb4fc/assets/Screenshot%202025-07-03%20at%2012.04.46.png)

3. Add Authoritative DNS Server

Scroll down to Authoritative DNS Servers section
In the Service Instances list, select the Infoblox NIOS-X instance (e.g. TEST) with type NIOS-X (BloxOne) DDI
Click the arrow >> to move it to the selected list

> [!NOTE]
> Note: the instance you selected is associated with the NIOS-X-as-a-Service instance deployed earlier in this lab


![Screenshot 2025-07-13 at 12.00.23.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/af2ada5e6e4a4fb8db3bd12a96baf87d/assets/Screenshot%202025-07-13%20at%2012.00.23.png)

5. Save & Close
	•	Click Save and Close
	•	Zone will now reflect NIOS-X as the authoritative server


![Screenshot 2025-07-13 at 12.01.05.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/2636347546e4c9631420a7f51a60c633/assets/Screenshot%202025-07-13%20at%2012.01.05.png)


🔍 Step 6: Validate DNS Resolution


### Step 1: Access the EC2 Instance

From the **Shell tab** in your lab, run the following:

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform output
```

This will show you the SSH command to access the EC2 instance - **WebServerProdEu1**

![Screenshot 2025-07-01 at 13.37.20.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f72fb1c74b7fb04e90c2d623448bc434/assets/Screenshot%202025-07-01%20at%2013.37.20.png)


> [!IMPORTANT]
> NOTE:Please use your specific SSH command from the `terraform output` to access the instance.

```
ssh -i 'EU_WEST_WebProd1.pem' ec2-user@35.177.254.177
```

![Screenshot 2025-07-01 at 13.39.13.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/1356e48269998e5d3e923b8fccb1c51a/assets/Screenshot%202025-07-01%20at%2013.39.13.png)


### Step 2: Check DNS Settings

Once inside the EC2 host **WebServerProdEu1** , confirm it’s using the Infoblox DNS server:

```
cat /etc/resolv.conf
```

![Screenshot 2025-07-01 at 13.39.54.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a9bdf0f65c4ad5b23244069f37c8394a/assets/Screenshot%202025-07-01%20at%2013.39.54.png)

> [!IMPORTANT]
> ✅ You should see: 10.10.10.3



If not reboot the instance and login again.

![Screenshot 2025-07-03 at 09.33.14.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/a009a9a8c182dea0dc94c41fbaa0d4bd/assets/Screenshot%202025-07-03%20at%2009.33.14.png)


From WebServerProdEu1 run the following command:

```run
dig @10.10.10.3 CNAME infobloxs3.infolab.com
```

Example output:

![Screenshot 2025-07-13 at 12.05.01.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/56b53a689c6d6265c81e4e5e6f9d285b/assets/Screenshot%202025-07-13%20at%2012.05.01.png)


🎯 Success means:
•	ANSWER SECTION is returned
•	AUTHORITY SECTION shows your Infoblox record
•	It resolves against @10.10.10.3 (your Infoblox DNS IP)



## Time for the Next Challenge

 Click **NEXT**!

