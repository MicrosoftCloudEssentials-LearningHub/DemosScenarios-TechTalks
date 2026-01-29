# Integrating Azure Language Services with Power Automate - Demo

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 
- [Use the Language service in Power Automate](https://learn.microsoft.com/en-us/azure/ai-services/language-service/tutorials/power-automate)
  
## How to 

-  Step 1: Create a Language Resource in Azure
    1. **Sign in to Azure Portal**:
       - Go to Azure portal.
       - Use your credentials to sign in.
    2. **Create a New Resource**:
       - Click on **Create a resource** in the left-hand menu.
       - In the search bar, type **Language** and select **Language** from the list.
       - Click **Create**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/ba0aed0d-2602-4c5a-bdf4-8bb3e9cc4dbc">

    3. **Configure the Resource**:
       - Fill in the necessary details like **Subscription**, **Resource Group**, **Region**, and **Name**.
       - Choose the **Pricing tier** that suits your needs.
       - Click **Review + create** and then **Create**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/36df57ee-c617-4bb4-9979-8ebc123ab3f8">

    4. **Retrieve Endpoint and Key**:
       - Once the resource is created, navigate to it.
       - In the left-hand menu, select **Keys and Endpoint**.
       - Note down the **Key1** and **Endpoint**. You will need these for Power Automate.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/3ec37ce5-6d61-434b-9fdf-d0364a0c8c07">

-  Step 2: Set Up Power Automate Flow
    1. **Sign in to Power Automate**:
       - Go to Power Automate.
       - Use your credentials to sign in.
    2. **Create a New Flow**:
       - Click on **My flows** in the left-hand menu.
       - Select **New flow** and then **Automated cloud flow**.
       - Name your flow and click **Skip** to continue without choosing a trigger.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/2585ebbd-28c1-4dc8-bea4-363258322fd4">

    3. **Add a Trigger**:
       - Under **Triggers**, select **Manually trigger a flow**.
       - Click **Create**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/c6ae9f68-4fe8-48b4-8b7a-5608685622fe">

-  Step 3: Add Language Service Connector
    1. **Add a New Step**:
       - Click on **+ New step**.

          <img width="550" alt="image" src="https://github.com/user-attachments/assets/b41445b2-224f-4f85-b169-d255c098ed50">

       - In the search bar, type **Azure AI Language**.

          <img width="550" alt="image" src="https://github.com/user-attachments/assets/94f8781a-75a8-4133-acaf-c1099b330d39">

    2. **Select an Action**: Choose the action you need, such as **Named Entity Recognition** or any other relevant action.
      
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/4a2b6642-6954-44c7-97d3-6eea0acb23a7">

    3. **Authenticate the Connector**:
       - You will be prompted to enter the **Endpoint** and **Key** from the Language resource you created in Azure.
       - Enter these details to authenticate.

          <img width="550" alt="image" src="https://github.com/user-attachments/assets/291bc6ea-c00a-4e05-b538-863de06749c8">
  
          ```
          DUMMY TEXT
  
          In a small village, there was a young person who loved exploring the forest nearby. 
          One day, they found a hidden path that led to a beautiful meadow filled with colorful flowers and butterflies.
          They spent hours there, enjoying the beauty of nature. This place became their secret spot of peace and happiness.
          ```
  
          <img width="550" alt="image" src="https://github.com/user-attachments/assets/6367aada-d379-40fd-9dc7-cb0ad5cd05d7">

-  Step 4: Integrate with OCR Engine
    1. **Add Another Step**:
       - Click on **+ New step**.
       - In the search bar, type **Computer Vision**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/227b9d28-6da2-4d59-8e9d-c7632b8192be">

    2. **Select an OCR Action**: Choose the action you need, such as **Read** or **Recognize Text**.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/93949f66-cb8c-4bad-bd39-6c443ea92790">

    3. **Authenticate the Connector**: Enter the **Endpoint** and **Key** from your Computer Vision resource in Azure.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/a71e3a50-f1c9-4ea7-9b38-20818bafd919">

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/fb77dccc-dc99-4548-a2ce-e92168ff4682">

        > Example of use:

        ```
        https://github.com/microsoft/.github/blob/main/images/open-at-microsoft.png
        ```

-  Step 5: Test Your Flow
    1. **Save Your Flow**: Click **Save** at the top right corner.
    2. **Test the Flow**:
       - Click **Test** from the top navigation menu.
       - Follow the prompts to test your flow and ensure it works as expected.
        
        > Dummy image
        
          <img width="550" alt="image" src="https://github.com/user-attachments/assets/c0457ecc-5819-47d0-b325-29e3dee35191">
        
          <img width="550" alt="image" src="https://github.com/user-attachments/assets/8195f173-d871-4576-87a3-59cdc925e7bb">
        
          <img width="550" alt="image" src="https://github.com/user-attachments/assets/377443ed-c343-40d6-ad46-12db4104e276">
        
          <img width="550" alt="image" src="https://github.com/user-attachments/assets/3427dd72-2ca3-4d6b-b3cf-867b933c3c3e">

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->