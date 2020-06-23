# Advanced Logic Blocks

In this tutorial, you'll learn about table triggers and action blocks, which are different ways to use logic blocks. You'll also learn the specifics of the **Convert to Text**, **Concatenate Text**, and **Update Records** actions. You'll create a table and build an application using existing data items to capture transaction information. You'll receive specific requirements for a logic block, and then you'll build a logic block that combines field values to create and populate a link ID to meet the requirements. After you add your logic block as a table trigger, you'll test your logic block when you create a record.

This tutorial contains the following sections:

- Table triggers
- Action blocks
- Convert to text action
- Concatenate text action
- Update records action
- Build an advanced logic block
- Checkpoint

---

## <a name="Back_To_Top"></a> Top

---

- ### [1 TABLE TRIGGERS](#1_TABLE_TRIGGERS)
- ### [2 NEXTWORLD EXAMPLE PayableTransactionsPostTrigger LOGIC BLOCK](#2_NEXTWORLD_EXAMPLE_PayableTransactionsPostTrigger_LOGIC_BLOCK)

---

## <a name="1_TABLE_TRIGGERS"></a>1 TABLE TRIGGERS

Use a table trigger to run a logic block any time a record in a table is altered. Table triggers allow you to validate record data and update multiple tables.

Using table triggers provides a way to process data the same way, regardless of how the data is altered. Logic blocks configured as triggers on tables run after a record is altered. This is compared to logic blocks configured as an action in an application, which run before a user clicks save. For example, a logic block configured as a Field Value Changed event runs when a user changes a field value, or a logic block configured as a Row Entered event runs when a user clicks into a row.

You can use a table trigger when importing records to a table. For example, if you import records to the Directory, you could use a table trigger to add a contact role grouping to a record based on the contact role. Or, if you import records to an items application, you could use a table trigger to validate that the item class is acceptable for the item type in a record.

There are different types of triggers. Each type of trigger is comprised of a classification and a mode.

The prefix determines when the table trigger runs. The options are:

- 1. **Pre** — The table trigger runs before the change is saved to the table.

Use for data validation, defaulting values, or both.

- 2. **Post** — The table trigger runs after the change is saved to the table.

Use for data validation and to update associated tables with updated record information.

The mode is how the table is being altered. The modes are:

- **Insert** — The table trigger runs when a new record is created.

- **Update** — The table trigger runs when an existing record is changed.

- **Delete** — The table trigger runs when an existing record is removed.

For example, a Pre-Update table trigger runs the logic block before saving an altered record to the table. The `PayablesHeaderPreTrigger` logic block sets the **Payment Status** field in **SupplierInvoices** after the record is created or updated, but before the change is persisted to the table.

In contrast, a Post-Insert logic block runs after a change is persisted to the table, and is often used to update values in associated or secondary tables with values from the new record. The `UpdateSupplierInvoices` logic block updates the **Pending Payment** field in the header table when records are saved in the detail table. The `BankDepositsPostTrigger` logic block sets the value of the LinkID field with a value that is comprised of the `ContactID`, `TransactionType`, and `DepositTransactionNumber` values saved in the record.

> ### The **Transaction Scope** check box prevents the table records from being saved if an error occurs in the trigger logic block. This means that when an error occurs, the entire transaction is rolled back. By default, this check box is selected.

See the **_TABLE TRIGGERS BEST PRACTICES_** topic for best practices information.

---

- [Top](#Back_To_Top)

---

## <a name="2_NEXTWORLD_EXAMPLE_PayableTransactionsPostTrigger_LOGIC_BLOCK"></a>2 NEXTWORLD EXAMPLE PayableTransactionsPostTrigger LOGIC BLOCK

This is a helpful example of an advanced logic block because it creates a unique identification key, the LinkID, which is used by other logic blocks and several applications.

### Object overview

The `PayableTransactionsPostTrigger` logic block is used in the **ExpenseReport** application to concatenate record values into a Link ID, and then add that value to the record.

This logic block fetches the `Company` table lookup, which looks up on the `Directory` table.

### Configuration elements

This logic block is set up as a Post-Insert trigger, which means that it runs after a user clicks save. This means that after the user clicks save, the logic block runs. When the logic block runs, it creates the Link ID, and then updates the record with the value. Because **TransactionNumber** is an automatic number, the **LinkID** cannot be created until after the database creates the automatic number.

---

- [Top](#Back_To_Top)

---

![guidelines](../../images/advanced-logic-blocks/createtablelookups.png)

[Table Lookups -> nwId](https://github.com/WNortier/nextworld/blob/master/nextworld-platform-tutorials/01-build-an-application/00-build-an-application-overview.md#3_TABLE_LOOKUPS)
