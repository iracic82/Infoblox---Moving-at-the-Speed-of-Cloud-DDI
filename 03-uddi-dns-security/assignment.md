---
slug: uddi-dns-security
id: 1l7jrkanrryx
type: challenge
title: GenAI DNS Threat Simulation
teaser: GenAI DNS Threat Simulation
notes:
- type: video
  url: https://videos.infoblox.com/watch/DytGsd2iVoUeVhaqva1kNm?
tabs:
- id: gwoxcxn24nxx
  title: Shell
  type: terminal
  hostname: shell
- id: ajdwm3hsqv5p
  title: Editor
  type: code
  hostname: shell
  path: /root/infoblox-lab
- id: 6zulr2hcqavf
  title: Flask UI
  type: browser
  hostname: flask-ui
- id: hdomtere8osv
  title: AWS Console
  type: browser
  hostname: aws
- id: vdyxp9fywv5b
  title: Lab Diagram
  type: browser
  hostname: lab
difficulty: ""
timelimit: 0
lab_config:
  default_layout_sidebar_size: 0
enhanced_loading: null
---
🔐 GenAI DNS Threat Simulation — Key Takeaways

🎯 Objective

Simulate how Generative AI could inadvertently suggest or generate malicious or untrusted domains — and demonstrate how Infoblox DNS Security detects, blocks, and logs such queries in real time.

⸻

🧠 How It Works in This Demo

•	The Flask app queries AWS Bedrock (or simulates it) to generate a list of “health-related” domains — some legitimate, some fabricated and suspicious.

•	These domains include:

•	Trusted: webmd.com, cdc.com, mayoclinic.com etc

•	AI-generated but plausible: ai-medicine-data.com, suspicious-healthinfo.com

•	DNS-exfiltration-style FQDNs: chunk1.ai-medicine-data.com, etc.

•	The client issues HTTP requests, triggering DNS queries that are logged and analyzed by Infoblox Threat Insight.

⸻

✅ Detection & Policy Enforcement

•	Custom List: For demonstration purposes, we include the AI-generated domains in a Custom List to guarantee consistent detection and show deterministic behavior.

•	In Production: Infoblox DNS Threat Insight can automatically:

•	Detect DNS exfiltration patterns (based on frequency, entropy, and burst behavior).

•	Identify newly observed, low-reputation, or algorithmically generated domains.

•	Enforce policy based on domain classification, DGA detection, or exfiltration heuristics — even if the domains are not pre-listed.

⸻

🧩 Why Keep the Custom List in the Demo - Custom List usage in Infoblox UDDI Security Policy

•	Ensures repeatable, controlled demo experience

•	Guarantees that AI-generated suspicious domains are blocked and logged regardless of real-time behavior patterns

•	Accelerates time-to-value demonstration in lab conditions


In production, the same DNS queries would be flagged without needing to manually pre-load lists — thanks to Infoblox’s machine learning models, threat feeds, and DGA detection.

⸻



Infoblox Product Portoflio is here to help

![Screenshot 2025-07-03 at 20.43.26.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/f938de16b8bb06a0f3714b9cf48e3676/assets/Screenshot%202025-07-03%20at%2020.43.26.png)

##  Login to your cloud account consoles
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


## 🛠 Step-by-Step Instructions
==

Login to your Infoblox Portal before moving forward.

### 1. Let's Create Custom List
Go to:
`Configure > Security > Policies` -> Please select Tab Custom List

![Screenshot 2025-07-04 at 13.53.11.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/c9c772ad5a5483d6164ebb84e2e4141e/assets/Screenshot%202025-07-04%20at%2013.53.11.png)

Click on **IMPORT** button
Give it the name in List Name field:

```
Gen AI Policy List
```

and afterwards  **SELECT File**

![Screenshot 2025-07-04 at 13.53.29.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/5caaec002cd49a6c623d4575493877c8/assets/Screenshot%202025-07-04%20at%2013.53.29.png)

On the **HOME**  section select **gen-ai.csv** file

![Screenshot 2025-07-04 at 14.52.58.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/00928ba782eea0819a8576cf3263d9f7/assets/Screenshot%202025-07-04%20at%2014.52.58.png)

Click Import after selecing and adding the file.





### 2. Navigate to Policies
Go to:
`Configure > Security > Policies`

You will see:
- `Default Global Policy` (auto-generated)

Mark the policy and Click Clone

![Screenshot 2025-07-01 at 13.10.50.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/64e42ab5093d0c2c90f5ea9fabda7d66/assets/Screenshot%202025-07-01%20at%2013.10.50.png)

### 3. Edit the Lab Policy

Give it the name `Infoblox-Lab` .

![Screenshot 2025-07-01 at 13.12.34.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/4a8e0a182b7f7bb82c2e0ead1fcd9bad/assets/Screenshot%202025-07-01%20at%2013.12.34.png)

#### On the **General** tab:
Ensure the following are set:
- **Precedence**: `2`
- **All options disabled**: Geolocation, Safe Search, DoH per Policy, Block DNS Rebinding, Local On-Prem Resolution

---

