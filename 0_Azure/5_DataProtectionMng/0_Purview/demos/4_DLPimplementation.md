# Data Loss Prevention (DLP) in Azure Purview - How to configure it 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-24

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>
  
- [Learn about the new Microsoft Purview portal](https://learn.microsoft.com/en-us/purview/purview-portal)
- [Microsoft Purview compliance portal](https://learn.microsoft.com/en-us/purview/purview-compliance-portal)

</details>

## Access the Microsoft Purview Compliance Portal

- Go to the [Microsoft Purview portal](https://purview.microsoft.com/).
- Sign in with your administrator credentials.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/8c39f351-c098-4858-9e41-96c8b91de5b1">

## Create a DLP Policy

- Go to `Data loss prevention`

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/da6ef80f-7ca8-456a-993d-a6d40bb28c53" />


- Select `Policies` > `Create policy`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/85f706eb-276e-4f7f-998f-f44bcf8fbfc3" />

- Choose a template or create a custom policy based on your organization's needs.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/b4128763-851e-46ee-8a74-fdf189fa8762">


## Define Policy Scope

- Select the locations where the policy will apply (e.g., Exchange email, SharePoint sites, OneDrive accounts, Teams chat).
- Specify the users or groups the policy will target.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/bdc69781-9f9b-464b-b8dd-b15198c11a25" />

## Configure Policy Settings

- **Sensitive Information Types**: Choose the types of sensitive information the policy will detect (e.g., credit card numbers, social security numbers).
- **Conditions**: Set conditions for when the policy should trigger (e.g., when sensitive information is shared externally).
- **Actions**: Define actions to take when a policy violation occurs (e.g., block sharing, send alerts, notify users).

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/bab1c3cf-2bc0-4646-aa8f-92805d68e30f" />

        
  https://github.com/user-attachments/assets/a9165b97-f197-4f37-877e-9776015a3297


## Set Up Alerts and Notifications

- Configure alerts to notify administrators and users when a policy violation occurs.
- Customize notification messages to inform users about the policy and the actions taken.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/a827175b-8520-4b01-8d26-e95e599850db">
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/5b44727d-013a-45f6-9e57-91bd4294cf0e" />

## Customize access and override settings

https://github.com/user-attachments/assets/eb3d57d3-5bef-43f2-b069-1d25c3ef047b

## Test and Deploy the Policy

- **Test Mode**: Initially deploy the policy in test mode to monitor its impact without enforcing actions.
- **Review Results**: Analyze the test results and adjust the policy settings as needed.
- **Enforce Policy**: Once satisfied with the configuration, switch the policy to enforce mode.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/944945f0-ad0c-49ea-b157-47613c48590b" />

    https://github.com/user-attachments/assets/0a38b331-33e8-4e15-96be-3edbe79119f6

## Monitor and Manage Policies

- Regularly review policy performance and adjust settings based on new threats or changes in business needs.
- Use the DLP reports and dashboards to track policy effectiveness and compliance.

## Advanced Configuration (Optional)

- **Endpoint DLP**: Configure settings for endpoint devices to restrict actions like copying, printing, or transferring sensitive data
- **Integration with Microsoft Defender**: Extend DLP alerts to Microsoft Defender XDR and Microsoft Sentinel for advanced threat detection and response
     
<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
