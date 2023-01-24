# Lesson 09 Lab Instructions

## Exercise 1: Creating a Script Task to Merge Error Messages

1. Open **Chapter 09 Reliability\Labs\Starters\SimulateErrors\SimulateErrors.sln** in
 SSDT.
2. Create two package variables. One named **ErrorMessage** of type object and the other named
 **MailText** of type string. No default values need to be set. The **ErrorMessage**
 variable
 will hold an array.
3. Add an event handler at the package level that runs when an error occurs.
4. Add a Script Task to the event handler that you created. Configure the Script Task language to VB.Net. The
 Script
 Task will need to be passed the current system error description and the array of error messages. Set up the two
 variables that will be passed to the script. You will need to be able to change the ErrorMessage variable, but not
 the
 system error description variable.
5. Edit the script. Use a Try/Catch block to see if your array already exists. If it does, add the current error
 descriptions to the array. If not, initialize the array, and then concatenate any new messages. To cause the error
 messages to be on individual lines, add a hard return after each new message.
6. Create an event handler that will run after the final task has completed to send out an email message with the
 collected error messages. Remember, task error messages are propagated to the parent, so depending on where and
 how
 you create your script and mail tasks, you may receive multiple emails.
 
In addition to using an
 Event Handler, there are other ways to create a single email message with collected error messages included.
 Feel free
 to experiment.
7. Add a Script Task to write the contents of the error message array variable to the MailText variable, placing a
 hard return between each error message in the array when writing the error messages to the MailText variable.
8. Add a task to send an email message to your event handler after the Script Task completes. Set the To Line and
 From Line email addresses to **Admin@adventure-works.com**. Add a subject line of “Package Completed”,
 and
 a message body populated by your MailText variable.
9. Test your package.
10. Close your project and solution, but leave SSDT open for the next exercise.

## Exercise 2: Configure a package to use transactions

The goal of this exercise is to configure the tasks and containers in a package to participate in transactions. You
 will run the package simulating errors at different points in time to see the effects that transactions have on
 package
 execution when failures occur.

1. Open the **Chapter 09 Reliability\Labs\Starters\Restarting\Restarting.sln** file in
 SSDT.
2. Open the **TestTransaction.dtsx** package.
3. Enable and execute the Create DemoTransactions Table task. Disable the task again after executing it.
4. Review the package checkpoint properties. Notice that these options are not configured. You should avoid mixing
 transactions and checkpoints because the combination is not supported by Microsoft.
5. To allow your transactions sufficient time to rollback, configure the **Execute SQL Task
 *X***
 tasks so that they do **NOT** fail the package when they fail.
6. Modify the package properties so that a transaction is started when the package starts. Additionally, all tasks
 should join the transaction.
7. Add the forward slash back into the Execute SQL Task 10 SQL statement to cause a divide by zero error.
8. Execute the **TestTransactions.dtsx** package, notice that Execute SQL Task 10 failed,
 and then stop debugging.
9. Use SQL Server Management Studio to verify that no rows were added to the DemoTransactions table.
10. Configure the **Execute SQL 2 Task** so that it runs independently and in its own native SQL based
 transaction. It should insert its row even if the package transaction fails.
    1. Configure **Execute SQL Task 2** to not join the parent package’s transaction.
    2. Configure **Execute SQL Task 2** to begin a SQL native transaction with the SQL statement, and
     then
     commit the transaction at the end of the SQL Statement. This over simplification is to show how the concept
     functions.
     In an actual package, you might call a stored procedure from your server that uses a Try/Catch block and only
     commits
     the rows once one or more checks have been run on the data. Otherwise, it rolls the changes back.
11. Execute the TestTransaction package, and verify that everything except Execute SQL Task 10 succeeds, and then
 stop
 debugging.
12. Switch to SSMS and verify that Task 2 has a row in the DemoTransactions table. Close SSMS.
13. In SSDT, save and close your project.