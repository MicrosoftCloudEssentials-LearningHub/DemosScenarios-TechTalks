# Important Changes to App Service Managed Certificates: Is Your Certificate Affected? - Overview 


Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> [!IMPORTANT]
> Please review this article first: [Important Changes to App Service Managed Certificates: Is Your Certificate Affected?](https://techcommunity.microsoft.com/blog/appsonazureblog/important-changes-to-app-service-managed-certificates-is-your-certificate-affect/4435193)

> [!NOTE]
> For the scenarios outlined in the article, please find an alternative set of queries to help you determine whether your environment might be impacted. These queries include visual guidance for reference.
> If you have any questions or need further clarification, please reach out to your Microsoft account team or contact Microsoft directly: [Microsoft Sales and Support](https://support.microsoft.com/contactus?ContactUsExperienceEntryPointAssetId=S.HP.SMC-HOME) for additional support and guidance, or

## Your site is not publicly accessible

> Please find below some examples of how it looks:

<details>
<summary><b> Public Network </b> (Click to expand)</summary>

<img width="700" alt="image" src="https://github.com/user-attachments/assets/b81befa9-a84b-40fc-9268-23bce1da7b5e" /> 
 
<img width="700" alt="image" src="https://github.com/user-attachments/assets/4b6c7b74-7dd7-4877-b340-e800ae675a48" />

</details>

<details>
<summary><b> Private Network </b> (Click to expand)</summary>

<img width="700" alt="image" src="https://github.com/user-attachments/assets/ac55c945-1b01-4687-a417-29bb87a19508" /> 
 
<img width="700" alt="image" src="https://github.com/user-attachments/assets/477e8b23-c43f-425e-a3ef-93a46bad37a7" />

<img width="700" height="962" alt="image" src="https://github.com/user-attachments/assets/aaf516b2-a081-4a84-a13c-bd5b3fc47b60" />

</details>

> You’re affected if public accessibility is blocked in any of these ways:
> - `Public network access = Disabled`
> - `Private endpoints` only (VNet-only access)
> - `IP restrictions` that `don’t allow the CA’s HTTP challenge`
> - `Client-certificate enforcement` on incoming requests

[This query](./query-how_to_know_if_your_site_is_not_publicly_accessible.kql), finds any App Service that meets any of those four conditions

https://github.com/user-attachments/assets/13cac993-764f-4fb7-972e-3c54d2f3cb8f

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->
