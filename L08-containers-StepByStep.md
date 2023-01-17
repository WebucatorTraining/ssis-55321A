# Lesson 08 Lab Instructions

## Exercise 1 – Answer Key

Please note, there are several ways to accomplish the same task in SSIS. The book uses a variety of methods to
 expose
 you to different options. Feel free to use your favorite method throughout the exercises.

The goal of this exercise is to create a package with a Foreach Loop container that will read a list of email
 addresses and birthdays from the ThisMonthBirthdays view in the AdventureWorksDW database, and then send a custom
 email
 message to each email address.

1. Use SQL Server Management Studio to execute the **Chapter 08
 Containers\Labs\Starters\Ch8\_CreateView.sql** script.
    1. Open SQL Server Management Studio.
    2. Click the Open File icon (![open file icon](Images/ssis-open-file-icon.png))
     in the toolbar.
    3. In the Open File dialog box, browse to **Chapter 08 Containers\Labs\Starters\**,
     and
     then select the **Ch8\_CreateView.sql** file, and then click <code class="nocopy">Open</code>.
    4. Click the <code class="nocopy">Execute</code> button (![ssis open file icon](Images/ssis-execute.png)) or
     press <code class="nocopy">F5</code> to run the query to create the ThisMonthBirthdays view that will be used in this lab.
2. Create a new SSIS project and solution named **Ch8Lab** in the **Studentfiles** folder.
    1. Open SQL Server Data Tools.
    2. On the File menu, click **New | Project**.
    3. Select Integration Services Project as the template type, enter **Ch8Lab** in the Name field.
     Browse
     to the **Studentfiles** folder and save the project.
3. Rename the default package to **BirthdayEmails.dtsx**
    1. In Solution Explorer, in the SSIS Packages folder, right-click the **Package.dtsx** package, and
     then click <code class="nocopy">Rename</code>.
    2. Type **BirthdayEmails.dtsx**, and then press <code class="nocopy">Enter</code> to save the change.
4. Add the following variables to the package scope. Define the variable properties based on their function.
    1. The EmailToAddress variable will be used to hold the email address after it is retrieved from the database,
     and
     then passed to the send mail task.
        1. If necessary, open the Variables window by right-clicking the design surface, and then selecting
         Variables.
        2. On the Variables window toolbar, click the Add Variable icon.
        3. Enter or verify the following settings:
            * Name: EmailToAddress
            * Scope: Package
            * Data type: String
            * Value: DefaultEmail@AdventureWorks.com
    2. The Name variable should hold the person’s name returned from the birthday table.
        1. Use the <code class="nocopy">Add Variable</code> button to add a variable with the following settings:
            * Name: Name
            * Scope: Package
            * Data type: String
            * Value: Default Name
    3. The EmailSource variable will be dynamically set to contain a message that personalizes the Happy Birthday
     message by concatenating in the person’s name.
        1. Use the <code class="nocopy">Add Variable</code> button to add a variable with the following settings:
            * Name: EmailSource
            * Scope: Package
            * Data type: String
            * Value: Happy Birthday
        2. Click the ellipsis (<code class="nocopy">…</code>) to the right of the Expression column to open the Expression
         Builder.
        3. In the Expression Builder, use a combination of typing and dragging items from the Variables and
         Parameters and
         Function areas to create the following expression:
         "Happy Birthday " + @[User::Name]
        4. Click <code class="nocopy">Evaluate Expression</code> to verify that the results look correct.
    4. The ResultSet variable will hold the list of names and email addresses being returned from the
     ThisMonthBirthdays
     view.
        1. Use the <code class="nocopy">Add Variable</code> button to add a variable with the following settings:
            * Name: ResultSet
            * Scope: Package
            * Data type: Object
5. Add a **Data Flow Task** and a **Foreach Loop Container** to the **BirthdayEmails.dtsx**
 package.
    1. Drag a **Data Flow Task** from the SSIS Toolbox to the Control Flow design surface.
    2. Drag a **Foreach Loop Container** from the SSIS Toolbox to the Control Flow design surface.
6. Configure the **Foreach Loop Container** to execute only after successful execution of the
 **Data Flow Task**.
    1. Use the green precedence constraint arrow to connect the **Data Flow Task** to the
     **Foreach
     Loop Container**.
7. Configure the **Data Flow Task** to use a query to retrieve the full name and email address of each
 prospective buyer from the **ThisMonthBirthdays** view. Concatenate the first and last names to
 create a
 single column with the full name.
    1. Switch to the **Data Flow** tab.
    2. Drag an **OLE DB Source** from the Other Sources section of the SSIS Toolbox to the design
     surface.
    3. Right-click the **OLE DB Source**, and click <code class="nocopy">Edit</code>.
    4. On the Connection Manager page, click <code class="nocopy">New</code> to configure a new OLE DB connection manager.
    5. In the Configure OLE DB Connection Manager window, select the **LocalHost.AdventureWorksDW** in
     the Data connections area if available.
        * If it is not available, click <code class="nocopy">New</code>.
        * In the Connection Manager window, enter a period (.) for in the Server name field, and then select
         **AdventureworksDW** from the Select or enter a database name drop-down list, and then click
         <code class="nocopy">OK</code>.
    6. Click <code class="nocopy">OK</code> to close the Configure OLE DB Connection Manager dialog box.
    7. In the OLE DB Source Editor, select **SQL command** in the Data access mode dialog box.
    8. Write your own query to retrieve the full name and email address, or click the <code class="nocopy">Browse</code> button to
     browse and open
     the **Ch8\_RetrieveData.sql** query located at **Chapter 08
     Containers\Labs\Starters\**.
    9. Change to the **Columns** page of the OLE DB Source Editor.
    10. Verify that both columns are selected, and then click <code class="nocopy">OK</code>.
