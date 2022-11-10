# Lesson 12 Lab Instructions

## Exercise 1: Securing the SSIS Catalog

In this exercise, you will test certain administrative functions such as deploying and executing packages to
 reinforce the concepts of what permissions are required to perform certain tasks.

The classroom setup should have created three Windows users named SSISadminUser, DeploymentUser, and ExecuteUser.
 If the users have not been created, use the Run as Administrator option to execute the batch file at
 **SSIS2016\Setup\AddUser.bat**. Verify that the three create user commands completed
 successfully, then press the “Any
 Key”.
 

Additionally, if you do not want to log out and back in to test the security settings, and the right-click Run as
 different user option is not available on your Start menu, and have Windows 10 or Pro, you can perform the tasks
 described at <https://www.ilovefreesoftware.com/15/windows-10/run-program-another-user-windows-10.html>
 to enable this functionality. If you have Windows 10 Home edition, or don’t want to make the changes, you can log
 out and back in to test the security settings configured in the lab.

1. Create SQL Server Logins for the SSISadminUser, DeploymentUser, and ExecuteUser accounts.
    1. Create the SSISadminUser Login based on Windows authentication of a Windows account with the same name.
    2. Set the default database to **SSISDB**.
    3. Add the login id to the SSISDB database as a user with the same name.
    4. Repeat this process for the DeploymentUser and ExecuteUser accounts.
2. Add the SSISadminUser to the SSIS\_Admin role.
3. Launch a new copy of SSMS using the right-click Run as different user option and launch the application as
 SSISAdminUser.
4. Run the **DynamicPackage.dtsx** package that you deployed in Chapter 10.
5. View the execution report for all executions. Notice that this user can see all executions, not just their own.
 The package execution probably failed. Review the messages to determine the cause of the error. You will not be
 fixing
 this particular error at this time, but an explanation exists in the **Solution** section detailed
 step 5. (2).
6. Close the SSISadminUser copy of SSMS and return to the copy of SSMS where you are logged on as
 administrator.
7. Modify the permissions on the Chapter 10Lab folder to include the DeploymentUser and ExecuteUser accounts.
 DeploymentUser should be able to deploy projects, but not execute the packages in the projects they deploy or in
 other
 projects. The ExecuteUser account should be able to execute packages, but not create environments, modify
 permissions,
 or deploy new projects.
8. The DeploymentUser should be able to redeploy the Lab7 project, but should NOT be able to modify environments or
 other projects already deployed in the Chapter 10Lab folder.
9. Test the permissions you assigned.
    1. DeploymentUser should be able to deploy projects, but not execute the packages in the projects they deploy
     or in
     other projects already deployed to the server. Additionally, they should not be able to modify any of the
     existing
     environments.
    2. The ExecuteUser account should be able to execute packages, but not create environments, modify permissions,
     or
     deploy new projects.
    3. As ExecuteUser, review the **All Executions** report from the Chapter 10Lab folder. Notice that
     ExecuteUser can only see executions associated with his account.
10. If time permits, create a different folder under SSISDB, and test to see if the DeploymentUser account can
 deploy
 a project to that folder.