### 4. Configure Policy Rules
Go to the **Policy Rules** tab.

Find the rule 16 and configure it as you see on the picture below

![Screenshot 2025-07-01 at 13.14.01.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/e583320faf9007d7741976b520ff4342/assets/Screenshot%202025-07-01%20at%2013.14.01.png)

### 5. Add new rule
Go to the **Add Rule** menu in the top and select **Custom List**

![Screenshot 2025-07-01 at 13.15.53.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/99c0ee7cde5b4ebf9e12afce37108a03/assets/Screenshot%202025-07-01%20at%2013.15.53.png)

Find **Gen AI Policy List** just created and Select it


![Screenshot 2025-07-04 at 15.04.16.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/1d9c68df08692ce99e911124b48f9e9a/assets/Screenshot%202025-07-04%20at%2015.04.16.png)

Make sure that setting for this is Block No Redirect as on the picture below

![Screenshot 2025-07-04 at 15.03.17.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/2d30889cdecbe8c7304dbe365d8bcf60/assets/Screenshot%202025-07-04%20at%2015.03.17.png)


### 6. Save and Finish
Click **Next**, then **Finish** to save your policy configuration.

### 7. Assign the Policy to a Service

#### Navigate to:
`Configure > Service Deployment > As-A-Service`

![Screenshot 2025-07-01 at 13.20.07.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/8e5d05ef510128814d7d92a3d798ae5b/assets/Screenshot%202025-07-01%20at%2013.20.07.png)

You should see an existing deployed service instance (e.g., `Test`).

![Screenshot 2025-07-01 at 13.20.20.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/02892ca97bab908e90672ed37171962d/assets/Screenshot%202025-07-01%20at%2013.20.20.png)

---

### 8. Edit the Security Service Profile

1. Click the Security service.
2. Click the three-dot menu → **Edit**.


![Screenshot 2025-07-01 at 13.20.30.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/c3ad0845fe2f011145fdd804ab3da38b/assets/Screenshot%202025-07-01%20at%2013.20.30.png)

3. Click on **Security** under **Service Capabilities Section**
4. From the **Profile** dropdown, choose your custom policy (e.g., `Infoblox-Lab`)

---

### 9. Add the Security Capability

1. Under **Service Capabilities**, click **Add**
2. For **Type**, select: `Security`

> [!IMPORTANT]
> NOTE: Steps 1 and 2  - has to be done now ONLY  if you skipped these steps during the previous challenge when creating the NIOS-as-a-Service deployment, make sure to add it now.

3. From the **Profile** dropdown, choose your custom policy (e.g., `Infoblox-Lab`)
4. Click **Update Capability**

![Screenshot 2025-07-01 at 13.20.39.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/00ce251352ddcaa123c3e3e3f5b85ecb/assets/Screenshot%202025-07-01%20at%2013.20.39.png)

![Screenshot 2025-07-01 at 13.20.46.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/2443ca627e328bdbe77d6d9721d9b3d5/assets/Screenshot%202025-07-01%20at%2013.20.46.png)


### 10. Save the Configuration

1. Review the service deployment (ensure it’s using correct location and policy).
2. Click **Save**.

