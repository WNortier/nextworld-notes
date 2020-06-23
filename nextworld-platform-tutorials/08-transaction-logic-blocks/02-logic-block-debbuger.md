---
<a name="Back_To_Top"></a> Top
---

- ### [1 LOGIC BLOCK DEBUGGER](#1_LOGIC BLOCK DEBUGGER)
- ### [2 START A DEBUG SESSION](#2_START_A_DEBUG_SESSION)

---

## <a name="1_LOGIC BLOCK DEBUGGER"></a>1 LOGIC BLOCK DEBUGGER

Use the Logic Block Debugger when you're troubleshooting a problem with your logic block. For example, troubleshooting unexpected errors set by the logic block when it runs, or unexpected results produced by the logic block.

Access the Logic Block Debugger through the Logic Block Builder. You can only access the debugger when you have debug mode turned on in your user settings.

Use the Debugger for logic blocks that run because of an action in the UI. This includes table triggers and action blocks that run after a user clicks **Save**.

The Logic Block Debugger runs a logic block a single action at a time. In other words, the logic block debugger breaks down the process that occurs when a logic block runs so you can identify problems. Problems can include when:

- Your logic block isn't working as expected, and you don't know why. For example, if a condition isn't being met that you expect to be met.

- You want to know the value of something you can't see in the UI. For example, if you want to see a fetched value before it is passed into a logic block.

- You need to identify a problem and how to fix it. For example, if a field in your record is being set to a wrong value.

When debugging a logic block, you may find a variety of issues to fix. These issues can range from conditional actions being nested incorrectly, to incorrectly validated information being passed to the logic block, to looping issues in a fetch. Once you identify issues, you can open the logic block in the Logic Block Builder to fix them.

---

- [Top](#Back_To_Top)

---

## <a name="2_START_A_DEBUG_SESSION"></a>2 START A DEBUG SESSION

### Start a debug session

Use these steps when you need to troubleshoot your logic block using the debugger.

Start a debug session

1. On the Settings page of the user menu, turn on the **Debug Mode** toggle. The user menu is accessible from the main menu bar.

2. In **Logic Blocks**, open your logic block in the Logic Block Builder.

3. Select the **Debug Mode** check box, and then click **Save and Exit**.

4. Use the row action menu to generate your logic block.

### Use the debugger

1. In a new browser window or tab, launch your application in the same lifecycle as your logic block.

2. Select the action to troubleshoot using the **Debug** action button.

You must select an action before you can start the debug session.

3. Perform the action that runs the logic block.

For example, if your logic block is configured as a Field Value Changed event, then change the field value in the application that is associated with the event.

4. When your debug session begins, open your logic block in the Logic Block Builder, and then click the **Debug** button.

Your session should be automatically detected in the Flow Control panel on the left.

5. Use the controls in the Flow Control panel to go through your logic block.

6. After you finish your session, open your logic block in the logic block builder, clear the **Debug Mode** check box, and then click **Save and Exit**.

> ### Performance issues may occur if you don't clear the **Debug Mode** check box when you are done with your session.
