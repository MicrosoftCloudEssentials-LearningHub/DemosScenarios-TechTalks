# Microsoft Fabric: Automating Pipeline Execution with Activator

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-05

----------

> This process shows how to set up Microsoft Fabric Activator to automate workflows by detecting file creation events in a storage system and triggering another pipeline to run.

<details>
<summary><b>List of References </b> (Click to expand)</summary>

</details>


## Set Up the First Pipeline

1. **Create the Pipeline**:
   - In [Microsoft Fabric](https://app.fabric.microsoft.com/), create the first pipeline that performs the required tasks.

> [!NOTE]
> This code generates random data with fields such as id, name, age, email, and created_at, organizes it into a PySpark DataFrame, and saves it to a specified Lakehouse path using the Delta format. 

https://github.com/user-attachments/assets/95206bf3-83a7-42c1-b501-4879df22ef7d

   - Add a `Copy Data` activity as the final step in the pipeline.

2. **Generate the Trigger File**:
   - Configure the `Copy Data` activity to create a trigger file in a specific location, such as `Azure Data Lake Storage (ADLS)` or `OneLake`.
   - Ensure the file name and path are consistent and predictable (e.g., `trigger_file.json` in a specific folder).
3. **Publish and Test**: Publish the pipeline and test it to ensure the trigger file is created successfully.

https://github.com/user-attachments/assets/798a3b12-c944-459d-9e77-0112b5d82831

## Configure Activator to Detect the Event

> [!TIP]
> Event options:

https://github.com/user-attachments/assets/022c195f-5af0-4382-8f57-c2efe6728e54

1. **Set Up an Event**:
   - Create a new event to monitor the location where the trigger file is created (e.g., ADLS or OneLake). In your workspace, click on `+ New Item` and create an `Activator`.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/076d6cde-2579-4f17-a426-27f7dbabbfb8" />

   - Choose the appropriate event type, such as `File Created`.

2. **Test Event Detection**:
   - Save the event and test it by manually running the first pipeline to ensure Activator detects the file creation.
   - Check the **Event Details** screen in Activator to confirm the event is logged.

---

### **Step 3: Define the Rule in Activator**
1. **Create a New Rule**:
   - In Activator, create a rule that responds to the event you just configured.
   - Set the condition to match the event details (e.g., file name, path, or metadata).

2. **Set the Action**:
   - Configure the rule to trigger the second pipeline.
   - Specify the pipeline name and pass any required parameters.

3. **Save and Activate**:
   - Save the rule and activate it.
   - Ensure the rule is enabled and ready to respond to the event.

---

### **Step 4: Set Up the Second Pipeline**
1. **Create the Pipeline**:
   - In Microsoft Fabric, create the second pipeline that performs the next set of tasks.
   - Ensure it is configured to accept external triggers.

2. **Publish the Pipeline**:
   - Publish the second pipeline and ensure it is ready to be triggered.

---

### **Step 5: Test the Entire Workflow**
1. **Run the First Pipeline**:
   - Execute the first pipeline and verify that the trigger file is created.

2. **Monitor Activator**:
   - Check the **Event Details** and **Rule Activation Details** in Activator to ensure the event is detected and the rule is activated.

3. **Verify the Second Pipeline**:
   - Confirm that the second pipeline is triggered and runs successfully.

---

### **Step 6: Troubleshooting (If Needed)**
- If the second pipeline does not trigger:
  1. Double-check the rule configuration in Activator.
  2. Verify that the second pipeline is set to accept external triggers.
  3. Review the logs in Activator for any errors or warnings.

---

Would you like me to assist with any specific step, such as configuring the event or rule in Activator?


<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

