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

## Content

- [Create a Microsoft Fabric Workspace](#create-a-microsoft-fabric-workspace)
- [Create a Notebook with Parameters](#create-a-notebook-with-parameters)
- [Using the Notebook in a Pipeline](#using-the-notebook-in-a-pipeline)

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
        file_path = "abfss://<your-container-name>@<your-storage-account-name>.dfs.core.windows.net/<your-bronze-lakehousename>.Lakehouse/Tables/<table name>"
        token = ""
        ```
5. **Mark as Parameter Cell**: Select the `Toggle Parameter Cell` option to mark the cell as a parameter cell

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/540fa3cc-a896-41b5-a144-81955e130a67" />

6. Save and Use the Notebook
      1. **Save the Notebook**: Save your notebook to ensure all changes are applied.
      2. **Use the Notebook in a Pipeline**: You can now use this notebook in a pipeline and pass parameters to it as needed.

            <img width="550" alt="image" src="https://github.com/user-attachments/assets/1cf3afe3-8f74-4e1a-a1fe-e9d30418737e" />

## Using the Notebook in a Pipeline

1. **Open the Notebook**: Navigate to the notebook you created in your Microsoft Fabric workspace.
2. **Go to the Run Tab**: In the notebook view, click on the `Run` tab at the top of the page.
3. **Add to Pipeline**: Under the `Run*` tab, select the `Add to pipeline` option. This will allow you to add the notebook to a new or existing pipeline.
      1. **Create a New Pipeline**: If you don't have an existing pipeline, you can create a new one by providing a name and selecting **Create**.
      2. **Select an Existing Pipeline**: If you already have a pipeline, select it from the list of available pipelines.

            <img width="550" alt="image" src="https://github.com/user-attachments/assets/10037c04-2608-418c-9d26-cf1dafa5835c" />
      
            <img width="550" alt="image" src="https://github.com/user-attachments/assets/f99bdef2-25ac-474b-b164-90366696694a" />

4. Configure the Notebook Activity
      1. **Open Pipeline Editor**: Once the notebook is added to the pipeline, the pipeline editor will open.

            <img width="550" alt="image" src="https://github.com/user-attachments/assets/6b8dc57f-a228-417b-a2b6-ecb2410443cb" />

      2. **Select the Notebook Activity**: Click on the `Notebook activity` that was added to the pipeline.
      3. **Configure Parameters**: In the `Settings` tab of the `Notebook activity`, find the `Parameters` section. Add the parameters you want to pass to the notebook. Ensure the parameter names match the names defined in the notebook. For example:
          ```json
          {
              "file_path": "/path/to/your/file",
              "token": "your_token_here"
          }
          ```

https://github.com/user-attachments/assets/67c12ca6-0392-4313-9836-63ae6300154d

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
