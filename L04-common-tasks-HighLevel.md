# Lesson 04 Lab Instructions

## Exercise 1 – Create a package to copy a file and send an email message on completion

The goal of this exercise is to create a new project and then modify the default package to copy the
 **ProductsBlue.csv** file from the **Starters** folder to the
 **Studentfiles\Ch4LabEx1** folder. You will also configure a Send Mail Task to send an
 email notification if the file copy fails.
 

1. Create a new project in a new solution. Both the project and the solution should be named
 **Ch4LabEx1**. You should create a separate folder for the solution file. Save the files
 to the
 **Studentfiles** folder. Make note of the full path to your new project. Set your
 project
 TargetServerVersion to SQL Server 2016.
2. Rename the default **Package.dtsx** file to **CopyFile.dtsx**.
3. Add a `File System Task` item to the Control Flow and name it **Copy File**.
4. Set the following properties for the Copy File task.
    1. Set the **Operation** to **Copy file**.
    2. Set the **SourceConnection** to a new connection manager that points to the existing file **Chapter 04 Common Tasks\Labs\Starters\ ProductsBlue.csv**.
    3. Set the **DestinationConnection** to a new connection manager that points to the existing
     folder that
     you wrote down in step 1 above.
    4. Configure the destination so that a file can be copied multiple times and simply overwrite the existing file
     each
     time.
5. Execute just this new task to test it. Once the task has completed successfully, leave debug mode. If the task
 failed, double check your settings and execute the task again.
6. Add a `Send Mail Task` that will run only when the copy task fails. Configure the SMTP connection
 manager to point to localhost. Add a subject line and message source telling the recipient that the copy file task
 failed.
 
If you are using a corporate email server, the To and From addresses should both
 be your email address.
7. Execute the entire package. The Send Mail Task should not execute. Set the Copy File task to report a failure
 even
 when it succeeds, and then test the entire package again to verify that the package ran and the send mail task ran
 successfully.

## Exercise 2 – Create a package to perform data profiling and then review the results.

The goal of this exercise is to utilize the Data Profiling Task to explore the data contained in various tables
 from
 the AdventureWorksDW database. You will set up four profile requests. The first will allow you to determine if the
 ProductAlternateKey field contains unique values, and if not, what duplications exist. The second and third will
 allow
 you to look at the distribution of country codes in both the DimGeography and the FactResellerSales table to see if
 the
 actual sales are distributed in a similar way to the reseller locations. The fourth profile request will show you
 general statistics on the SalesAmount column for each line item.

1. Use SQL Server Management Studio to run the **Ch4\_CreateView.sql** script in the **Chapter 04
 Common Tasks\Labs\Starters\** folder. This will create a view that includes both reseller sales data and
 country
 codes.
2. Return to SSDT and the **Ch4LabEx1** project that you created in Exercise 1.
3. Add an ADO.NET project connection manager to the AdventureWorksDW database.
4. Create a new package named **Data Profiling** in the **Ch4LabEx1** project that you
 created in Exercise 1. If you did not complete exercise 1, you can use the solution located at **Chapter 04 Common Tasks\Labs\Answers\Ch4LabEx1**.
5. Add a `Data Profiling Task` to the control flow that uses a new file connection as the destination.
 If the task is run multiple times, the existing data should be overwritten. Configure four profile requests as
 described in the following steps.
6. Configure a **Candidate Key Profile Request** with the following settings:
    1. ConnectionManager – the **AdventureWorksDW** connection manager created in Step 2.
    2. TableOrView – **dbo.DimProduct**
    3. KeyColumns – **ProductAlternateKey**
    4. ThreshholdSetting – **None**
    
    If the threshold setting is set to Specified or Exact, data will
     only be returned to the report if the threshold is met or exceeded, depending on the setting. None will
     return all
     values and allow you to browse an unfamiliar data source.
7. Configure a Column Value Distribution Profile Request with the following settings:
    1. ConnectionManager – the AdventureWorksDW connection manager created in Step 2.
    2. TableOrView – dbo.DimGeography
    3. Column – CountryRegionCode
    4. ValueDistributionOption – AllValues
8. Configure a Column Value Distribution Profile Request with the following settings:
    1. ConnectionManager – the AdventureWorksDW connection manager created in Step 2.
    2. TableOrView – dbo.vResellerSalesWithCountry
    3. Column – CountryRegionCode
    4. ValueDistributionOption – AllValues
9. Configure a Column Statistics Profile Request with the following settings:
    1. ConnectionManager – the AdventureWorksDW connection manager created in Step 2.
    2. TableOrView – dbo.FactResellerSales
    3. Column – SalesAmount
10. Execute the DataProfiling project. Use the Profile Viewer in the Data Profiling Task Editor to review the
 information collected.

## Exercise 3 – Create a master package and test the execution flow of the child packages

The goal of this exercise is to configure a master package to emulate an ETL processing scenario. You will work
 with
 a project that includes all of the packages that you will need. You will then configure the master package to
 execute
 each of the three-dimension processing packages in parallel. Once the appropriate dimension tasks have successfully
 completed, the fact processing package should run. When both fact processing tasks have successfully completed, the
 cube
 processing package will run. Rather than actually processing data, for this simulation, a pop-up message box will
 appear
 telling you which package is running. Once you click `OK`, that package will complete successfully. This
 will allow you to
 test the control flow.

1. Use SQL Server Data Tools to open the **Chapter 04 Common
 Tasks\Labs\Starter\MasterPackage\MasterPackage.sln** solution file.
2. Add six Execute Package Tasks to the Control Flow of the **MasterPackage.dtsx**
 package.
3. Name, arrange, and edits the tasks and precedence constraints to meet the following goals.
    1. Tasks should be named to reflect the package that they are executing.
    2. The three dimension processing projects should be executed first, and in parallel.
    3. The **Execute FactProcess 1** task should only run after both the **Execute
     DimensionProcess
     1** and the **Execute DimensionProcess 2** tasks have successfully completed.
    4. The **Execute FactProcess 2** task should only run after both the **Execute
     DimensionProcess
     2** and the **Execute DimensionProcess 3** tasks have successfully completed.
    5. The **Execute CubeProcess** task should only run after both fact processing tasks have
     completed
     successfully.
4. Execute **MasterPackage.dtsx** in Debug mode. Notice that each of the packages opens
 when it starts
 running. Review the pop-up dialog boxes from the individual packages. Click `OK` on one message at a
 time,
 and review how this affects the task completions on the Control Flow tab of the **MasterPackage.dtsx**
 designer. When completed, exit Debug mode.
5. Execute the package again, and click `OK` on the task messages in a different order and review how
 the process
 changed. When completed, exit Debug mode.
6. Configure the **Execute FactProcess 1** task to report a failure even when it succeeds. Run the
 **MasterPackage.dtsx** package again and review the tasks as the package runs. click
 `OK` on the messages
 that appear. When completed, review the final state of the tasks in the **MasterPackage.dtsx** package,
 and then exit Debug mode.