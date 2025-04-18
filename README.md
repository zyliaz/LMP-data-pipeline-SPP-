# LMP-data-pipeline-SPP
### **Project Overview:**  
This project aims to create a data pipeline that fetches LMP data from the SPP website, transforms it into a time-series format, merges it with geographical coordinates and solar output, and then generates a summary statistics table (CSV format) to provide insights for solar development. With geographical coordinates included, the summary table can be uploaded to an ArcGIS Online dashboard for visualization.

### **Python Scripts for Database Creation and Maintenance**  
Five Python scripts are used to create and maintain a database with any relational database service (AWS Cloud is used here). Please refer to the **"Database Management Flowchart.png"** for the first three scripts. 

1. **"[AmazonAWS] Data Extraction & Connection with Relational Database.ipynb"**  
   - This Jupyter Notebook extracts all 2024 data from the SPP URL (covering 1/1/2024 6:00 to 1/1/2025 5:00), converts it to time-series format, and uploads it as `raw_lmp` to the database.  
   - It also uploads the coordinates table and the solar output table.  
   - After this step, the database will contain:  
     - `raw_df`: Table with all 2024 LMP data  
     - `node_coords`: Table with geographical coordinates  
     - `solar_output`: Table with solar output data  
   - _(Note: Initial testing was conducted on this notebook, which includes merging coordinates and solar outputs as well as testing daytime and nighttime averages. These parts can be ignored if not needed.)_

2. **"(Monthly Update 1) New Rows to raw_lmp Table.ipynb"**  
   - This Jupyter Notebook can be run periodically to update the database.  
   - The raw data is transformed into a time-series format and appended as new rows to the `raw_lmp` table.  
   - _Note: SPP does not update the previous month's data until around the 9th of the following month. Therefore, this script should be run after the 9th to retrieve data for the prior month._

3. **"(Monthly Update 2) Summary Stats Tables.ipynb"**  
   - This Jupyter Notebook should be run monthly after the first update to refresh the summary statistics.  
   - It generates statistics based on the past year's solar energy pricing data and the general yearly solar output, including: projected annual revenue, average and solar-weighted LMP, daytime and nighttime average LMP, etc.   
   - The table is then merged with geographical location data and exported as a CSV file.

4. **"Monitor Database Data Tables"**  
   - This Jupyter Notebook is used to inspect the tables and features of the database.  
   - Functionality includes:  
     - Listing all table names  
     - Viewing the schema of a specific table  
     - Checking the first and last rows of a table  

5. **"Making Changes in AWS Database"**  
   - This Jupyter Notebook allows modifications to the database, including:  
     - Renaming tables  
     - Sorting data  
     - Dropping tables  

### **About the Data**  

1. **LMP Data (raw_lmp)**  
   - The original LMP dataset is fetched from a dynamically generated URL on the SPP website.  
   - Number of settlement locations: **1,233**  

2. **Geographical Coordinates (node_coords)**  
   - Coordinates are obtained from Nira and SPP.  
   - The `"SETTLEMENTLOCATION"` column in this dataset matches the `"Settlement Location Names"` column in the LMP table.  
   - Number of settlement locations: **487**  

3. **Solar Output Data (solar_output)**  
   - Data is sourced from PVWatts.  
   - The `"node_id"` column matches the `"Settlement Location Names"` column in the LMP table (**487** locations).  
   - The `"hour"` column contains hourly datetime values for one year; the year 1999 was chosen arbitrarily.  
