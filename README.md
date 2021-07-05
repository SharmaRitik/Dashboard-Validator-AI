# Dashboard-Validator-AI
Power BI Visuals Underlying Data Validation Against Backend SQL DataBase Using AI 
Dashboard Validator AI Documentation

Introduction:

This is a power bi dashboard validation tool to validate BI report widgets/kpi’s with the L5 database for required number of slicer values, given the SQL queries as the source of truth.

Requirements:
powerbiclient
sql_metadata
psycopg2
pandas, numpy etc.

Important Prerequisite:
1. If the slicers in the report are single check type please convert them to multiple correct types of slicers first. You can do it by duplicating the report and making every slicer as multiple correct time in Power BI Service itself

2. Wait for sometime for the report to load and render inside notebook and then move ahead
.

Input Guide:
User Inputs: BI credentials, SQL query in particular format, Slicer Information.

Input Guide Description:
SQL query format: 
Input a .xlsx file with column name same as the title of the widget and the report while the alias of the measurement should be same as what given in its DAX query. E.g. Select count(empi) as Attributed Lives … Note: in this query Attributed Lives is same as there in the DAX query for Attributed Lives.
It is better to have the name of a measurement same in the DAX as well as the report, it makes our code run smoothly.
Note: the .xlsx file must have the same number of sheets as the number of pages in the report and each sheet will be named the same as the name of the page in BI report. Each sheet would contain the queries for widgets on that page.
The order of columns in the queries must be the same as the order of the columns in the report. Again column name should be the same it was in the DAX query.
Always pass subquery in a proper sub-query format e.g. { select xyz/(select * from ... as t) from .... }
Always write where conditions in this format:
select xyz from pqr where col1 = {0} and col2 = {1} and col3 = {2}....
The where conditions in subquery and main-query should be identical/same/identical e.g. select xyz/(select * from ... where col1 = {0} and col2 = {1} and col3 = {2}.... as t) from col1 = {0} and col2 = {1} and col3 = {2}....
Power BI Credential Input Guide:
Format of config.json:
{ "username": "xyz.pqr@innovaccer.com", "password": "password_here", "group_id": "dd5cfa79-4e23-4cc4-95e6-1666178f530c", "report_id": "8da7b124-51ec-47ef-a5dc-4aed69978839" }

Slicer input information:
Input a .xlsx file with column names same as the column name in the database and the values of the column will be the slicer values on which the dashboard is needed to be validated.
Title of the slicer should be the same as the column name in the database e.g. the slicer name should be changed from “Month” to “month_of_year” because the column name in the date table is “month_of_year”.

Note: Any spelling mistake and the mismatching due to wrong inputs may lead to an error so crosscheck the input files twice.

Challenges:
Installing the requirements in different environments.
Proxy settings to be unchecked if “unable to reach a domain” error occurs.
Whitelisting of these domains may be required:
1.https://api.powerbi.com
2.https://analysis.windows.net/powerbi/api/.default
3.https://analysis.windows.net/powerbi/api/Dataset.ReadWrite.All
4.https://analysis.windows.net/powerbi/api/Content.Create
5.https://analysis.windows.net/powerbi/api/Workspace.ReadWrite.All
6.https://login.microsoftonline.com/your_tenant_name
7.https://login.microsoftonline.com/organizations
8.https://github.com/Microsoft/powerbi-jupyter/issues
9.https://github.com/Microsoft/powerbi-jupyter
10.https://unpkg.com
11.https://microsoft.com
Enable powerbiclient notebook extension if the report is not loading inside it



Demo “queries.xlsx” →
https://docs.google.com/spreadsheets/d/1xRCesNWDgRwT8y_g3kTG9oDkTcEXJpntBK3oWVSXnag/edit?usp=sharing

Demo “slicers.xlsx” →
https://docs.google.com/spreadsheets/d/1qqnT8sSVZ_ImykrvjuiN4DztrXFZ6Qp8K2xLfv7W338/edit?usp=sharing



For an in-depth understanding of how this tool works inside please check out the report.





