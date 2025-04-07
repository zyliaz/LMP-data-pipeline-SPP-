# LMP-data-pipeline-SPP
This project aims to create a data pipeline that fetch LMP data from SPP website, transform into time series form, merge with geographical coordinate and solar output, then create summary statistics to draw insights for solar development. 
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
