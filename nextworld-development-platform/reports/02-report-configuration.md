---
<a name="Back_To_Top"></a> Top
---

- ### [Report Configuration](#Report_Configuration)
- ### [Flattened Table Report Configuration](#Flattened_Table_Report_Configuration)
- ### [Report Application Link Configuration](#Report_Application_Link_Configuration)
- ### [Emailing Reports Configuration](#Emailing_Reports_Configuration)
- ### [Report Best Practices](#Report_Best_Practices)
- ### [Report Naming Conventions & Standards](#Report_Naming_Conventions_&_Standards)

---

## <a name="Report_Configuration"></a>Report Configuration

The information here describes the configuration options and requirements that you should be aware of when building a Nextworld report.

### Reports

In the **Reports** application, you must:

- Create a new report with a name, product family and module, and a data source table. All data items that are in this table become available in the Report Builder.

- If your data for the report must be processed in a logic block before the report can run, select the **Built Over Logic Block Data**? check box and specify the logic block used in the **Report Data Logic Block** field.

  - Learn more about report data that must be processed in a logic block in the FLATTENED TABLE REPORT CONFIGURATION topic.

- Save the new report and refresh the list to see the new report record.

- Open the report record and ensure the **Externally Defined** check box is not selected. If you try to use Report Builder to build or edit your report with the check box selected, you receive an error.

- Select the **Report Builder** form action to start creating a report template.

### Report Builder

In the Report Builder component, you must:

- Create a report template using the three configuration panels to arrange how you want the driver table data displayed.
- After you are satisfied with your report template, select the **Create Inputs Table** form action located within the **Actions** menu. The default inputs from the Report Builder along with any additional inputs you added appear in the Fields page of the table.
  - You can also create a report table manually through the Tables application. If you choose to create the report table manually, add all the data items listed in the Editor panel of the Report Builder as available input fields.
- After you save the table, navigate back to Report Builder and select the **Create Report Application** form action located within the **Actions** menu.

### Report application

Configure the report application where users can run reports. Use the inputs and available fields from the driver table to create filters for the users to narrow down their report parameters.

---

