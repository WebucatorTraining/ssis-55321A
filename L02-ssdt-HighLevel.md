# Lesson 02 Lab Instructions

## Exercise 1: Import and run a package in SSDT-BI

The goal of this exercise is to practice adding an existing package to an Integration Services project in SQL
 Server
 Data Tools.

1. Create a new SSIS project named **Ch2LabEx1** stored in the **Studentfiles** folder. The project should be created in a new solution with the same name.
2. Delete the default **Package.dtsx** package.
3. Add the package located at **Chapter 02 SSDT\Labs\Starters\
 **EmployeeHistoryAppend.dtsx**** to the Ch2LabEx1 project.
4. Review the Control Flow and Data Flow tabs. Notice that the package is moving data from a csv file to the
 MyEmployeeHistory table.
 
    If you did not perform the lab in Chapter 1 or if your <code class="nocopy">MyEmployeeHistory</code> table was deleted,
    import and run the **ImportMyEmployeeHistory.dtsx** file in the
    **Chapter 02 SSDT\Labs\Starters** folder before running the
    **EmployeeHistoryAppend.dtsx** package.

5. Run the package and verify that it ran successfully. End debug mode to return to design mode.
6. Use SQL Server Management Studio to verify that the new rows were added to the dbo.MyEmployeeHistory table in
 the Adventureworks database.