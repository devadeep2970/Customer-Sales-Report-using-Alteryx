📌 Project Overview
This Alteryx workflow automates the end-to-end processing of customer sales data — a task that would typically take hours of manual work in Excel. The workflow ingests raw data from two sources, cleans and transforms it, joins them together, and outputs a structured Excel report segmented by customer type — all in under an hour.

🎯 Objective
To automate customer sales reporting by:

Cleaning and filtering raw customer data
Aggregating transaction-level sales data per customer
Joining both datasets to enrich the output
Ranking top 10 customers by sales within each customer segment
Exporting the final report to Excel automatically


📂 Input Data Sources
FileFormatDescriptionCustomers.csvCSVCustomer master data including CustomerID, Store Number, Segment, Responder status, and contact detailsTransactions.xmlXMLTransaction-level data including Transaction ID, Customer ID, Product Name, Sales amount, and Order ID

🔧 Tools Used & Workflow Logic
Stream 1 — Customer Data Processing
StepToolAction1Input DataLoad Customers.csv2SelectRename CustomerID → Customer Number, cast to Int16, drop unnecessary fields (Address, City, State, Zip, Lat, Lon)3FilterKeep only non-responders — [Responder] = "NO"4Data CleanseClean First Name & Last Name — remove whitespace, fix title case, replace nulls with blanks
Stream 2 — Transaction Data Processing
StepToolAction1Input DataLoad Transactions.xml2SelectCast fields to correct types — Transaction (Int16), Customer_ID (Int16), Sales (Double), Order_ID (Int32)3SummarizeGroup by Customer_ID → Sum of Sales (Total Sales), Count of Order_ID (No Of Orders)
Final Processing — Joining & Output
StepToolAction1JoinJoin Stream 1 (Customer Number) with Stream 2 (Customer_ID) to enrich customer records with sales data2SortSort by Total Sales — Descending3SampleExtract Top 10 customers per Customer Segment4OutputExport to Customer Sales Report.xlsx, split into separate sheets by Customer Segment

📊 Output

File: Customer Sales Report.xlsx
Contents: Top 10 customers by Total Sales, segmented by Customer Segment
Fields: Customer Number, Store Number, Customer Segment, First Name, Last Name, Total Sales, No Of Orders


⚡ Key Outcome

Tasks that previously required hours of manual Excel work — data cleaning, aggregation, joining, filtering, and reporting — are fully automated and completed in under an hour using this workflow.


🛠️ Tech Stack

Tool: Alteryx Designer x64 v2025.2
Input Formats: CSV, XML
Output Format: Excel (.xlsx)


👤 Author
Nalam Devadeep
