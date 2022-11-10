# Lesson 06 Lab Instructions

## Exercise 1—Working with Derived Column Transformations

The goal of this exercise is to reinforce your ability to work with the derived column transformation to add a new
 column to the data flow pipeline. This new column will be derived by concatenating two of the existing columns.

1. Open the Ch05LabEx1 project (you can use the solution you created in chapter 5 or the **Ch05LabEx1.sln** file located
 in the **Chapter 06 Transform\Labs\Starters** folder. If necessary, open the
 **DataSourcesandDestinations.dtsx** package.
2. Modify the DF\_ProductsFFtoOLEDB data flow task to include a Derived Column transformation. The transformation
 should add a new column that concatenates the ProductNumber before the Name. Name the new column
 **ProdBusinessKey**. Use the Advanced Editor to change the ProdBusinessKey derived column to a string
 data type.
3. Use the **ModifyCh5Products.sql** file located in the **Chapter
 06
 Transform\Labs\Starters** folder to add a new column to the destination table. Modify the destination and
 map the
 new derived column from the data flow pipeline to the new column in your destination table.
4. Test just this dataflow and verify that the new column is populated in the Ch5Products table.

## Exercise 2—Working with Lookup Transformations

The goal of this exercise is to review the process of using a lookup transformation to retrieve data from a
 different
 source to use in the data pipeline.

1. Change the DF\_SalesOrdersExceltoRecordset data flow task to use a Conditional Split transformation to produce
 two
 outputs. Records with a SalesPersonID should go to an output named ResellerSales. The default output should be
 renamed
 to InternetSales.
2. The InternetSales output should go directly to the RecordSet destination. Rename this destination
 appropriately.
3. Use a Data viewer to verify that the records do not include a SalesPersonID.
4. Use the Advanced Editor to modify the XL\_SalesOrder\_Source so that SalesPersonID output column has a Data Type
 of
 **four-byte signed integer**.
5. Use a Lookup transformation to Add the SalesPerson’s name as a single column to the ResellerSales output.
 
You have to use the Person.Person table in the AdventureWorks database to locate the sales person’s name. The
 lookup
 should be performed by matching the SalesPersonID and the BusinessEntityID. The transformation should be set
 up so as
 not to fail even if a sales person’s name cannot be found.
6. Send the full Reseller Sales Output to a new flat file named **ResellerSalesOrders2011.csv**.
 Configure the output to append to the end of the file each time the component is run.
7. Test this dataflow and verify that the csv file has the correct information.