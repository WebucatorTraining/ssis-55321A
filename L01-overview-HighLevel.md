# Lesson 01 Lab Instructions

## Exercise 1: Use the Import/Export Wizard from SSMS

The goal of this exercise is to use the Import/Export Wizard to import data from a flat file into a new table in
 the **AdventureWorks** database. A completed package can be found at: **\Chapter
 01\Labs\Answers\ImportMyEmployeeHistory.dtsx**.

1. Use SQL Server Management Studio to launch the Import Wizard from the **AdventureWorks**
 database.
2. Use the wizard to load the **Chapter 01 Overview\Labs\Starters\EmployeeHistory.csv**
 file into a new table named **[dbo].[MyEmployeeHistory]** in the **AdventureWorks**
 database. The file is a comma-delimited flat file with column names in the first row.
3. Save the package as **ImportMyEmployeeHistory** in the default directory. Note the location of the
 file.
4. Run the completed package and verify that the package was successful.
5. Use SQL Server Management Studio to verify that the **dbo.MyEmployeeHistory** table was created in
 the **Adventureworks** database.