# Lesson 05 Lab Instructions

## Exercise 1—Working with Data Sources and Destinations

In this lab you will create a package with three data flow tasks. You will configure each of these tasks to use a
 variety of data sources and data destinations. Note that there are many ways to accomplish the same task.

The **Solution** section provides a set of individual steps to accomplish the objectives listed here,
 and a variety of
 methods are demonstrated. You can use the methods that you prefer.

1. Create an SSIS project named Ch5LabEx1 in the **Studentfiles** folder. Rename the
 default package to **DataSourcesAndDestinations.dtsx**.
2. Add three Data Flow tasks to the Control Flow tab. Rename the Data Flow tasks to:
 **DF\_ProductsFFtoOLEDB**, **DF\_EmployeesSQLtoExcel**, and
 **DF\_SalesOrdersExceltoRecordset**.
3. Add a project connection manager to the AdventureWorks database.
4. Edit the DF\_ProductsFFtoOLEDB data flow task as follows:
    1. Add a flat file data source named **FF\_ProductsRed\_Source** pointing to **Chapter 05 Data Flow\Labs\Starters\RedProducts.csv**.
    2. Add an OLEDB destination named **OLE\_ProductsRed\_Destination**. Connect the data source to it.
     Configure the data destination to use the OLEDB connection manager you created earlier. In the destination
     properties,
     create a new table named **Ch5Products** and map the input columns to this new table.
5. Edit the DF\_EmployeesSQLtoExcel data flow transformation as follows:
    1. Add an OLE-DB source named **OLE\_Employees\_Source** that retrieves data from the AdventureWorks
     database using the query found at **Chapter 05 Data
     Flow\Labs\Starters\Employees.sql**.
    2. Add an Excel connection manager named **XL\_Employees** and a destination named
     **OLE\_Employees\_Destination**. The connection manager should point to a new Excel 2007 workbook
     in your
     **Studentfiles** folder named **EmployeeExport.xlsx**. The
     worksheet should
     be named **EmpExport**.
6. Add a package variable named **SalesDataset** with a data type of Object.
7. Edit the DF\_SalesOrdersExceltoRecordset dataflow as follows:
    1. Add an Excel Connection Manager named **XL\_SalesOrders** configured to point to the **Chapter 05 Data Flow\Labs\Starters\2011SalesOrders.xlsx** file.
    2. Add an Excel data source named **XL\_SalesOrders\_Source** configured to point to the first
     worksheet
     in the file accessed through the **XL\_SalesOrders** connection manager.
    3. Add a Recordset destination that stores the result set in the SalesDataset variable created earlier in this
     lab.
8. Save and close the project and solution that you created. Note the location you saved it in as you will be using
 it in future lab exercises.

The Project created in this lab will be used as the starter file for the Chapter 6 Lab. An answer key is provided
 in the event that you did not have time to complete this lab.