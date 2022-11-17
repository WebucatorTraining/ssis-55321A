# Lesson 05 Lab Instructions

## Exercise 1: Answer Key

In this lab you will create a package with three data flow tasks. You will configure each of these tasks to use a
 variety of data sources and data destinations. Note that there are many ways to accomplish the same task. The step
 by
 step directions use both the Source and Destination Assistants for some but not all of the steps to demonstrate some
 of
 the options available. Feel free to use the method that you prefer.

1. Create an SSIS project named Ch5LabEx1 in the **Studentfiles** folder. Rename the
 default package to **DataSourcesAndDestinations.dtsx**.
    1. Select **Start > All Programs > Microsoft SQL Server >SQL Server Data Tools**
    2. Select **File > New > Project**.
    3. In the New Project window, expand **Templates > Business Intelligence > Integration
     Services**. Select **Integration Services Project**. Change the Name to
     **Ch5LabEx1**.
     Browse to change the location to **C:\Classfiles\SSIS2016\Studentfiles\**. Check the
     **Create
     directory for solution** check box, and then click <code class="nocopy">OK</code>.
    4. In the Solution Explorer, expand SSIS Packages (if necessary), right-click **Package.dtsx** and
     select **Rename**. Rename the package
     **DataSourcesAndDestinations.dtsx**.
2. Add three Data Flow tasks to the Control Flow tab. Rename the Data Flow tasks to:
 **DF\_ProductsFFtoOLEDB**, **DF\_EmployeesSQLtoExcel**, and
 **DF\_SalesOrdersExceltoRecordset**.
    1. Drag three Data Flow Tasks from the SSIS Toolbox to the Control Flow. Rename the task as indicated above by
     right-clicking each task and selecting **Rename**.
3. Add a project connection manager to the AdventureWorks database.
    1. In Solution Explorer, right-click <code class="nocopy">Connection Managers</code> and select **New Connection
     Manager**.
    2. In the Add SSIS Connection Manager, select **OLEDB** and click <code class="nocopy">Add</code>.
    3. In the Configure OLE DB Connection Manager, click <code class="nocopy">New</code>.
    4. In the Connection Manager, type a period (.) for the Server name. In the Connect to a database section,
     click the
     **Select or enter a database name** option and choose **AdventureWorks** from the
     list. Click
     <code class="nocopy">OK</code>.
    5. Click <code class="nocopy">OK</code> to close the Configure OLE DB Connection Manager.
4. Edit the DF\_ProductsFFtoOLEDB data flow task as follows:
    1. Add a flat file data source named **FF\_ProductsRed\_Source** pointing to **Chapter 05 Data Flow\Labs\Starters\RedProducts.csv**.
        1. On the Control Flow tab, select the **DF\_ProductsFFtoOLEDB** task and then switch to the
         **Data Flow** tab.
        2. In the SSIS Toolbox, expand **Favorites** if necessary and drag **Source
         Assistant** to
         the Design area.
        3. In the Source Assistant – Add New Source window, set Select source type to **Flat File**.
         In the
         Select connection managers area, double-click <code class="nocopy">New</code>.
        4. In the Flat File Connection Manager Editor on the General page, click <code class="nocopy">Browse</code> and navigate
         to **Chapter 05 Data Flow\Labs\Starters\ProductsRed.csv**, and then click
         <code class="nocopy">Open</code>. You may
         have to change the file type to **CSV files (\*.csv)** using the list in the lower right-hand
         corner in
         order to see the file.
        5. In the Flat File Connection Manager Editor, set the properties as follows:
            * Format: Delimited
            * Text qualifier: “ (double-quote)
            * Header row delimiter: {CR}{LF}
            * Header rows to skip: 0
            * Column names in the first data row: Checked
        6. Note the warning “![Warning](Images/ssis-warning-icon.png "Warning")Columns are not defined for this connection manager” at the bottom of the window.
         Switch to
         the Columns page. The editor will assign the column names using the header row from the flat file. Click
         <code class="nocopy">OK</code>.
        7. Right-click the Flat File Source and select **Rename**. Rename the source
         **FF\_ProductsRed\_Source**.
    2. Add an OLEDB destination named **OLE\_ProductsRed\_Destination**. Connect the data source to it.
     Configure the data destination to use the OLEDB connection manager you created earlier. In the destination
     properties,
     create a new table named **Ch5Products** and map the input columns to this new table.
        1. In the SSIS Toolbox, drag **OLE DB Destination** from the Other Destinations group
         to the Design area.
        2. In the design area, select the **FF\_ProductsRed\_Source** and drag the blue arrow to the
         **OLE
         DB Destination**.
        3. Double-click the **OLE DB Destination**. In the OLE DB Destination Editor, verify that the
         project
         Localhost.AdventureWorks connection manager is selected in the drop-down list.
        4. 
        5. Click <code class="nocopy">New</code> next to the **Name of the table or the view** list.
        6. In the Create Table window, change the table name from **[OLE DB Destination]** to
         **[Ch5Products]**. Then, click <code class="nocopy">OK</code>.
        7. In the OLE DB Destination Editor, switch to the **Mappings** page. The editor will
         automatically map
         the input columns to the destination columns. Click <code class="nocopy">OK</code>.
        8. Right-click the OLE DB Destination and select **Rename**. Rename the source
         **OLE\_ProductsRed\_Destination**.
        9. Right-click the design surface and select Execute task. Green check marks should appear in the corners
         of each
         box to indicate success. A red “X” icon will appear if there is an error. You need to click <code class="nocopy">Stop Debugging</code>
         to return to design mode and resolve the error before continuing.
