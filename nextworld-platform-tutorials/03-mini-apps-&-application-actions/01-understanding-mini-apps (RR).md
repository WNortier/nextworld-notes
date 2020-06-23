---
<a name="Back_To_Top"></a> Top
---

- ### [1 UNDERSTANDING MINI APPS](#1_UNDERSTANDING_MINI_APPS)
- ### [2 BUILD A MINI APP](#2_BUILD_A_MINI_APP)

---

## <a name="1_UNDERSTANDING_MINI_APPS"></a>1 UNDERSTANDING MINI APPS

A mini app is an application that opens in a floating window over the current application, allowing you to perform some actions in the mini app without navigating away from what you're doing in the main application. Mini apps are often used with search fields to let you locate a record from another application.

Mini apps are usually built over the same table as a standard style application. This means that both applications display the same records. Changes made to records in the mini app are saved to the application table, and are visible in the standard application.

Often, you open mini apps from a search field using a search action.

> ### You can apply application settings to a mini app. For example, you can apply an application setting to a mini app so it opens with a default value in the filter. You could also apply an application setting to enter a default value when new records are created. Learn more in the **_APPLICATION SETTINGS_** topic.

[Understanding application settings -> application settings](https://github.com/WNortier/nextworld/blob/master/nextworld-platform-tutorials/01-build-an-application/03-understanding-applications.md#4_UNDERSTANDING_APPLICATION_SETTINGS)

---

- [Top](#Back_To_Top)

---

## <a name="2_BUILD_A_MINI_APP"></a>2 BUILD A MINI APP

In this section you'll build a mini app, NNCustomers. In the next section, you'll add your mini app as a search action to an application.

### Build Customers mini app

1. In Applications, create a new mini app with the following information:

![miniapps](../../images/mini-apps-&-app-actions/miniapps1.png)

2. Configure the following display options on the List Form Fields page:

![miniapps](../../images/mini-apps-&-app-actions/miniapps2.png)

3. On the Detail Form Fields page configure the layout with the following information:

![miniapps](../../images/mini-apps-&-app-actions/miniapps3.png)

4. On the Subtable Fields page, clear the Hide On Table field for the following fields:

- `EmailAddress`
- `EmailType`
- `PhoneNumber`
- `PhoneType`

5. Save and generate your application.

### Open mini app and create records

1. In **Application**, use the action menu to launch your mini app.

2. Create a new contact record, and then click **Save and Exit**.

---

- [Top](#Back_To_Top)

---
