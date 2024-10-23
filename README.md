# CDR Data Analysis Project

## Project Overview
This project utilizes Databricks to process and analyze Call Detail Records (CDRs) from a public S3 bucket. The goal is to extract meaningful insights regarding SMS, call, and internet activities over a specific time period.

## Dataset Information
The dataset comprises Call Detail Records (CDRs) located in WeCloudData's S3 bucket:

- **S3 Bucket Link:** `s3://weclouddata/datasets/telecom/CDR`
- **Data Structure:**
  - The data is organized into monthly subfolders, with each day containing a text file.
  - We focus on the `cdr_by_grid_december` folder and analyze the first five days of December.

### Column Definitions
The dataset contains the following columns, which do not include headers in the raw files:

1. **square-id**: ID of the square part of the Milano GRID (numeric)
2. **time-interval**: Beginning of the time interval (numeric, milliseconds since Unix Epoch)
3. **country-code**: Phone country code (numeric)
4. **sms-in-activity**: Received SMS count in the square during the time interval (numeric)
5. **sms-out-activity**: Sent SMS count in the square during the time interval (numeric)
6. **call-in-activity**: Received call count in the square during the time interval (numeric)
7. **call-out-activity**: Issued call count in the square during the time interval (numeric)
8. **internet-traffic-activity**: Internet traffic count in the square during the time interval (numeric)

## Project Goals
- Mount the CDR data from the S3 bucket to Databricks.
- Create a schema with appropriate headers.
- Perform various data transformations and analyses as outlined below.

## Tasks Completed
1. **Data Mounting**: Mounted the CDR data from the specified S3 subfolder.
2. **Data Cleaning**: Renamed columns by replacing `-` with `_`.
3. **Feature Engineering**:
   - Added a new column, `sms_ratio`, showing the ratio of `sms-in-activity` to `sms-out-activity`.
   - Created a date column from `time-interval` and formatted it as `yyyy/MM/dd`.
4. **Summary Statistics**: Calculated aggregated statistics at the `square-id` level, including means, minimums, and maximums for various activities.
5. **Min/Max Values**: Found minimum and maximum values for key activity metrics grouped by `square-id`.
6. **Aggregate Table**: Generated an activity summary table for SMS, calls, and internet activities by country and date. Wrote this DataFrame to the `tmp` folder in Parquet format.
7. **Data Export**: Mounted a personal AWS S3 bucket and exported the summary statistics to the S3 bucket.
8. **Ranking Internet Activity**: Used window functions to rank internet activity by country code and date.

## Instructions to Run the Notebook
1. **Prerequisites**: Ensure you have access to Databricks and the necessary AWS credentials.
2. **AWS Configuration**: Set up AWS credentials using the provided JSON file.
3. **Run the Notebook**: Execute the notebook cells in order to mount the data, process it, and generate the summary statistics.

## Future Work
- Extend the analysis to include more data months or other data sources.
- Implement visualizations to better illustrate trends and patterns in the CDR data.

## Acknowledgments
- Dataset sourced from WeCloudData.
- Special thanks to the Databricks community for ongoing support.

## License
This project is licensed under the MIT License. See the LICENSE file for details.
