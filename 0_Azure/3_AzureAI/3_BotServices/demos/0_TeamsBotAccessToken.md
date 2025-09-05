# Retrieving Access Token from Team's bot

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

---------------

## Wiki 

- [Add authentication to a bot](https://learn.microsoft.com/en-us/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=userassigned%2Caadv2%2Ccsharp)
- [Teams Auth Bot](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-teams-authentication/python)
- [TeamsFx SDK](https://learn.microsoft.com/en-us/microsoftteams/platform/toolkit/teamsfx-sdk)

## Ideas on How to Implement it:

Here’s are some ideas on how you can retrieve an access token for Microsoft Graph calls within a Teams chat using Bot Framework:

### BotFrameworkAdapter’s GetUserTokenAsync (Python example):

| Pros | Cons |
| ---- | ---- | 
| - **Flexibility**: Using the `BotFrameworkAdapter`, you have more control over the authentication flow and token retrieval process. <br/> - **Customization**: You can customize error handling, logging, and other aspects of token retrieval. <br/> - **Generalization**: This approach isn't tied exclusively to Teams; it can be used for other scenarios as well. |     - **Additional Complexity**: Implementing token retrieval and handling requires more code and understanding of OAuth flows. <br/> - **Manual Token Management**: You'll need to manage tokens explicitly, which can be more work. |


In Python, utilize the BotFrameworkAdapter class to obtain the token after the following steps:
1. Setting up OAuth 2.0 authentication with Azure AD v1 or v2. 
2. Apply the code to fetch the user's token, see an example below:

```python
from botbuilder.core import BotFrameworkAdapter
from botbuilder.schema import TokenResponse

# Initialize your BotFrameworkAdapter
adapter = BotFrameworkAdapter()

# Replace 'connection_name' with the appropriate connection name
connection_name = 'your_connection_name'

async def get_user_token(context):
    try:
        result: TokenResponse = await adapter.get_user_token(
            context, connection_name, None
        )
        if result and result.token:
            # Use 'result.token' for your Microsoft Graph API calls
            return result.token
        else:
            # Handle case where token retrieval failed
            return None
    except Exception as ex:
        # Handle exceptions (e.g., user hasn't signed in)
        return None

# Usage example:
user_token = await get_user_token(context)
if user_token:
    # Make your Microsoft Graph API calls using 'user_token'
    pass
else:
    # Handle case where token retrieval failed
    pass
```

### Teams Authentication Library (TeamsFx):

The Teams Authentication Library, also known as TeamsFx, is a powerful tool for integrating authentication into your Microsoft Teams applications. The Teams Toolkit (TeamsFx) offers built-in authentication features. You can set up authentication providers like Azure Entra ID directly in your Teams app manifest. This ensures that when users interact with your bot, Teams manages the authentication process and issues an access token.

| **Pros** | **Cons** |
|----------|----------|
| **Built-in Authentication**: Simplifies the process of setting up authentication providers like Azure Entra ID directly in your Teams app manifest. | **Dependency on Teams SDK**: Requires your bot to be built using the Teams SDK. |
| **Seamless Integration**: Teams manages the authentication process and issues an access token, enhancing user experience. | **Limited Customization**: Abstracts some implementation details, which may limit customization options. |
| **Single Sign-On (SSO)**: Supports SSO, allowing users to authenticate once and access multiple services without logging in again. | **Learning Curve**: May require some learning to understand and implement correctly. |
| **Cross-Platform Support**: Can be used in both client and server environments, including browser and Node.js. | **Complex Configuration**: Setting up the app manifest and configuring authentication providers can be complex. |
| **Simplified Code**: Reduces the complexity of writing authentication code, often down to single-line statements. | **Potential Security Risks**: Misconfiguration can lead to security vulnerabilities. |

Here’s an example of how to use TeamsFx for Single Sign-On (SSO) in a Teams bot application:

1. Install the TeamsFx SDK:

```bash
pip install msal requests
```

2. Set Up Your Bot: In your bot’s code, you need to configure the MSAL (Microsoft Authentication Library) to handle authentication.

```python
from msal import ConfidentialClientApplication
import requests

# Initialize the MSAL confidential client application
client_id = 'your-azure-ad-app-id'
client_secret = 'your-client-secret'
authority = 'https://login.microsoftonline.com/your-tenant-id'
scope = ['https://graph.microsoft.com/.default']

app = ConfidentialClientApplication(client_id, authority=authority, client_credential=client_secret)

# Function to get an access token
def get_access_token():
    result = app.acquire_token_for_client(scopes=scope)
    if 'access_token' in result:
        return result['access_token']
    else:
        raise Exception("Could not acquire token: " + result.get("error_description"))

# Function to get user profile
def get_user_profile(access_token):
    headers = {'Authorization': 'Bearer ' + access_token}
    response = requests.get('https://graph.microsoft.com/v1.0/me', headers=headers)
    return response.json()

# Example usage
access_token = get_access_token()
user_profile = get_user_profile(access_token)
print(f"Hello {user_profile['displayName']}!")
```

3. Configure Authentication in Teams App Manifest: Update your Teams app manifest to include the necessary authentication settings. This ensures that Teams can handle the authentication flow and issue tokens.

```json
{
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    "id": "your-app-id",
    "packageName": "com.example.yourapp",
    "developer": {
        "name": "Your Name",
        "websiteUrl": "https://yourwebsite.com",
        "privacyUrl": "https://yourwebsite.com/privacy",
        "termsOfUseUrl": "https://yourwebsite.com/terms"
    },
    "description": {
        "short": "Your app description",
        "full": "Your app full description"
    },
    "permissions": [
        "identity",
        "message",
        "team",
        "channel",
        "groupchat"
    ],
    "validDomains": [
        "yourwebsite.com"
    ],
    "webApplicationInfo": {
        "id": "your-azure-ad-app-id",
        "resource": "https://yourwebsite.com"
    }
}
```

### Retrieving information based on Meeting ID:

TeamsInfo class retrieves meeting information based on the meeting ID

| Pros | Cons |
| ---- | ---- | 
| - **Simplicity**: The `TeamsInfo` class offers a straightforward method to retrieve meeting details directly using the meeting ID. <br/> - **Built-in Functionality**: Specifically designed for Teams scenarios, it integrates seamlessly with Teams features. <br/> - **Access to Join URLs**: Easily access join URLs, participants, and other meeting-related information. | - **Limited Customization**: The `TeamsInfo` class abstracts some implementation details, potentially limiting customization options. <br/> - **Dependency on Teams SDK**: Your bot must be built using the Teams SDK to utilize this approach. |

Here is an example: 

``` python
from botbuilder.core import BotFrameworkAdapter, TurnContext
from botbuilder.schema import MeetingInfo, TeamsInfo

async def get_meeting_info(turn_context: TurnContext, meeting_id: str = None) -> MeetingInfo:
    try:
        # Call the get_meeting_info method
        result: MeetingInfo = await TeamsInfo.get_meeting_info(turn_context, meeting_id)
        if result:
            # Process the meeting info (e.g., access join URL, participants, etc.)
            return result
        else:
            # Handle case where meeting info retrieval failed
            return None
    except Exception as ex:
        # Handle exceptions (e.g., invalid meeting ID)
        return None

# Usage example:
meeting_id = "your_meeting_id"
meeting_info = await get_meeting_info(context, meeting_id)
if meeting_info:
    # Process the meeting info
    pass
else:
    # Handle case where meeting info retrieval failed
    pass
```

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->