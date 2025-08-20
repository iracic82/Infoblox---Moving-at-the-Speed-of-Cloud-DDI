---
slug: uddi-agility
id: 1l7jrkanrryx
type: challenge
title: Review and Enhance DNS + Security Policies
teaser: Review and Enhance DNS + Security Policies
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
- id: hdomtere8osv
  title: AWS Console
  type: browser
  hostname: aws
- id: kointaid9p1q
  title: Infoblox Portal
  type: browser
  hostname: infoblox
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
🔒 Challenge 3: Enhance DNS Security Policy with NIOS-X-as-a-Service
==

Your NIOS-X-as-a-Service instance is already deployed and integrated with your AWS VPC. DNS resolution is confirmed to be working — now it’s time to review the active DNS security protections and enforce stricter controls like blocking adult content.

### 🧩 Part 1: Review the Active Security Policy

Let’s begin by reviewing the Security Policy that is currently applied to your NIOS-X-as-a-Service deployment.
1.	Log into the Infoblox Universal DDI Console.
2.	Go to:
**Configure → Service Deployment → As-a-Service**
3.	Locate your existing NIOS-X-as-a-Service instance.
4.	Under the Service Capabilities, click on the Security section.
5.	Note the name of the assigned Security Profile (e.g., Default Global Policy).

![Screenshot 2025-07-13 at 11.12.47.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/2db58ceba2dbd1c07a9c4dfcb53ad51a/assets/Screenshot%202025-07-13%20at%2011.12.47.png)

6.	Navigate to:
**Configure → Security → Policies**
7.	Open the assigned policy and inspect existing rules and threat categories being enforced. Click the Hamburger Icon associated with the Default Global Policy, then click Edit.


![Screenshot 2025-07-13 at 11.14.05.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/9f0f7d46c217144cce8c03e95116e4d3/assets/Screenshot%202025-07-13%20at%2011.14.05.png)

![Screenshot 2025-07-13 at 11.14.14.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/dd5c74475d0b0b914ab9ce74383f5197/assets/Screenshot%202025-07-13%20at%2011.14.14.png)

🎯 Goal: Understand what DNS security protections are active — such as blocking malware, DNS tunneling, phishing, and C2 domains.


### 🔧 Part 2: Clone the Policy and Add Adult Content Block

Now you’ll take it a step further by cloning the policy and adding a rule to explicitly block adult content domains.

1.	In the Policies page, click the hamburger icon next to the Default Global Policy, then  → select Clone. Note by cloning the policy, you’re copying all existing policy rules and creating a new policy.

![Screenshot 2025-07-13 at 11.14.14.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/dd5c74475d0b0b914ab9ce74383f5197/assets/Screenshot%202025-07-13%20at%2011.14.14.png)

3.	Name the cloned policy: Infoblox-Lab.
4.	Click  the Policy Rules text in the left side-panel.
5.	Click Add Rule → choose Category Filter.

![Screenshot 2025-07-13 at 11.17.08.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/d34f2a5e71cbd036d45a4f37ac3a4179/assets/Screenshot%202025-07-13%20at%2011.17.08.png)

Scroll all the way to the bottom to locate the newly added row.

![Screenshot 2025-07-13 at 11.17.48.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/6dc47327f9951e65c86eb00bc2901632/assets/Screenshot%202025-07-13%20at%2011.17.48.png)

7.	In the dropdown → click New Category Filter
	•	Name it Adult
	•	Move the Adult category to the Selected column
	•	Set Action to: Block – No Redirect

	![Screenshot 2025-07-13 at 11.19.36.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/4583c945daa099518d57a8396c1ae565/assets/Screenshot%202025-07-13%20at%2011.19.36.png)

	![Screenshot 2025-07-13 at 11.19.11.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/f32ff01da8c304d9c84b7b886a73957d/assets/Screenshot%202025-07-13%20at%2011.19.11.png)


	6.	Click Add → and move the rule higher in the rule list (for precedence).
	7.	Click Finish → then Save your new policy.

