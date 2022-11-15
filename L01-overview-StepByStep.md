# Lesson 01 Lab Instructions

## Exercise 1: Answer Key

Please note, there are several ways to accomplish the same task in SSIS. The book uses a variety of methods to
 expose you to different options. Feel free to use your favorite method throughout the exercises.

The goal of this exercise is to use the Import/Export Wizard to import data from a flat file into a new table in
 the **AdventureWorks** database. A completed package can be found at: **\Chapter
 01\Labs\Answers\ImportMyEmployeeHistory.dtsx**.

1. Use SQL Server Management Studio to launch the Import Wizard from the **AdventureWorks**
 database.
    1. Start **SQL Server Management Studio**. In the Connect to Server dialog box, verify that:
        * Server type is set to **Database Engine**,
        * Server name is set to **(local)**,
        * Authentication is set to **Windows Authentication**.
         **Note:** If your configuration varies from the default classroom configuration, enter the
         appropriate server name and credentials.
    2. Click <code class="nocopy">Connect</code>.
    3. Expand <code class="nocopy">Databases</code>, right-click <code class="nocopy">AdventureWorks</code>, and then select `Tasks >
     Import Data`. The SQL Server Import and Export Wizard opens.
2. Use the wizard to load the **Chapter 01 Overview\Labs\Starters\EmployeeHistory.csv**
 file into a
 new table named **[dbo].[MyEmployeeHistory]** in the
 **AdventureWorks** database. The file is a comma-delimited flat file with column names in the first
 row.
    1. If the Welcome page appears, check the **Do not show this starting page again** checkbox, and
     then click <code class="nocopy">Next</code>.
    2. On the **Choose a Data Source** page, set the Data source to **Flat File
     Source**.
    3. To configure the File name, click <code class="nocopy">Browse</code> and navigate to the
     **Chapter 01 Overview\Labs\Starters\EmployeeHistory.csv**
    **Note:** You have to change the file type to
     **CSV files (\*.csv)** in order to see the file.
    4. Click <code class="nocopy">Open</code>.
    5. On the **Choose a Data Source** page, verify that:
        * Format is set to **Delimited**,
        * Text qualifier is set to **<none>**,
        * Header row delimiter is set to **{CR}{LF}**,
        * Header rows to skip is set to **0**,
        * Column names in the first data row is checked.
    6. Note that there is a warning at the bottom of the window that says “Columns are not defined for this
     connection manager”.
    7. Click <code class="nocopy">Next</code>. Since the column names have not been defined, the wizard takes us to the column
     page of the **Choose a Data Source** window. Review the options, and then click
     <code class="nocopy">Next</code>.
    8. On the Choose a Destination page, set Destination to **SQL Server Native Client 11.0** using
     the list. Verify that:
        * Server name is set to **(local)**,
        * Authentication is set to **Use Windows Authentication**,
        * Database is set to **AdventureWorks**.
         **Note:** If your configuration varies from the default classroom configuration, enter the
         appropriate server name and credentials.
    9. Click <code class="nocopy">Next</code>.
    10. On the Select Source Tables and Views page, click **[dbo].[EmployeeHistory]** in the
     **Destination** column and change it to
     **[dbo].[MyEmployeeHistory]**.
    11. Click <code class="nocopy">Next</code>.
    12. On the Save and Run Package page, verify the following settings:
        * Run immediately is checked,
        * Save SSIS Package is checked,
        * The **File system** option is selected,
        * Package protection level is set to **Encrypt sensitive data with user key**.
    13. Click <code class="nocopy">Next</code>.
3. Save the package as **ImportMyEmployeeHistory** in the default directory. Note the location of
 the file.
    1. On the Save SSIS Package page, set Name to **ImportMyEmployeeHistory**, and then click
     <code class="nocopy">Next</code>. Make a note of the location of the file.
    2. On the **Complete the Wizard** page, review the steps that will be performed, notice that you
     can click the
     <code class="nocopy">Back</code> button to fix anything that wasn’t configured correctly, and then click
     <code class="nocopy">Finish</code>.
    3. On the **Complete the Wizard** page, review the information provided, and then click
     <code class="nocopy">Finish</code>.
4. Run the completed package and verify that the package was successful.
    1. The Wizard processes the package and reports “The execution was successful”. Note that the Message column
     next to the Copying to [dbo].[MyEmployeeHistory] action contains a link that says “290 rows transferred”.
    2. Click <code class="nocopy">Close</code>.
5. Use SQL Server Management Studio to verify that the **MyEmployeeHistory** table was created in
 the **Adventureworks** database.