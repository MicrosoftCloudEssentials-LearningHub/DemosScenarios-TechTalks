# Passing Parameters to a Notebook from a Pipeline - Quick Guide

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-03

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [What is Azure Data Factory?](https://learn.microsoft.com/en-us/azure/data-factory/introduction)
- [Quickstart: Get started with Azure Data Factory](https://learn.microsoft.com/en-us/azure/data-factory/quickstart-get-started)
- [Quickstart: Create a data factory by using the Azure portal](https://learn.microsoft.com/en-us/azure/data-factory/quickstart-create-data-factory)

</details>

## Create a Microsoft Fabric Workspace

1. **Sign in to Power BI**: Go to the Power BI Service and log in.
2. **Create a New Workspace**:
   - From the navigation pane, select `Workspaces`.
   - Click on `+ New workspace`.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/34fca476-6799-49b9-a1ce-a04384415305" />

   - In the `Create a workspace` pane, enter a name for your workspace.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/bf18ce14-bdf1-4c5a-a15d-54fe538dba02" />

   - Expand the `Advanced` section and choose either the Fabric capacity or Trial license mode.
   - Select `Apply` to create and open the new workspace

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/72789bb8-1e6f-4a34-b117-3127dc0e0eb8" />

## Create a Notebook with Parameters

1. Go to Your Workspace:
    1. **Sign in to Power BI**: Go to the Power BI Service and log in.
    2. **Navigate to Workspaces**: From the navigation pane, select `Workspaces`.
    3. **Select Your Workspace**: Choose the workspace where you want to create the new item.
2. Create a New Item
    1. **Click on New Item**: In your workspace, click on the `New item` button.
    2. **Choose the Item Type**: From the list of item types, select `Notebook`.

         <img width="550" alt="image" src="https://github.com/user-attachments/assets/c281bc81-7592-4f51-a4f5-20201cee2c70" />

3. Create and Configure the Notebook
    1. **Provide a Name**: Enter a name for your new notebook.
    2. **Configure the Notebook**: You can configure various settings for your notebook, such as the language (e.g., Python, Scala) and the environment.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/c9f4778c-4a64-4275-bdcd-24394484c908" />

4. Define Parameters in the Notebook
    1. **Open the Notebook**: Once the notebook is created, open it.
    2. **Define Parameters**: Add a cell to define the parameters you want to pass. For example:

        ```python
        # Parameters
        file_path = ""
        token = ""
        ```

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
