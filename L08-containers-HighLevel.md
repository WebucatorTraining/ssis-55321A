# Lesson 08 Lab Instructions

## Exercise 1 – Use a Foreach Loop container to send a custom email to the names found in a database view.

The goal of this exercise is to create a package with a Foreach Loop container that will read a list of email
 addresses and birthdays from the ThisMonthBirthdays view in the AdventureWorksDW database, and then send a custom
 email
 message to each email address.

1. Use SQL Server Management Studio to execute the **Chapter 08
 Containers\Labs\Starters\Ch8\_CreateView.sql** script.
2. Create a new SSIS project and solution named **Ch8Lab** in the **Studentfiles** folder.
3. Rename the default package to **BirthdayEmails.dtsx**
4. Add the following variables to the package scope. Define the variable properties based on their function.
    1. The EmailToAddress variable will be used to hold the email address after it is retrieved from the database,
     and
     then passed to the send mail task.
    2. The Name variable should hold the person’s name returned from the birthday table.
    3. The EmailSource variable will be dynamically set to contain a message that personalizes the Happy Birthday
     message
     by concatenating in the person’s name.
    4. The ResultSet variable will hold the list of names and email addresses being returned from the
     ThisMonthBirthdays
     view.
5. Add a **Data Flow Task** and a **Foreach Loop Container** to the **BirthdayEmails.dtsx**
 package.
6. Configure the **Foreach Loop Container** to execute only after successful execution of the
 **Data Flow Task**.
7. Configure the **Data Flow Task** to use a query to retrieve the full name and email address of each
 prospective buyer from the **ThisMonthBirthdays** view. Concatenate the first and last names to
 create a
 single column with the full name.
8. Configure a Recordset Destination to place the results of your query into the ResultSet variable that you
 created
 earlier.
9. Configure the **Foreach Loop Container** to use a **Foreach ADO Enumerator** to read
 all
 of the rows in your first table of the **RecordSet** variable that you configured. Map your
 **Name** and **EmailToAddress** variables to the columns being returned in the
 **RecordSet** variable.
10. Add a **Send Mail Task** to the Foreach Loop Container.
    1. Configure the SMTPConnection to the SMTP connection information for the class.
    2. Configure the email message to come from **Sales@AdventureWorks.com**. Set the
     Subject to “Happy
     Birthday!”
    3. Configure the Send Mail Task to use expressions for the To line and the MessageSource line. Configure the To
     line
     to point to the **EmailToAddress** variable. Set the email message to be the value set by the
     **EmailSource** variable.
    4. Change the **Send Mail Task** properties to delay validation.
11. Execute the package. If all tasks succeed, leave debug mode. Verify that the email messages were sent.
12. Close the **BirthdayEmails.dtsx** package designer.
13. Save your project.