---
<a name="Back_To_Top"></a> Top
---

- ### [1 BUILD A TRANSACTION LOGIC BLOCK](#1_BUILD_A_TRANSACTION_LOGIC_BLOCK)
- ### [2 RetrieveGLMappingTypes LOGIC BLOCK](#2_RetrieveGLMappingTypes_LOGIC_BLOCK)
- ### [3 DeriveGLAccount LOGIC BLOCK](#3_DeriveGLAccount_LOGIC_BLOCK)
- ### [4 CHECKPOINT](#4_CHECKPOINT)

---

## <a name="1_BUILD_A_TRANSACTION_LOGIC_BLOCK"></a>1 BUILD A TRANSACTION LOGIC BLOCK

In this section, you'll read the context and requirements for a logic block for your **NNExpenseReport** application. Then you'll create a new logic block definition and configure the logic to meet the requirement of populating the GL account based on the expense classification. After your logic block is built, you'll add it to your **NNExpenseReport** application and then test your logic block.

### Logic block requirements

You need to build a logic block that finds the correct GL account for the expense classification entered in an application used to submit expense reports. In the Nextworld **Expense Report** application, the GL account associated with an expense is determined by the classification of the expense. This association is defined during implementation. This ensures that when employees submit expenses in an expense report, the expenses are charged to the correct account.

Logic blocks are built based on requirements. Here are the requirements for the logic block:

- Fetch the current `PayableTransactions` detail record.

- Check whether the **ExpenseClassification** field has a value.

- Check whether the **OrganizationalUnit** field has a value.

- If **ExpenseClassification** and **OrganizationalUnit** are not empty call the `RetrieveGLMappingTypeslogic` block.

  - Call the logic block when the user creates a new record.
  - Pass in the constant `Employee Expenses` to the **EntryType** field.

- If **ExpenseClassification** and **OrganizationalUnit** are not empty, also call the `DeriveGLAccountlogic` block.

  - Call the logic block when the user creates a new record.
  - Pass in the **ExpenseClassification** and **OrganizationalUnit** fields from the current detail row.
  - Pass in the **nwId** from the `RetrieveGLMappingTypes` logic block call to the `GLEntryType` field.

- Check if the **GLAccount** field is empty. If the field is not empty you don't want to override a user-entered value so you must check if it has a value.

- If the **GLAccount** field is empty, set the value of the **GLAccount** field with the value from the `DeriveGLAccount` logic block call.

- If the **ExpenseClassification** and **OrganizationalUnit** are empty do nothing.

Use the following actions:

- **Conditional**
- **Fetch Detail Records**
- **Call a Logic Block**
- **Set Values**

After the logic block is built and generated add the it to the **NNExpenseReport** application as a Field Value Changed event for the **OrganizationalUnit_Name** and the **ExpenseClassification** fields.

### Create a new logic block definition

1. Open the **Logic Blocks** application, and then click **Create**.

2. Enter the following information, and then click **Save and Exit**.

### Build a logic block

Use the `Logic Block Builder` to create a logic block that meets the requirements.

You can look at the `DefaultExpenseGLAccount` logic block to double-check your logic.

### Add your logic block to your application

Add your logic block to your **NNPayablesDetail** on the Actions page as a Field Value Changed event for the **OrganizationalUnit_Name** and the **ExpenseClassification** fields.

Generate your **NNPayablesDetail** and your **NNExpenseReport** applications.

### Test your logic block

1. Launch your application after it is generated.

2. Create a new expense report record and enter values in the header fields.

3. Use the **Add Expense Report Detail** button to add a detail record with any **Expense Classification**, an **Org Unit** of `NW Smart Solutions`, and leave the **GLAccount** field blank.

After you change the value of the **Expense Classification** field, your logic block runs and populates the **GLAccount** field.

> ### If your logic block does not run, you can use the Logic Block Debugger to troubleshoot it. You can learn more in the **_START A DEBUG SESSION_** topic.

[Table Lookups -> nwId](https://github.com/WNortier/nextworld/blob/master/nextworld-platform-tutorials/01-build-an-application/00-build-an-application-overview.md#3_TABLE_LOOKUPS)

---

- [Top](#Back_To_Top)

---

## <a name="2_RetrieveGLMappingTypes_LOGIC_BLOCK"></a>2 RetrieveGLMappingTypes LOGIC BLOCK

The `RetrieveGLMappingTypes` logic block uses a Fetch Records action to fetch records from the **GLMappingTypes** table, and then sets the **DrivingClass**, **LowestLevel**, and **nwId** fields.

The `RetrieveGLMappingTypes` logic block is called to find the GLMapping type for an entry type. If a record is found where the GLEntryType is the same, the values for the **DrivingClass**, **LowestLevel**, and **nwId** fields are set. If no records are found, an error message displays that says "GL Entry Type is not set up in GL Mapping Types. Choose a different GL Entry Type".

When the logic block is called by another logic block, the values for the **GLEntryType** and the **DrivingClass** fields are passed in. The logic block then passes back the **GLEntryType** nwId. This value is usually passed in when the `DeriveGLAccount` logic block is called.

---

- [Top](#Back_To_Top)

---

## <a name="3_DeriveGLAccount_LOGIC_BLOCK"></a>3 DeriveGLAccount LOGIC BLOCK

The DeriveGLAccount logic block is called by other logic blocks with the purpose of deriving any GL Account.

The DeriveGLAccount logic block uses a series of hierarchical queries to derive the GL Account for any of the following: entry type, organizational unit, ledger, or classification. The logic block uses the value, along with module settings, to derive a GL Account.

Other logic blocks call this logic block and then can use a Set Values action to use the GL Account that is derived.

When calling the DeriveGLAccount logic block, you are required to pass in **EntryType** and **OrganizationUnit**. You have the option of passing in **Ledger** and **Classification** as well.

The process of deriving a GL account is hierarchical. Based on the company structure, GL accounts can be different for different organizational units, but at least one rule must exist for the top company level.

The logic block performs the following hierarchy of queries to derive the GL Account:

- GLEntryType, Organizational Unit, Specific Class Type, Specific Ledger

- GLEntryType, Organizational Unit, Specific Class Type, Blank Ledger

- GLEntryType, Organizational Unit, Blank Class Type, Specific Ledger

- GLEntryType, Organizational Unit, Blank Class Type, Blank Ledger

The logic block checks to see if a rule exists for the organizational unit on the transaction. If no rule exists, the logic block continues to traverse up the company structure and check for a rule with each organizational unit in the structure until it reaches the top level company.

If no GL Account is derived with any of the organizational units in the company structure, the user will receive an error that says "The GL entry type does not exist."

This logic block uses the following actions:

- Fetch a table lookup

- Set message

- Retrieve Module Settings

- Call a Logic Block

- Conditional

- Traverse Tree

- Loop Conditional

- Set Values

---

- [Top](#Back_To_Top)

---

## <a name="4_CHECKPOINT"></a>4 CHECKPOINT

In this tutorial you built a logic block over the `PayableTransactions` table that populated the GL account based on the expense classification. You called the `DeriveGLAccount` and the `RetrieveGLMappingTypes` logic blocks in your logic block to determine the correct GL mapping type and GL account. You added your logic block to your **NNExpenseReport** application and configured it so it ran when the **Organization Unit** or the **Expense Classification** field value changed.

Be able to do the following:

- Read logic block requirements and build a logic block that meets them in an efficient way
- Pass field values to called logic blocks
- Pass values resulting from a called logic block to a called logic block
- Group actions using conditionals
- Efficiently fetch relevant records
