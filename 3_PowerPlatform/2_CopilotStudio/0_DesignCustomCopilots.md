# How to build Custom Copilots with Copilot Studio - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Use entities and slot filling in copilots](https://learn.microsoft.com/en-us/microsoft-copilot-studio/advanced-entities-slot-filling)
- [Create and edit topics with Copilot](https://learn.microsoft.com/en-us/microsoft-copilot-studio/nlu-authoring#whats-supported?wt.mc_id=power-virtual-agents_inproduct)
- [Microsoft Power Automate documentation](https://learn.microsoft.com/en-us/power-automate/)
  
</details>

<details>
<summary><b>Table of Content</b> (Click to expand)</summary>

- [Overview](#overview)
- [Examples of types of copilots using Microsoft tools](#examples-of-types-of-copilots-using-microsoft-tools)
    - [Copilot Agents](#copilot-agents)
    - [Autonomous Copilots](#autonomous-copilots)
    - [Declarative Copilots](#declarative-copilots)
    - [Analytical Copilots](#analytical-copilots)
    - [Creative Copilots](#creative-copilots)
    - [Integrative Copilots](#integrative-copilots)
- [Demo](#demo)
    - [Configure your your environment and Create a Copilot](#configure-your-your-environment-and-create-a-copilot)
    - [Understanding Entities & Slot Filling](#understanding-entities--slot-filling)
    - [Copilot Studio to request data from another data source using Power Automate](#copilot-studio-to-request-data-from-another-data-source-using-power-automate)
    - [Benefits](#benefits)
    - [Use Cases](#use-cases)

</details>

## Overview 

> Copilot Studio on the Microsoft Power Platform introduces a user-friendly way to build and customize AI copilots using low-code/no-code tools, making AI solution development accessible for everyone. It simplifies task automation, enhances customer interactions, and improves workflow efficiency. 

| Feature                        | Description                                                                 | Example Use Case                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| **Build Custom AI Solutions**  | Easily create AI copilots that can assist with a variety of tasks.           | - Creating a chatbot to handle customer inquiries on your website. <br> - Developing an AI assistant to manage inventory and restocking. |
| **Enhance Productivity**       | Automate repetitive tasks and free up time for more strategic activities.    | - Setting up an AI to automatically sort and respond to emails. <br> - Using an AI copilot to generate regular reports and analytics. |
| **Improve Customer Engagement**| Develop AI-driven interactions that enhance customer service and satisfaction.| - Implementing an AI assistant to provide personalized product recommendations. <br> - Creating an AI-driven feedback system to gather and analyze customer opinions. |
| **Integrate Seamlessly**       | Connect your AI copilots with other Microsoft tools and services for a cohesive experience.| - Integrating an AI copilot with Microsoft Teams to assist with scheduling and reminders. <br> - Connecting AI solutions with Power BI for advanced data visualization. |

## Examples of types of copilots using Microsoft tools

### Copilot Agents

> **Tool**: Power Virtual Agents

**Steps**:
1. **Sign in to Power Virtual Agents**: Go to the Power Virtual Agents website and sign in with your Microsoft account.
2. **Create a New Bot**: Click on `Create a bot` and follow the prompts to set up your bot.
3. **Define Topics**: Add topics that your bot will handle. Topics are the different areas of conversation your bot can engage in.
4. **Build Conversations**: Use the graphical interface to design the conversation flow for each topic.
5. **Test and Publish**: Test your bot to ensure it works as expected, then publish it to make it available to users.

### Autonomous Copilots

> **Tool**: Power Automate

**Steps**:
1. **Sign in to Power Automate**: Go to the Power Automate website and sign in with your Microsoft account.
2. **Create a Flow**: Click on `Create` and choose the type of flow you want to build (e.g., automated, instant, scheduled).
3. **Add Triggers and Actions**: Define the trigger that starts the flow and add the actions that the flow will perform.
4. **Configure Details**: Set up the details for each action, such as specifying conditions and data inputs.
5. **Test and Activate**: Test your flow to ensure it works correctly, then activate it to start running.

### Declarative Copilots

> **Tool**: Power Automate

**Steps**:
1. **Sign in to Power Automate**: Go to the Power Automate website and sign in with your Microsoft account.
2. **Create a Flow**: Click on `Create` and choose the type of flow you want to build.
3. **Define Rules**: Use the graphical interface to set up rules and conditions that dictate how the flow operates.
4. **Add Actions**: Specify the actions that the flow will take based on the defined rules.
5. **Test and Deploy**: Test your flow to ensure it follows the rules correctly, then deploy it.

### Analytical Copilots

> **Tool**: Power BI

**Steps**:
1. **Sign in to Power BI**: Go to the Power BI website and sign in with your Microsoft account.
2. **Import Data**: Connect to your data sources and import the data you want to analyze.
3. **Create Reports**: Use the Power BI interface to create reports and dashboards that visualize your data.
4. **Add Insights**: Use Power BI's AI features to add insights and predictive analytics to your reports.
5. **Share and Collaborate**: Share your reports with others and collaborate on data analysis.

### Creative Copilots

> **Tools**: Microsoft Designer, Microsoft 365 Apps

**Steps**:
1. **Sign in to Microsoft Designer**: Go to the Microsoft Designer website and sign in with your Microsoft account.
2. **Create a New Project**: Start a new design project and choose a template or create from scratch.
3. **Add Content**: Use the design tools to add text, images, and other content to your project.
4. **Use AI Features**: Leverage AI-driven suggestions and tools to enhance your design.
5. **Save and Share**: Save your design and share it with others.

### Integrative Copilots

> **Tools**: Power Platform, Microsoft Teams, Power BI

**Steps**:
1. **Identify Integration Points**: Determine which Microsoft tools and services you want to integrate.
2. **Create Flows**: Use Power Automate to create flows that connect different tools and automate tasks.
3. **Set Up Connectors**: Use connectors to link your AI copilots with other Microsoft services like Teams and Power BI.
4. **Configure Actions**: Define the actions that your copilot will take within the integrated environment.
5. **Test and Implement**: Test the integrations to ensure they work seamlessly, then implement them.

## Demo 

### Configure your your environment and Create a Copilot

- Go to [Microsoft Copilot Studio Home Page](https://copilotstudio.microsoft.com/)
- Prompt your case, for example:

  ```text
  I'm planning to develop a support copilot for our Contoso customers. This tool will assist by providing answers to frequently asked questions and performing routine tasks, such as order status updates.
  ```

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/db23a02f-6000-43b7-8617-af4504faa040">

- Setup your Copilot Name, Icon, description and instructions:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/2197193b-d91e-4a2a-8078-251441c06e3a">

  ```
  - Information should come from https://learn.microsoft.com/en-us/microsoft-copilot-studio/ and from https://www.microsoft.com/en-us/microsoft-copilot/
  - Maintain a professional, cheerful tone focused on our clients, avoiding any mention of competitors or comparisons with their products.
  ```

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/3de35622-6af0-4dc8-b383-2c39e347bee7">

  > You will see a screen like this while you wait to Copilot to create your bot:
  
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/028904ba-88c5-418b-9203-bc879b640b97">

  > You can see it by the `Copilots` section:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/d828671c-eb5b-4049-95f0-32ee8b46ccd5">

- You can keep configuring different settings available:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/e7bd4c43-7e2d-46e9-a37b-3cc4f6f41a51">

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/b680d628-6462-4728-bec2-6957ee2fa065">

- Create topics if needed:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/ee2f4108-7698-4ede-8b99-ff0418dbb7d2">

  > It will look like this:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/94dd43e1-02b5-4468-8b82-38745492356a">

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/4b9b6ec4-69bd-45c6-bea3-554e3d7d064d">

- Before you publish your copilot, please navigate to the `Security` section and adjust the `Authentication` settings according to your requirements:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/047ac431-27c4-4ab0-913e-bc80004dd962">

- Once you are ready, `Publish` your own Copilot:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/c1f5deb9-8541-4fbf-9208-c354fc72e4f8">

### Understanding Entities & Slot Filling

| Concept       | Description                                                                 | Example                                                                                   |
|---------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **Entities**  | Key pieces of information that the AI copilot needs to understand and extract from user inputs. | - **Examples**: Names, dates, locations, product names, quantities. <br> - **Usage**: "Book a flight to New York for tomorrow" (Entities: "New York" - location, "tomorrow" - date). |
| **Slot Filling** | The process of collecting all necessary entities (or slots) required to complete a task. The AI copilot asks follow-up questions to gather any missing information. | - **Example**: For booking a flight, the copilot might need the departure city, destination city, date, and time. If the user only provides the destination, the copilot will ask for the remaining details. <br> - **Scenario**: Booking a meeting room. <br> **Entities**: Date, time, room number, duration. <br> **User Input**: "I need a room for a meeting tomorrow." <br> **Slot Filling**: <br> - Copilot: "What time is the meeting?" <br> - User: "At 3 PM." <br> - Copilot: "How long will the meeting last?" <br> - User: "2 hours." <br> - Copilot: "Which room would you like to book?" <br> - User: "Room 101." |

- Go to `Settings` in top-right corner, and select `Entities`. Then select `Add` an entity and `New entity`.

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/b543c6ff-ac7c-4b6b-9268-d9bacd301a02">

- You can choose between `Closed list` or `Regular expression (Regex)`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/9171775c-140b-4a2c-b344-a1bbda1f46c1">

  > If you choose `Closed list` you will se a window like this:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/562c8b59-6f42-46ab-b634-9209f695ea71">

- You can add that `Entity` to the `Topic`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/bfd4ce79-59c4-4bbf-86e5-62a776dcaa5c">


  <img width="550" alt="image" src="https://github.com/user-attachments/assets/53155f54-de30-462a-a0c8-3cae98d05758">

- You can test the `Slot Filling`, by having the `Variables` window open:

  <video src='https://github.com/user-attachments/assets/625d865d-6259-4b07-8d6c-565c0d3675d1' width=180/>

- You can access the code editor:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/3918e5a0-6ef7-4898-a84d-a0e6630f37c3">

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/011e6cb9-e779-4852-9277-1038600eecab">

### Copilot Studio to request data from another data source using Power Automate

> Microsoft Power Automate (formerly known as Microsoft Flow) is a cloud-based service that enables users to `create automated workflows between their favorite apps and services`. This helps streamline repetitive tasks, integrate various systems, and improve overall productivity.

| **Category**               | **Key Features**                                                                                     |
|----------------------------|-----------------------------------------------------------------------------------------------------|
| **Automate Workflows**     | - **Cloud Flows**: Automate tasks across cloud services like Office 365, Dynamics 365, and third-party applications.<br>- **Desktop Flows**: Automate tasks on your desktop, such as data entry and file management, using robotic process automation (RPA). |
| **Integration**            | - **Connectors**: Power Automate offers hundreds of connectors to integrate with various services and applications, including SharePoint, Outlook, Twitter, and more.<br>- **Custom Connectors**: Create custom connectors to integrate with proprietary or less common services. |
| **AI Capabilities**        | - **AI Builder**: Incorporate AI models into your workflows to automate tasks like form processing, object detection, and sentiment analysis. |
| **User-Friendly Interface**| - **Templates**: Start with pre-built templates to quickly create common workflows.<br>- **Drag-and-Drop**: Use a visual designer to build workflows without writing code. |

### **Benefits**

| **Benefit**     | **Description**                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **Efficiency**  | Automate repetitive tasks to save time and reduce human error.                                       |
| **Productivity**| Focus on higher-value tasks by offloading routine processes to automated workflows.                  |
| **Scalability** | Easily scale your automation efforts as your business grows.                                         |

### **Use Cases**

| **Use Case**                  | **Description**                                                                                     |
|-------------------------------|-----------------------------------------------------------------------------------------------------|
| **Business Process Automation**| Automate approval processes, notifications, and data synchronization.                               |
| **Data Collection**           | Automatically collect and process data from various sources.                                       |
| **Integration**               | Seamlessly integrate different systems and applications to ensure data consistency and streamline operations. |

> Example of connecting to Snowflake

- Create `Add a topic`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/4cb1a631-1374-4d97-a5c2-2afd82c65b29">

- Click `+`. amd a `Question`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/4d79dba2-4a12-4edb-971f-ef613fb2e3d1">

- Add some description around the topics:
    
  <img width="550" alt="image" src="https://github.com/user-attachments/assets/3eec2fde-9857-47d3-b402-2d4aff37dfa0">

  ```text
  Yes, I can get you the status of your receipt. What is your receipt number?
  ```

- Add and `Identity`, click on `Create an Entity`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/5113e492-460c-4089-83ce-8aa24f18dfba">

  > Choose between `Closed list`, or  `Regular expresion (Regex)`:

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/881f8773-bc09-4fd3-bd3d-c4693f5f69dc">

  > Add you `name, description` and `list items`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/190e6100-7da9-415d-bd11-c8e22ee8925a">

  > Adjust the variables properties as required, and click on `Save`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/9c7ceb8d-7f16-420f-8a41-539fc3c23b61">

- Add Power Automate cloud flow:

  > Click on `+`, `Call an action `, and `Create a flow`:
  
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/bbc59a26-de56-4b45-b770-cf95696a9e3b">

  > An Power Automate window will open:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/4c8c6107-9d3b-4702-a4a6-d7cb282135cd">

  > Click on `When Copilot Studio calls a flow`, to `Add an input`:
  
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/2e5b7c11-9b83-48d2-a2b7-f17734d08b22">
  
  > For this example, click on `Text` and add `ReceiptNumber`:

    <img width="379" alt="image" src="https://github.com/user-attachments/assets/72504c97-8a86-4472-9f2a-8aed95b9379a">

  > CLick on `Collapse` and `+`, so we can add a new action:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/0d0f5639-ecae-409e-b02b-4c53ad8b118d">

  > `Add an action`:
  
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/1d679711-2fef-484b-be42-2207b0d74f40">

  > Search for `Azure AI Search`, in this example we'll indexing a document:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/871f142d-5227-4416-a5f9-707d06b9f4a8">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/af6b08b7-c248-490f-a77e-6d834ae7209a">

  > Fill the information and click on `Create new`:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/15c129a3-538c-492d-a31e-d9c72559931c">

  > Add the `Parameters`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/46dd9a30-f60b-4e16-890c-e9f309abfc69">

  > Add `Action timeout`, and turn on `Security` features:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/389514a5-915a-4306-a4a5-6a8c85198ea8">

  > You can add `Status`, and `Outputs` for testing, then click on `Save`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/5067efc0-5780-4d68-8f32-69a5faba1ef7">

  > `Add an output` to the `Return values(s) to Power Virtual Agents`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/411f8aa4-0250-4fea-a592-a86271ba79e4">


  > Once you add all your desired output parameters, click on `Save`:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/1be27b5b-1a0b-438b-a57d-d9af2509164f">

  > Adjust the name of the `Power Automate Flow` as desired, click on `Save` to change the name:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/0241aa6b-7ddf-4967-bf3d-fe45fe561dcd">

  > Go back to , click on `+`, `Call an action`, and you'll see your recently created flow:

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/655cd3e7-753c-4894-b2d3-e66a843aaa76">

  > You'll see `action` created, click on `Enter or select a value`, select the `variable` created:
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/b52028a9-6be5-477e-8722-554dd579d76d">


<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1633-limegreen" alt="Total views">
  <p>Refresh Date: 2025-12-03</p>
</div>
<!-- END BADGE -->