5. Edit the DF\_EmployeesSQLtoExcel data flow transformation as follows:
    1. Add an OLE-DB source named **OLE\_Employees\_Source** that retrieves data from the AdventureWorks
     database using the query found at **Chapter 05 Data
     Flow\Labs\Starters\Employees.sql**.
        1. On the Data Flow tab, change to the **DF\_EmployeesSQLtoExcel** task using the **Data
         Flow
         Task** drop-down list.
        2. In the SSIS Toolbox, drag **OLE DB Source** from the **Other Sources** group
         to the
         Design area.
        3. Right-click the **OLE DB Source** and select **Rename**. Rename the source
         **OLE\_Employees\_Source**.
        4. Double-click the **newly renamed OLE\_Employees\_Source**. In the OLE DB Source Editor on the
         Connection Manager page, verify that the project **LocalHost.AdventureWorks** connection
         manager is
         selected, and then set Data access mode to **SQL command** using the list.
        5. Click <code class="nocopy">Browse</code> and navigate to: **Chapter 05 Data
         Flow\Labs\Starters\Employees.sql**, and then click <code class="nocopy">Open</code>.
        6. Click <code class="nocopy">OK</code> to dismiss the OLE DB Source Editor.
    2. Add an Excel connection manager named **XL\_Employees** and a destination named
     **OLE\_Employees\_Destination**. The connection manager should point to a new Excel 2007 workbook
     in your
     **Studentfiles** folder named **EmployeeExport.xlsx**. The
     worksheet should
     be named **EmpExport**.
        1. In the SSIS Toolbox, drag **Destination Assistant** to the Design area.
        2. In the Destination Assistant – Add New Destination window, set Select destination type to
         **Excel**.
         In the Select connection managers area, double-click **New.**
        3. In the Excel Connection Manager, click <code class="nocopy">Browse</code> and navigate to your **Studentfiles** folder.
         Enter **EmployeeExport.xlsx** as the File name and then click
         <code class="nocopy">Open</code>.
        4. Verify that the Excel version is set to **Microsoft Excel 2007-2010** and that the First
         row has
         column names box is checked, and then click <code class="nocopy">OK</code>.
        5. Click the **OLE\_Employees\_Source** and drag the blue arrow to the **Excel
         Destination**.
        6. Double-click the **Excel Destination**. In the Excel Destination Editor on the Connection
         manager
         page, click <code class="nocopy">New</code> next to Name of the Excel sheet. A warning message indicating that there is
         not sufficient
         information appears. Click <code class="nocopy">OK</code> to dismiss it. In the Create Table window, change the table
         name from <code class="nocopy">Excel Destination</code> to <code class="nocopy">EmpExport</code>, and then click <code class="nocopy">OK</code>.
         
        The single quotes that appear in this window are actually “accent grave” characters. Type them
         using the key next to the numeral 1 that is shared with tilde (~).
        7. An information box appears that asks you to select the Excel sheet. Dismiss it by clicking
         <code class="nocopy">OK</code>. Use
         the drop-down list to select the **EmpExport$** sheet.
        8. Change to the **Mappings** page. The editor automatically maps the input columns to the
         destination
         columns. Click <code class="nocopy">OK</code>.
        9. Right-click the **Excel Destination** and select **Rename**. Rename the
         destination
         **XL\_Employees\_Destination**.
        10. In the Connection Managers area, right-click the **Excel Connection Manager** and select
         **Rename**. Rename the connection manager **XL\_Employees**.
        11. Right-click the design surface and select Execute task. Green check marks should appear in the corners
         of each
         box to indicate success. Click <code class="nocopy">Stop Debugging</code> to return to design mode.
