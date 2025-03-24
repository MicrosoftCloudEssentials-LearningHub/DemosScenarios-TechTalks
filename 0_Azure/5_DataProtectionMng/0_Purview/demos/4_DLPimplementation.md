# Data Loss Prevention (DLP) in Azure Purview - How to configure it 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-19

----------

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

## Define Policy Scope

- Select the locations where the policy will apply (e.g., Exchange email, SharePoint sites, OneDrive accounts, Teams chat).
- Specify the users or groups the policy will target.

## Configure Policy Settings

- **Sensitive Information Types**: Choose the types of sensitive information the policy will detect (e.g., credit card numbers, social security numbers).
- **Conditions**: Set conditions for when the policy should trigger (e.g., when sensitive information is shared externally).
- **Actions**: Define actions to take when a policy violation occurs (e.g., block sharing, send alerts, notify users).

## Set Up Alerts and Notifications

- Configure alerts to notify administrators and users when a policy violation occurs.
- Customize notification messages to inform users about the policy and the actions taken.

## Test and Deploy the Policy

- **Test Mode**: Initially deploy the policy in test mode to monitor its impact without enforcing actions.
- **Review Results**: Analyze the test results and adjust the policy settings as needed.
- **Enforce Policy**: Once satisfied with the configuration, switch the policy to enforce mode.

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
