---
<a name="Back_To_Top"></a> Top
---

- ### [1 ACTION BLOCKS](#1_ACTION_BLOCKS)
- ### [2 NEXTWORLD EXAMPLE WriteCashTransferGLRecord LOGIC BLOCK](#2_NEXTWORLD_EXAMPLE_WriteCashTransferGLRecord_LOGIC_BLOCK)
- ### [3 CONVERT TO TEXT ACTION](#3_CONVERT_TO_TEXT_ACTION)
- ### [4 CONCATENATE TEXT ACTION](#4_CONCATENATE_TEXT_ACTION)
- ### [5 UPDATE RECORDS ACTION](#5_UPDATE_RECORDS_ACTION)
- ### [6 BUILD AN ADVANCED LOGIC BLOCK](#6_BUILD_AN_ADVANCED_LOGIC_BLOCK)
- ### [7 CHECKPOINT](#7_CHECKPOINT)

---

## <a name="1_ACTION_BLOCKS"></a>1 ACTION BLOCKS

Action blocks are logic blocks that run instead of a save, update, or delete when a user clicks a button to save or delete a record. Action blocks contain logic actions to update the table they are configured for.

Action blocks give application developers full control of what happens when a user clicks a button that saves or deletes a record. In other words, instead of Nextworld automatically saving a record, you include actions in your logic block to manually save a record. For example, you could include an **Insert Records** or **Update Records** action.

Action blocks require specific user action to run. This means that action blocks do not run when data is imported to a table, or another logic block inserts records to the table. They do run when they are called by other logic blocks.

Action blocks act as a link between the data and the database. They take the information from the table they are called from, and then either connect that data with another table, or insert the data into the table that calls them. Other applications or integrations should call the action block to insert records into the table.

Use action blocks to write to transactional tables. That is, tables used to store transaction records like the `GeneralLedgerTransactions` table. If you expect records to be inserted into this table from multiple sources, you should use an action block to update the table. That is, if other processes use this table, it is important to use an action blocks to ensure the validity of the data. If a table is used for a setup application, configure your logic block as a table trigger instead because it is not updated by other processes.

Add actions blocks as part of the table configuration. They _take over_, or run instead of, the save in an application. This is compared to when Nextworld controls the save, and tables are updated automatically at the end of the logic block. Action blocks require specific configuration to manually save records. Taking over the save ensures that there is only one logic block that performs all validations and operations on the table. Taking over the delete ensures data integrity, making any necessary updates to other tables when a record is deleted.

Logic blocks are often configured as action blocks to:

- Ensure there is only one point from which records can be inserted into a table.
  - The action block could include actions that validate the information and an action to save the record.
- Write entered information from the application to another table when the application is used only for data entry.
  - The action block could include actions that call other logic blocks.

---

- [Top](#Back_To_Top)

---

## <a name="2_NEXTWORLD_EXAMPLE_WriteCashTransferGLRecord_LOGIC_BLOCK"></a>2 NEXTWORLD EXAMPLE WriteCashTransferGLRecord LOGIC BLOCK

The `WriteCashTransferGLRecord` logic block is a helpful example of an advanced logic block because the `WriteCashTransferGLRecord` logic block runs as an action block on the `CashTransfer` table and inserts a journal entry record with the values from the cash transfer and updates the associated bank accounts.

Object overview

The `WriteCashTransferGLRecord` logic block is used in the Financials family to write journal entries associated with cash transfers. Part of writing the journal entry record is to credit the bank account the transfer is to, and debit the account the transfer is from.

This logic block retrieves the General Accounting module settings. It also calls the `WriteGLTransaction` logic block, and fetches table lookups that look up to the `ChartOfAccounts`, `CashTransfer`, and the `FromBankAccountPointer` tables.

Configuration elements

This logic block is built over the `CashTransfer` table, which is of type Work Table. This logic block uses actions to create temp tables, retrieve module settings, set values, convert values to text, and insert records. This logic block also validates that a journal entry has not already been created for the cash transfer. This logic block creates a link ID using the values from the `TransactionType`, `TransactionNumber`, and `ContactID` fields.

---

- [Top](#Back_To_Top)

---

## <a name="3_CONVERT_TO_TEXT_ACTION"></a>3 CONVERT TO TEXT ACTION

The **Convert to Text** action allows you to convert field values, such as numbers, to text. Use the **Convert to Text** action to change the value of a non-text data item to text so that values can be compared to text values and manipulated.

For example, in an application used to enter bank deposits, you can use a **Convert To Text** action to convert the Deposit Transaction Number, which is a number, to text. You could then use another action to concatenate the transaction number and other information into a unique ID.

In the **From** section of the action, you can choose from different value types to convert to text including field values, system values, and variables.

In the **To** section of the action you can output converted values to different value types including:

- **Variable** — select a variable previously defined in the logic block.

- **New variable** — enter a name to define a new variable that can be used in subsequent actions.

- **Text field** — select a table, and then select a field.

> ### You have the option to select a data item to use as a format template using the **Format Template** field. When you select a data item in the **Format Template** field, the configurations defined on the Formatting & Validations page of the selected data item apply to the value converted to text. This includes formatting, validations, data precision, or maximum value.

---

- [Top](#Back_To_Top)

---

## <a name="4_CONCATENATE_TEXT_ACTION"></a>4 CONCATENATE TEXT ACTION

---

- [Top](#Back_To_Top)

---

## <a name="5_UPDATE_RECORDS_ACTION"></a>5 UPDATE RECORDS ACTION

---

- [Top](#Back_To_Top)

---

## <a name="6_BUILD_AN_ADVANCED_LOGIC_BLOCK"></a>6 BUILD AN ADVANCED LOGIC BLOCK

---

- [Top](#Back_To_Top)

---

## <a name="7_CHECKPOINT"></a>7 CHECKPOINT

In this tutorial you created a table and built and application over it using existing data items. Then you built a logic block over your table that concatenated field values to create a link ID. You added your logic block as a table trigger that runs after the save button is clicked, and then adds the link ID value to the record. After you generated your logic block and application you created a record to test your logic block.

Be able to do the following:

- Read logic block requirements and build a logic block that meets them
- Convert values to text to be concatenated
- Concatenate values and output them as a field value
- Update a table record with a logic block after the save button is clicked
- Configure a logic block as a table trigger

---

- [Top](#Back_To_Top)

---

![guidelines](../../images/advanced-logic-blocks/createtablelookups.png)

[Table Lookups -> nwId](https://github.com/WNortier/nextworld/blob/master/nextworld-platform-tutorials/01-build-an-application/00-build-an-application-overview.md#3_TABLE_LOOKUPS)
