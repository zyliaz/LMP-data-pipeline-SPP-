# LMP-data-pipeline-SPP
This project aims to create a data pipeline that fetch LMP data from SPP website, transform into timeseries format, merge with geographical coordinate and solar output, then create summary statistics to draw insights for solar development. 
There are 4 Python scripts that can be used to update and maintain the database with any relational database service (AWS cloud service is used here).  
  1. "[AmazonAWS] SPP data extraction & connection with relational database": this jupyter notebook can grab all the 2024 data from the SPP url (from 1/1/2024 6:00 to 1/1/2025 5:00), convert to the timeseries form (for 1233 nodes), merge with coordinates table (487 nodes), solar output table (487 nodes) and upload the final merged dataframe (44 nodes) to the database. The database should already have a dataframe called final_df with all 2024 data. 
  
  2. "Monthly Update (SPP LMP data)": this jupyter notebook can be run periodically to update data to the database. It follows similar steps as the 1st one, grabbing data from last month (SPP doesn't update the data from the previous month until the final days of the following month. So, we might need to run this script around the 27th or 28th of each month to retrieve the data from the prior month.), merge with coordinate and solar output table, then append the new data as new rows to the final_df in the database. 
  
  3. "Monitor database data tables": This jupyter notebook can monitor features of and tables in the database. Listing all table names, view schemas of a specific table, and check first and last few rows in a table. 
  
  4. "Making Changes in AWS Database": this  jupyter notebook can make changes to the database, including sorting and dropping a table. 

ABOUT THE DATA: 
  1. The LMP data is fetched from an engineered URL from the SPP website, which is then converted to a dataframe with columns:
      1. Datetime (date-time data type): Hourly from 1/1/24 6:00 to 1/1/25 5:00
      2. Settlement Location Name (string type): Total of 1233 Settlement Locations
      3. LMP (float type)
      4. MLC (float type)
      5. MCC (float type)
  2. The coordinate data.
      1. "SETTLEMENTLOCATION" column in the coordinate tableSettlement locations after this step is 487.
      2. 
  4. The solar output data is obtained from PVWatts with three columns:
      1. "node_id" column have the same values as the "Settlement Location Names" column in the LMP table.
      2. "hour"
      3. "output" is the estimated solar production for 
