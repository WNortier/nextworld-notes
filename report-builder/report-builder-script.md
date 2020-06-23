# Report Builder Class

### Slide 1 - Welcome

---

### Slide 2 - Safe Harbor

---

### Slide 3 - Title

- Purpose of Class
  - You will learn
    - Most of What's essential to know
    - Some of what's good to know
    - little of what's nice to know but hoping that when you work thru your exercises you uncover alot of this
  - This class is geared toward an implementer/solution developer (not an end user)
    - It assumes you are somewhat familiar with Nextbot Platform
- Version 1 of Report Builder - is not an end-user ad-hoc query tool. Not a data analytics tool. Behind the scenes, it is be a metadata-creation tool. The skin on top is in its infancy but it is a very powerful tool.

### Objectives

By the end of the session you will be able to:

- Use the Report Builder interface
- Identify data required for report
- Design and create a simple report
- Launch a report from a menu
- Modify a version
- Create a more complex report using logic block to flatten data

### Slide 4

The Big Picture

Let's look at the big picture here.

- Data source - contains the data you want to report on
  - Single Table (T1) can be a direct data source to a report (ie..Payment terms)
- If you have any of the following as data sources, you will need to write a logic block to flatten the data first
  - Header/Detail
  - Multiple tables
  - Joins
  - Cubes

> #### NOTE: Joins and Cubes will be supported as data sources in 2020.2 (Loge)

- Define the Report (report definition, data source, logic block if using to flatten table)
- Design the Report (layout, inputs, filters, etc)
- Create Report Input Table (Default inputs plus user inputs to use as filters, etc)
- Create Report Application (application for user to interface with to submit report)
- Versions - users version of report/report app
- Report itself - pdf, web, etc

> #### NOTE: JDE speak for former JDE folks

- Report input table and report application = version overrides in JDE

> #### NOTE: If you write a logic block to flatten data, Report Input Table is the driver table for LB

So that is the big picture - We will come back to this slide often!

### Slide 5 - Simple Report Requirements

Let's first decide what we want on our simple report:

Just want a report that show supplier name, email, primary phone and primary address.
**Name** (composite data field)
**Primary email**
**Primary Phone**
**Primary Address**

How do we determine supplier?

**_contact role = supplier_**

That will be our filter. We will hard-code the filter for this report (within report builder) as opposed to letting the user input the contact type before they run the report

**Supplier Class** - lets group our suppliers by their Supplier class; We will also sort our report by Supplier Class
Let's also count the number of suppliers by class.

> ### NOTE: The focus of this follow along is really nailing down all the parts of the Big Picture. When you are in there this afternoon, you can play with all the little feature things.

---

### Slide 6

We will be focused on the yellow box part of our process "Define the Report"

---

### Create a Report (Go into the software)

1. Go to Menu, Then Reports
2. Click on Create Report button
3. Fill in the following Fields

**Report Name**

- By convention, the report name should not include the word "Report". (click on field level helps)
- Go into field-level helps
- Name-spaced
- Put your initial for now after name-space
- Camel Case
- Call your report nsTrnXXSupplierListing (where XX is your initial)

**Product Family** - Playpen (ie..Financials)

**Product Module** - Personal (ie..Receivables)

**Table**: Directory

- If we need to build a flat table, we would provide the name of the Flat table we create here

**Built Over Data Logic Block** - Don't check. going away

**Report Data Logic Block** - fill in the name of the logic block you create to flatten table. (in this case we do not have one - we are accessing the Directory directly)

**Save and Exit**

1. Find your report in the reports list, Double click.

1. This is going to bring you into the Report Definition record you just created

1. Talk about this "Report Definition"

- if you change the datasource or add your logic block you do it here

- notice check box "**externally defined**" - this means the report was not built in report builder **Externally Defined**: Whether this report is externally defined or developed solely through Nextworld. Externally defined reports are all existing reports that were not created using Nextworld's Report Builder. If this box is checked, the external version of the report will be executed. If it is unchecked, the Report Builder version will be executed, regardless of whether this record corresponds to an external report

- **Run in Nextworld**: Controls where the report will execute. True will execute on a Nextworld server, False will execute on a reporting server (**this is internal and will not be there in future - From Bruce:** not fully functional and will not stay around. We are re-doing how we run things behind the scenes and need that knob for now so we can test it out before we turn it on for everyone.)