🎯 Goal: Enforce enhanced corporate compliance by blocking access to explicit content domains, ensuring a safe and policy-compliant browsing environment for users across the organization.

This includes categories such as:
- Adult content
- Gambling
- Violence & Hate
- Illegal or unethical content

To achieve this, we leverage Infoblox Threat Intelligence feeds and DNS category filtering. Domains are automatically classified using real-time threat intel and reputation scoring — no manual blacklist needed.




### 🛠️ Part 3: Apply the Enhanced Security Policy to NIOS-X


1.	Navigate back to:
Configure → Service Deployment → As-a-Service
2.	Edit your existing NIOS-X-as-a-Service instance.
3.	Under Service Capabilities, locate Security → click Edit

![Screenshot 2025-07-13 at 11.22.58.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/5e9b279b407137462d09ca303f307b3e/assets/Screenshot%202025-07-13%20at%2011.22.58.png)

4.	From the Profile dropdown, select your new policy (Infoblox-Lab)

![Screenshot 2025-07-13 at 11.23.06.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/84ecb89847e4fc0b3ab73787bb8baf71/assets/Screenshot%202025-07-13%20at%2011.23.06.png)

6.	Click Update Capability → then click Save

🎯 Goal: Apply the enhanced policy to your service to start enforcing the new rules.


### 🧪 Part 4: Validate Policy Enforcement from EC2 (Adult Content Block)

Log back into your EC2 instance and test DNS resolution for an adult content domain — this will help verify that your security policy is being actively enforced.

To retrieve your EC2 instance details and SSH command, run:

```run
cd ~/infoblox-lab/secure-ai-infoblox/terraform
terraform output
```

This will display the SSH connection string you can use to access the instance.

![Screenshot 2025-07-13 at 11.25.17.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/48cfb7698db9a51ee14ec691764e5de3/assets/Screenshot%202025-07-13%20at%2011.25.17.png)

Use the SSH command provided by the previous terraform output step. The public IP address will vary per lab environment.

For example:
```
ssh -i 'EU_WEST_WebProd1.pem' ec2-user@18.171.44.117
```

🧠 Replace 18.171.44.117 with the actual IP shown in your output.


Once inside, try resolving a site like:

```run
dig +noall +answer +multiline bet365.com
```



🧪 This sends a DNS query for bet365.com, a known gambling domain (often categorized alongside adult or risky content depending on policy).


🔍 Expected Output

If the policy is active, you should see:

![Screenshot 2025-07-13 at 11.34.39.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/6981bcc57358999ec79b464e95a6f491/assets/Screenshot%202025-07-13%20at%2011.34.39.png)

📍 In the Infoblox Portal, navigate to:

**Monitor → Reports → Security → Security Activity** under Security Events

You’ll see entries like the one below confirming DNS Security enforcement is active:
•	Query: bet365.com
•	Class: CAT
•	Category: Gambling
•	Policy: Infoblox-Lab
•	Source: NIOS X (DPF)
•	Response: NXDOMAIN


![Screenshot 2025-07-13 at 11.34.10.png](https://play.instruqt.com/assets/tracks/26xnz6aweydm/f8d6634c5a21371bfca76d7cf86a192e/assets/Screenshot%202025-07-13%20at%2011.34.10.png)

This means the query was blocked — Infoblox Threat Defense returned NXDOMAIN, indicating that the domain resolution was denied by your applied DNS Security policy.

If you instead get a valid IP address, your policy might not be correctly applied or the category/rule isn’t matched — go back and review your Security Policy settings.


🧾 Lab Wrap-Up: Moving at the Speed of Cloud with NIOS-X-as-a-Service
==

In this challenge, you:
- Reviewed the DNS Security Profile assigned to your NIOS-X-as-a-Service deployment
- Cloned and customized the policy to block adult content
- Applied the updated profile to your NIOS-X-as-a-Service instance
- Verified DNS-based enforcement from your EC2 instance
- Observed live telemetry confirming Threat Defense in action

You now have a cloud-native, policy-enforced DNS layer running in AWS — deployable in minutes using NIOS-X-as-a-Service.
