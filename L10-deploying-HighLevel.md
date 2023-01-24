# Lesson 10 Lab Instructions

## Exercise 1: Deploying a Project to the SSIS Catalog

The goal of this exercise is to review the process of deploying a project to a new folder on an existing SSIS
 catalog. In this exercise, you will also review the process of configuring environments and attaching an environment
 when executing a package. Answers may vary depending on how the directions are interpreted.

1. Create two new folders in the **Studentfiles** folder, one named **Chapter
 10Dev,** and another named **Chapter 10QA**.
2. If one does not already exist on your SQL Server instance, create the SSIS Catalog.
3. In SQL Server Management Studio, create a new folder named **Chapter 10Lab** in the SSIS
 Catalog.
4. Open the Visual Studio solution file located at **Chapter 10
 Deploying\Labs\Starters\Lab7\_Answer\Lab7.sln**.
5. Deploy the project to the Chapter 10Lab folder on your SSIS Catalog.
6. Verify that the project was successfully deployed.
7. In SQL Server Management Studio, create two environments in the Chapter 10Lab folder. Name them
 **Dev** and **QA**.
8. In both the Dev and QA environments, create three variables that will map to the
 **DestinationPath**,
 **Department**, and **ProjEmailToAddress** Project parameters.
9. In the **Dev** Environment set the **DestinationPath** to
 **C:\Classfiles\SSIS2016\Studentfiles\Chapter 10Dev**, set the
 **Department** to
 **Sales**, and the **ProjEmailToAddress** to
 **DevAdmin@adventure-works.com**.
10. In the **QA** Environment set the **DestinationPath** to
 **C:\Classfiles\SSIS2016\Studentfiles\Chapter 10QA**, set the
 **Department** to
 **Quality Assurance**, and the **ProjEmailToAddress** to
 **QAAdmin@adventure-works.com**.
11. Configure the Lab7 project to reference the Dev and QA environments.
12. Map the variables that you created in Step 8 to the project parameters in the **Lab5** project.
13. Execute the **DynamicPackage.dtsx** package, associate the execution with one of the
 environments.
 Verify that the email is addressed to the appropriate admin, and that the Excel file is in the proper location and
 for
 the proper department.
14. Clean up your work environment by closing any projects, queries, or Windows Explorer windows that you opened
 during this lab.

## Exercise 2: Manually executing a Package

Some organizations have standardized on processes other than the SQL Server Agent to automate database jobs. For
 these cases, and when you need to test a package outside of SSDT or SSMS, it is important to know how to use command
 line utilities to execute your packages. In this exercise, use dtexec to run the **DynamicPackage.dtsx**
 package located in the SSIS catalog.

1. Open a command prompt window.
2. Use the /? option to view the available help for dtexec.
3. Use Notepad to create a batch file named **mydtexec.bat** that will use dtexec to run
 the
 **DynamicPackage.dtsx** package from the SSIS catalog on your server. The package should
 use the
 variables defined in the **Dev** environment. Creating the batch file will make it easier for you to
 troubleshoot and make modifications to your code, along with giving you the ability to reuse it.
 
You will need to specify the location of the package, the server where the package is located,
 and the environment id.
4. Execute your batch file, and then verify the results using the messages in the command prompt window as well as
 the SSIS execution reports in SSMS.