- **Relative URI** - created cant be modified (product family, module, report name)

- **LB Input Processing Only** - this was a unique requirement from appdev for work orders. Show me all the w/o's today to next week. Timezone was a factor. Timezone manipulation not available in RB but is in LB. _This will be going away_

3. Add a **Description** - "Supplier Listing". That's all we have to do.

4. Save and Stay

---

### Slide 7

Next we move onto Report Builder where we will design the report, create the report input table, create and generate the report application, preview the report, and then create a version and run it. (the yellow box outlines what takes place from within report builder for creating the elements). The report application/versions can be hooked to menus for user to run the report.

---

### In the Software

1. Click the Report Builder Button

BTW - the Grant Table Access on the blue action buttion- you can ignore - going away

---

### In the Software

Inside the Report Builder 3 panels:

**Structure** - a list of all available report sections and a compilation of available data. The structure panel provides the outline of the report.

It lets you:

- Define data and inputs available in the report.

- Add, remove, or reorder items within sections of the report

The **Viewer** panel - a visual representation of the report.

The viewer panel provides a visual representation of the report; this is your canvas, where you place content which will be visible when the report is run.

In the viewer, you can select content items to move and resize them, as well as editing their properties.

The **Editor** panel - the properties of report sections and content.

The editor panel is for configuring properties on various parts of the report. Select a node in the structure, or a section / content item in the viewer to edit its properties.

### Button bar

The button bar lets you preview your report and toggle draft mode, as well as providing actions to create an report application and table, based on your report.

Let's hop back over to PPT and talk about the Structure panel

1. There are 9 sections - we will walk thru them

---

### Slide 8 & 9

Talk through each - the examples are pretty self-explanatory. You could look at Nextworld Helps for a description of each.

---

Watch Follow along video for the next section (_RB_follow_along1.mp4_)

---

1. Let's start at the top

2. Click on REPORT (in the structure Panel)

- let's see what we can modify
- Go to the Editor panel
- Change to landscape (first change from px to inches) and the flip the height and width

3. Click the green plus sign next to report title in the Viewer Panel

- change the "Type" in the editor to Constant
- Type Supplier Listing in the Value field in the editor panel - this adds a title to your report
- Drag the stretch bars to fit the constant (over in the viewer panel)
- Drag the Title to the center in the Viewer Panel

4. Add a system date
   - click the plus sign next to report title in the Viewer Panel
   - change the "Type" in the editor to System
   - change the "System" in the Editor panel to Current Date

- Show crosshairs and center

5. Page Header - top of page just like in word

6. Header (header of the report detail) - usually field labels/column headings

   - 1. click on Fields in the Structure Panel)
     - 1. name (field label) - underline
     - 2. primary phone (field label) - underline
     - 3. primary address (field label) - underline

7. Detail

   - 1. click on fields
     - 1. name (field value) - stretch column
     - 2. primary phone (field value)
     - 3. primary address (field value) - stretch and change stretch value. Maybe move section height.

8. Footer - think of footer as a column footer (subtotals for detail records)

9. Page footer - think of this kind of like a footer in MS word

10. Last Page Footer

11. Report Summary

12. No Data - exactly what it says on it. "No Data" is the standard here.

Take a look at the Viewer Panel

- click the down triangle next to Viewer to toggle viewer and see layout

Now click the Action Button - Save and Stay

---

### Slide 10 Preview - discuss the bullet points about Previewing a report

---

Watch Follow along video for the next section (_RB_follow_along2.mp4_)

---

Before you can Preview your report, you must create your report input table and your report application:

- Must first create report input table

  - Actions button
  - Create Input Table
  - show fields have report input fields
  - check product family and product module
  - Save and Exit - takes you to Report Builder

- Then must create application and generate

  - Create Report Application
  - associate above table
  - check product family and product module
  - show list form fields and detail form fields
  - save and stay
  - Generate

> ### NOTE: Only modifying the input table or modifying the report app itself will cause you to need to regenerate. If you change the report you do not have to.

- Go to jobs in a duplicate tab
- When successful - go to application tab and click cancel to return to report builder
- Show on The Big Picture where we are

- Then you can preview

  - click preview
  - associate the newly create application
  - Run!