![Screenshot 2025-07-01 at 13.20.56.png](https://play.instruqt.com/assets/tracks/atmmwsclkofd/33e4ff1cc7452939cdca34cf896eef33/assets/Screenshot%202025-07-01%20at%2013.20.56.png)

🎉 Your DNS policy is now actively protecting the assigned service!





## 🧠 GenAI DNS Simulation: Detecting AI-Driven Threats via DNS
==

Now that the Secure AI DNS Flask app is running, let’s walk through how DNS is used to simulate LLM-based data access, and how Infoblox detects and blocks malicious queries triggered by GenAI.

We’ll validate:

1.	✅ The app works and queries the “fake” Bedrock API

2.	🧬 DNS queries generated by the app are captured by Infoblox

3.	🔐 DNS exfiltration attempts or suspicious domains are blocked + logged

---

### 🚀 Step 1: Launch the Flask App

📍 Navigate to the Flask UI

From the left-hand side panel, click on the “Flask UI” tab to open the application interface.

Alternatively, you can click the button below to launch the Flask UI directly in your current browser tab:

⬇️

[button label="Flask UI"  background="#c2fbd7" color="green"](http://[[ Instruqt-Var key="SANDBOX_ID" hostname="shell" ]]-websrv1infoblox.iracictechguru.com:5050)

![Screenshot 2025-07-07 at 11.18.47.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/9b0c0179cfc40e67193050785e976459/assets/Screenshot%202025-07-07%20at%2011.18.47.png)

> [!IMPORTANT]
> ⚠️ NOTE: This UI simulates a GenAI interface powered by Bedrock but using a mock API behind the scenes.

### 💬 Step 2: Ask a Health-Related Question


Try entering something like:

```
What allergy websites are considered safe?
```

Press Submit.

This triggers the following:

When a doctor submits a question through the Flask UI, the app sends a POST request to the simulated Bedrock endpoint (mimicking interaction with bedrock-runtime.amazonaws.com). Once the GenAI model generates a response, it includes links — some of which are legitimate domains (e.g. *.com, *.org) and others crafted to simulate malicious or suspicious behavior.


The Flask app then extracts and resolves these domains, performing real DNS lookups. This includes:

•	Normal FQDNs derived from the AI response (e.g., trusted health sources)

•	As well as intentionally embedded FQDNs that mimic exfiltration-style behavior (like chunk1.ai-medicine-data.com).

These suspicious domains are pre-classified and matched against a Custom List in Infoblox DNS Threat Defense. If a domain is found on the list, it is blocked, and the DNS response will show NXDOMAIN. The system logs this as a policy block event.

Of course due to this simulation we use pre-created Custom List but in reality Infoblox will auto-detect that without loading any pre-configured Custom List.

Throughout this process, DNS visibility is maintained in real time.

The Flask app displays each DNS resolution attempt (including the status: allowed, blocked, or NXDOMAIN) in its UI and logs them to dns_queries.log that is presented in the Flask UI.

![Screenshot 2025-07-07 at 11.39.15.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/b232d518a04d78076cef38a292353479/assets/Screenshot%202025-07-07%20at%2011.39.15.png)

Meanwhile, Infoblox Threat View captures all query activity, enabling security teams to analyze, alert, and validate that DNS-based risks from AI-generated traffic are fully observable and controlled.


## 📈 DNS Visibility & Threat Auditing in Infoblox Portal
==


Infoblox UDDI Portal provides detailed telemetry and context on every DNS security decision — from exfiltration attempts to blocked domains.

Head over to the Infoblox  UI:

Go to: Monitor → Reports → Security → Security Events

![Screenshot 2025-07-04 at 13.54.29.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/5896dfdf2f1f3dac503c09eee7e80c76/assets/Screenshot%202025-07-04%20at%2013.54.29.png)


You should see:

•	🔥 Domains like *.ai-medicine-data.com

•	🔒 Blocked by DNS policy

•	📉 Threat Level: Low

•	✖️ Response: NXDOMAIN

---

### 🛡️ Step 1: Validate Real-Time Blocking

🧠 What You Just Proved

You simulated a modern AI-assisted workflow — and validated that:
- ✅ DNS-layer policies protect against LLM-driven shadow IT
- ✅ AI-generated content can lead to domain risk exposure
- ✅ Infoblox blocks bad FQDNs even if they’ve never been seen before
- ✅ Your SOC can now monitor GenAI output at the DNS level — with zero agents, zero endpoint dependency


Go to: Monitor → Reports → Security → ThreatView

![Screenshot 2025-07-04 at 13.54.45.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/0cf88355b1c72e79266769278bfa87eb/assets/Screenshot%202025-07-04%20at%2013.54.45.png)

![Screenshot 2025-07-04 at 13.55.23.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/28f08a7037aa4ad3a0bcefbb41c0d2d4/assets/Screenshot%202025-07-04%20at%2013.55.23.png)


You’ll see:

•	🚨 Total Threats Detected
•	🎯 Top Threat Domains
•	✅ Action Taken: Blocked

### 📊 Step 2: Global Threat Visibility with Infoblox Security Dashboard

Once your GenAI DNS simulation is running and traffic is flowing, you can use the Infoblox Security Dashboard for a unified view of what’s happening across your environment.

From the Infoblox UI, go to:

**Monitor → Reports → Security → Security Dashboard**

![Screenshot 2025-07-04 at 13.58.32.png](https://play.instruqt.com/assets/tracks/uoielkrmzmtm/da9c34794c131dd7d4b43fac2545e8df/assets/Screenshot%202025-07-04%20at%2013.58.32.png)

This view gives you instant visibility into:

•	Total DNS Activity – including threat-associated queries

•	DNS Firewall Hits – how many queries were blocked by policy

•	Threat Activity – number of indicators triggered (including Custom Lists)

•	Action Taken – confirms enforcement (e.g., block vs. allow)

•	Top Threat Classes – e.g., CustomList entries like ai-medicine-data.com

•	Communication Threat Graphs – visualizes which domains were queried and blocked

•	Real-Time Traffic Trends – DNS query spikes when the Flask app is active

This dashboard is especially powerful in showcasing the impact of GenAI-driven applications. You’ll see spikes in DNS activity, associated blocks, and full lineage of threat domains tied to the AI queries.

> [!NOTE]
> 🔁 Pro Tip: Set the dashboard to auto-refresh every 15 minutes during a live demo and zoom in on the spike generated by the AI app traffic.

This step reinforces DNS as a control point for AI observability, threat prevention, and SOC-level visibility—all in real time.

### ✅ Summary

You’ve now validated:
- ✅ Client-side policy enforcement
- ✅ DNS resolver config via DHCP
- ✅ Blocked risky categories (gambling, adult)
- ✅ Real-time visibility in the Infoblox Portal
- ✅ Detection of DNS exfiltration attempts with feed-based policy

> Welcome to DNS-layer defense with full visibility. 🛡️

---

## Time for the Next Challenge

Click **NEXT**!