6. Add a package variable named **SalesDataset** with a data type of Object.
    1. Right-click in an empty area of the data flow designer, and then click <code class="nocopy">Variables</code>.
    2. In the Variables pane, click <code class="nocopy">Add Variable</code> . Name the variable **SalesDataset** and
     set
     the Data type to **Object** using the drop-down list.
7. Edit the DF\_SalesOrdersExceltoRecordset dataflow as follows:
    1. Add an Excel Connection Manager named **XL\_SalesOrders** configured to point to the
     **Chapter 05 Data Flow\Labs\Starters\2011SalesOrders.xlsx** file.
        1. On the Data Flow tab, change to the **DF\_SalesOrderExceltoRecordset** task using the
         **Data
         Flow Task** drop-down list.
        2. Right-click in the Connection Managers area at the bottom of the Design screen, and then select
         **New
         Connection**.
        3. In the Add SSIS Connection Manager dialog box, select **EXCEL** and then click
         <code class="nocopy">Add</code>.
        4. In the Excel Connection Manager, click <code class="nocopy">Browse</code> next to the Excel file path and navigate to
         **Chapter 05 Data Flow\Labs\Starters\2011SalesOrders.xlsx**, and then click
         <code class="nocopy">Open</code>.
         Verify that the Excel version is set to **Microsoft Excel 2007-2010** and that the First row
         has column
         names checkbox is checked. Click <code class="nocopy">OK</code> to close the dialog box.
        5. Right-click the Excel Connection Manager, and select Rename. Rename the connection manager
         **XL\_SalesOrders**.
    2. Add an Excel data source named **XL\_SalesOrders\_Source** configured to point to the first
     worksheet
     in the file accessed through the **XL\_SalesOrders** connection manager.
        1. In the SSIS Toolbox, drag **Source Assistant** to the Design area.
        2. In the Source Assistant – Add New Source window, set Select source type to **Excel**. In
         the Select
         connection managers area, click <code class="nocopy">XL\_SalesOrders</code>, and then click <code class="nocopy">OK</code>.
        3. Double-click the **Excel Source** and verify that the Connection manager is set to
         **XL\_SalesOrders**. Set the Name of the Excel sheet to **Sheet1$** using the
         list. Change to
         the Columns page and review the mappings, and then click <code class="nocopy">OK</code>.
        4. Right-click the **Excel Source** and select **Rename**. Rename the source
         **XL\_SalesOrders\_Source**.
    3. Add a Recordset destination that stores the result set in the SalesDataset variable created earlier in this
     lab.
        1. In the SSIS Toolbox, expand **Other Destinations** and drag **Recordset
         Destination**
         to the design area.
        2. Click the **XL\_SalesOrders\_Source** and drag the blue arrow to the **Recordset
         Destination**.
        3. Double-click the **Recordset Destination**. In the Advanced Editor for Recordset
         Destination on the
         **Component Properties** tab, change Name to **RS\_SalesOrders\_Destination**.
         Click the list
         for VariableName and select **User::SalesDataset**.
        4. On the **Input Columns** tab, check the top box to select all of the input columns, and
         then click
         <code class="nocopy">OK</code>.
         
        You will learn how to use this recordset in a later chapter.
        5. Right-click the design surface and select Execute task. Green check marks should appear in the corners
         of each
         box to indicate success. Click <code class="nocopy">Stop Debugging</code> to return to design mode.
8. Save and close the project and solution that you created. Note the location you saved it in as you will be using
 it in future lab exercises.