- [Top](#Back_To_Top)

---

## <a name="Flattened_Table_Report_Configuration"></a>Flattened Table Report Configuration

The information here describes the configuration options and requirements that you should be aware of when building a Nextworld report from data in a flat table.

Flat tables are used specifically for reports and are designed to contain a copy of all necessary data for that report. The data for the flat table is populated by a logic block that queries a series of tables, applies filters based on report parameters, and inserts the retrieved data into the flat table. After the logic block runs, you can create an application over the flat table to view and validate the data that you want to be in the flat table. After you validate, you can use the flat table as the data source table in a report.

Learn more in the REPORT NAMING CONVENTIONS AND STANDARDS topic to reference the naming conventions and standards when building flat reports.

### Tables

In the **Tables** application, you must create the following two tables:

1. Report table - The table where you can pass parameters, or inputs, to the execution logic block.

- Create a new table of type `Main`
- Add the following data items as input fields:
  - `ReportTitle`
  - `ReportVersion`
  - `ReportExecutionID`
- Add any additional data items that you want to act as field inputs for the logic block.

2. Flat table - The table that contains the copied data that can be used in a report.

- Create a new table of type `Main`.
- Use `FlatReportData` as the security group for the table. This security group restricts users so they can only access records created by them.
- Select the **Purge Active** check box and choose `Flat Report Data` in the **Data Purge Group** field. This feature purges older data that is no longer relevant from the table to accommodate the up-to-date data that may be continuously inserted into this table.
- Add the following data items as output fields:
  - `ReportExecutionID`
  - `ReportVersion`
- Add all data items that you want to be used as outputs within the Report Builder. The values of these fields are inserted through the logic block.

> ### If you build an application over the flat table, then it must only be used internally to validate that the logic block populates the flat table correctly. To ensure this, the application's **Product Family** should be `Playpen` and the **Product Module** should be `Personal`.

### Logic Blocks

In the **Logic Blocks** application, you must:

- Create a new logic block over the report table you created above and open the Logic Block Builder.
- Build the logic block according to your requirements.
- Insert records into the flat table you created.
  - Add `ReportExecutionId` and `ReportVersion` to every record inserted into the flat table.
  - Define outputs based on the logic you wrote above.

### Reports

In the **Reports** application, you must:

- Create a new report over the flat table you created above.
- Select the **Built Over Logic Block Data**? check box and specify the logic block you created above in the **Report Data Logic Block** field.
- Save the new report and refresh the list to see the new report record.
- Open the report record and ensure the **Externally Defined** check box is not selected. If you try to use Report Builder to build or edit your report with the check box selected, you receive an error.
  Select the **Report Builder** form action to start creating a report template.

### Report Builder

In the Report Builder component, you must:

- Create a report template using the three configuration panels to arrange how you want the driver table data displayed.
- After you are satisfied with your report template, select the **Create Inputs Table** form action located within the **Actions** menu. The default inputs from the Report Builder along with any additional inputs you added appear in the Fields page of the table.
  - You can also create a report table manually through the **Tables** application. If you choose to create the report table manually, add all the data items listed in the Editor panel of the Report Builder as available input fields.
- After you save the table, navigate back to Report Builder and select the **Create Report Application** form action located within the **Actions** menu.

### Report Application

Configure the report application where users can run reports. Use the inputs and available fields from the data source table to create filters for the users to narrow down their report parameters.

---

- [Top](#Back_To_Top)

---

## <a name="Report_Application_Link_Configuration"></a>Report Application Link Configuration

This information describes how to create an application link to a Report application.

If you would like an application link to run a report automatically then it must meet the following criteria. On the Actions page in the **Applications** application, you must:

- Add a new application link to the **Application Links** subtable.
- Name the application link and define the report application that the link should open to.
- Choose `Container` in the **Form** field.
- Choose `Container` as the **Destination Region** for all your data mappings.
- Add an additional field mapping into a value that doesn't exist in any report versions. For example, map a constant such as `NonExistentVersion` into one of your report inputs.

If you don't want your application link to run a report automatically, configure your data mappings to match an existing report version.

---

- [Top](#Back_To_Top)

---

## <a name="Emailing_Reports_Configuration"></a>Emailing Reports Configuration

The information here describes how to set up workflow emailing so that you can email reports from applications.

### Logic Blocks

In the **Logic Blocks** application, you must:

- Create a logic block over the table with workflow that you want to use to email a report.
- Open Logic Block Builder.
- Fetch the report table of the report you want to run.
- Insert the **Queue Report** action to the logic block.
  - Select the report application of the report you want to run.
  - Select a post-processing table, or your business data table. Without this, the report cannot be emailed.

### Approvals

In the **Approvals** application, you must:

- Create a `Notification` type record.
- Put {-ReportLink-} in the **Content** field.

### Workflow Definition

In the **Workflow Definition** application, you must:

- Open the workflow definition for the table that you built the logic block over above.
- Create a workflow detail with **Workflow Trigger** of type `Report Transition`.
- Select a **Workflow Condition** with a value of either `Report Success` or `Report Error`.
- Add the approval to the row or rows you setup with `Report Success`.
  - Select the `Send Notification` value for the **Action Type** field.
  - Put the name of your approval In the **Action Details** field.

---

- [Top](#Back_To_Top)

---

## <a name="Report_Best_Practices"></a>Report Best Practices

These best practices ensure that reports are configured consistently throughout Nextworld.

Do not leave the **No Data** section in Report Builder empty. If this section is empty, it is harder to distinguish if that section is empty because there is no data to retrieve or if there is an error. Select `Constant` in the **Type** field and enter `No Data` in the **Value** field. This establishes that when the report displays `No Data`, then no data exists to populate that section, and when then that section of the report is empty, there is most likely an error preventing data retrieval.

If you are building a report over a flat table, then configure the logic block that deposits data into the flat table as a `Background Task` in the **Logic Block Type** field. This ensures that the task does not time out if you are querying a large set of data.

---

- [Top](#Back_To_Top)

---

## <a name="Report_Naming_Conventions_&_Standards"></a>Report Naming Conventions & Standards

These naming standards ensure that reports across Nextworld follow the same conventions so that builders can easily identify and classify them.

Do not use the word `Report` in the report name because it is added on to the table and application names. Format the report objects according to the conventions listed below:

| Nextworld object   | Naming convention   | Example          |
| ------------------ | ------------------- | ---------------- |
| Report             | <Report name>       | SalesOrder       |
| Report table       | <Report name>Report | SalesOrderReport |
| Report application | <Report name>Report | SalesOrderReport |

> ### If you create the input table and report application through the **Actions** menu in Report Builder, the name of the report is automatically combined with `Report` when you follow the application links. If you create the input table and report manually, you must give it the name of the report and add `Report` after it.

### Flat tables

When you are building a report over a flat table, you must create some additional objects to the standard report building process that is mentioned above. Format the flat report objects according to the conventions listed below:

| Nextworld object | Naming convention          | Example                 |
| ---------------- | -------------------------- | ----------------------- |
| Flat table       | <Report name>Flat          | SalesOrderFlat          |
| Logic block      | <Flat table name>Execution | SalesOrderFlatExecution |

---

- [Top](#Back_To_Top)

---