- Looks good - except for one thing! Its the whole directory. We need to filter suppliers
- Draft - save with errors. For example if I change row height to 10000pixels and this is on, I can still save the report
- Go back to report

---

Watch Follow along video for the next section (_RB_follow_along3.mp4_)

---

### In the software

1. **Go to filters**

- 1. show expression
- 2. Add expression
- 3. role (contact role)
- 4. contains
- 5. specify value - supplier
- 6. Save

- 1. save and stay
- 2. Preview
- 3. "out of sync"
- 4. run again
- 5. Looks good - now lets let the user pass in their own report title

2. **Go to inputs**

- 1. look at inputs
- 2. drag report title to report title section
- 3. Aha..preview doesn't allow user inputs

- 4. so now we need to run this from the Report application
  - 1. action button
  - 2. Go to Report Application
  - 3. There are no versions yet
  - 4. create
  - 5. fill in inputs
  - 6. save and stay
  - 7. view report
  - 8. you have not run this report before
  - 9. Run, wait for green refresh or look in jobs
  - 10. close, save and exit, close...back to report builder

1. **Group By..**

- 1. let's say we want to group this by supplier classification
- 2. Add a group header section
  - 1. click on the properties of the section
  - 2. Set the group to supplierclassification
  - 3. Add a field to the group section (supplier classification)
  - 4. Add a formula/field/count on name in group footer and to report summary
  - 5. Add a Sort for SupplierClassification
  - 6. Go to Report Application
  - 7. Run, wait for green refresh or look in jobs
  - 8. close, save and exit, close...back to report builder

2. **Inputs and filters**

- 1.  there are some bugs here - composite data items seem not to be working for reason - I am testing that and have a bug entered. Suzie to find out if bug is fixed

- 2. For now, let's just say we want to give a user the chance to pick which supplier classification

- 3. Go to RB

  - 1. click on inputs
  - 2. Add input field - supplierclassification
  - 3. Save and Stay
  - 4. now its in RB but it is not in the Report Input table. We need to add it.

    - 1. actions
    - 2. edit report input table
    - 3. doubleclick
    - 4. fields
    - 5. add field
    - 6. supplierclassification
    - 7. save and exit
    - 8. close

  - 5. now its in my report table, how about our report app?

    - 1. Actions
    - 2. Edit Report Application
    - 3. Generate
    - 4. look at jobs
    - 5. cancel out
    - 6. close

  - 6. In RB, modify filter to include input field supplierclassification equal to input (add it to the filter expression that is already there for supplier)

  - 7. go to report application

    - 1. check your old version
    - 2. wa-la supplier classification is there
    - 3. select technology
    - 4. run the report - should get 4

  - 8. Test your output - Go to suppliers and contacts app - filter on supplier classification to make it technology. You should see the same 4.

---

### Slide 11

We have just been thru all this demonstrating how to launch a report from a report app

- this app is just like any other, you can edit it, apply app settings, add to a menu

---

### Notes

- you must run one preview before you can create a version
- it would appear that there are a couple of bugs in our environment (sort and filter of composite fields within Report Builder) but this is a great example of the processing difference. If we were using an LB to flatten data, the sorting and filtering logic would happen inside the logic block rather than inside the report builder.

---

### Slide 12 Exercise on your own - Your mission should you choose to accept it.

**Exercise 1 (handout)**

Fixed Asset Report

- assetid
- assetname
- netbookvalue
- fixedassetstatus

netbookvalue <= 0.00 (1)
groupby fixedassetstatus (2)
input fixedassetstatus (3)

---

### Slide 13 How to launch reports

---

### Slide 14-24

Now on to Logic Blocks

Flat tables This flow will remove the need for complex sql, as the same filters and result set can be achieved through running a logic block.

---

### Slide 25

**Exercise 2 (handout)**

---

### Slide 26 How to launch reports

20.1 Base Reports that have been converted to Report Builder

---

### Slide 27 How to launch reports

customizations

---

### Slide 28 How to launch reports

Modifying Delivered Base Reports

---

### Slide 29 How to launch reports

looking forward - Loge

---

### Slide 30 How to launch reports

Final Mission -

---

### Slide 31 How to launch reports

Rewrite the supplier activity report (no handout - just look at the current report delivered and try to rewrite using report builder)

---