8. Configure a Recordset Destination to place the results of your query into the ResultSet variable that you
 created
 earlier.
    1. Add a **Recordset Destination** to the Data Flow design surface.
    2. Connect the blue data pipeline arrow from the **OLE DB Source** to the **Recordset
     Destination**.
    3. Right-click the **Recordset Destination**, and then click <code class="nocopy">Edit</code>.
    4. In the Advanced Editor for Recordset Destination dialog box, on the Component Properties tab, select
     **User::ResultSet** in the VariableName drop-down list.
    5. Change to the **Input Columns** tab.
    6. Select the check box next to **Name**, which should select both the **FullName**
     and
     **EmailAddress** columns.
    7. Switch to the **Input and Output Properties** tab.
    8. Expand the **Recordset Destination Input** and **Input Columns** folders and
     verify
     that both the **FullName** and **EmailAddress** columns are listed.
    9. Return to the **Input Columns** tab and verify that the warning about having no input columns
     has
     disappeared.
    10. Click <code class="nocopy">OK</code> to close the Advanced Editor for Recordset Destination dialog box.
9. Configure the **Foreach Loop Container** to use a **Foreach ADO Enumerator** to read
 all of the rows in your first table of the **RecordSet** variable that you configured. Map your
 **Name** and **EmailToAddress** variables to the columns being returned in the
 **RecordSet** variable.
    1. Return to the **Control Flow** tab.
    2. Right-click the **Foreach Loop Container**, and then click <code class="nocopy">Edit</code>.
    3. In the Foreach Loop Editor, change to the **Collection** page.
    4. In the Foreach Loop Editor section of the Collection page, select Foreach ADO Enumerator from the Enumerator
     drop-down list.
    5. Select the User::ResultSet variable in the ADO object source variable drop-down list.
    6. Verify that **Rows in the first table** is selected in the Enumeration mode section.
    7. Change to the **Variable Mappings** page.
    8. Select the **User::Name** variable in the first row, under the Variable column.
    9. Select the **User::EmailToAddress** in the first column of the second row.
    
     
    If your query
     selects first the email address, then the full name, you must change the Index values. The array is 0
     based, so the
     index number 0 refers to the first column in the array and the number 1 refers to the second column.
    10. Click <code class="nocopy">OK</code> to close the Foreach Loop Editor.
10. Add a **Send Mail Task** to the Foreach Loop Container.
    1. Configure the SMTPConnection to the SMTP connection information for the class.
        1. Drag a **Send Mail Task** from the Common section of the SSIS Toolbox to the bottom section
         of the
         **Foreach Loop Container**.
        2. Right-click the **Send Mail Task**, and then click <code class="nocopy">Edit</code>.
        3. In the Send Mail Task Editor, switch to the **Mail** page.
        4. In the SMTPConnection drop-down, click **&lt;New connection…&gt;**.
        5. In the SMTP Connection Manager Editor, type the name of your SMTP server, or localhost if using a local
         SMTP
         server configured for the class.
        6. If necessary, configure any of the other properties as provided to you by your IT department.
        7. Click <code class="nocopy">OK</code> to close the SMTP Connection Manager Editor.
    2. Configure the email message to come from **Sales@AdventureWorks.com**. Set the
     Subject to “Happy
     Birthday!”
        1. On the Mail page of the Send Mail Task Editor, set the **From** field to
         **Sales@AdventureWorks.com**.
        2. Set the **Subject** field to **Happy Birthday!**
        3. Verify that the **MessageSourceType** is set to **Direct Input**.
    3. Configure the Send Mail Task to use expressions for the To line and the MessageSource line. Configure the To
     line
     to point to the **EmailToAddress** variable. Set the email message to be the value set by the
     **EmailSource** variable.
        1. In the Send Mail Task Editor, change to the **Expressions** page.
        2. Click in the Expressions text box, and then click the ellipsis (<code class="nocopy">…</code>) button.
        3. In the Property drop-down list on the first line, select **ToLine.**
        4. Use the ellipsis button (…) to set the Expression to the **User::EmailToAddress** variable.
         Use the
         <code class="nocopy">Validate Expression</code> button to verify that your default email address is displayed.
        5. In the **Property** drop-down list on the second line, select
         **MessageSource**.
        6. Use the ellipsis button (…) in the second row to set the Expression to the
         **User::EmailSource**
         variable. Use the <code class="nocopy">Evaluate Expression</code> button to verify that your default message is
         displayed.
        7. Click <code class="nocopy">OK</code> three times to close both the Expression Builder, Property Expressions Editor, and
         the Send
         Mail Task Editor.
    4. Change the **Send Mail Task** properties to delay validation.
        1. In the Properties window for the Send Mail Task, in the Execution section, change the DelayValidation
         property to
         **True**. The red circle with an x (![Red X](Images/ssis-red-x.png)) should disappear from the Send Mail Task.
11. Execute the package. If all tasks succeed, leave debug mode. Verify that the email messages were sent.
12. Close the **BirthdayEmails.dtsx** package designer.
13. Save your project.