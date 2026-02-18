/*
============================================================================
DDL Scripts: Create Bronze Tables
============================================================================
Script Purpose:
This scripts creates tables in the 'bronze'schema,dropping existing tables
if they already exist.
Run this script to re-define the DDL structure of 'bronze' Tables
===========================================================================
*/
/*
===========================================================================
Stored Purpose:
This stored procedure loads data into the 'bronze' schema from external csv files.
It performs the following actions:
-Truncates the bronze tables before loading data.
-Uses the 'BULK INSERT' command to load data from csv files to bronze tables.

Parameters:
  None.
  This stored procedure does not accept any parameters or return any values.
Usage Example:
  EXEC bronze.load_bronze;
===========================================================================
*/
CREATE OR ALTER PROCEDURE bronze.load_bronze AS
BEGIN
DECLARE @start_time DATETIME, @end_time DATETIME,@batch_start_time DATETIME,@batch_end_time DATETIME;
BEGIN TRY
SET @batch_start_time = GETDATE();
print '====================================================='
print 'Loading Bronze Layer'
print '====================================================='

print '-----------------------------------------------------'
print 'Loading CRM Tables'
print '-----------------------------------------------------'

set @start_time = GETDATE();--getdata return exact time
print'>> Truncating Table:bronze.crm_cust_info'
TRUNCATE TABLE bronze.crm_cust_info;
-- BULK is written to load all csv files into the bronze table
print'>> Inserting Data Into: bronze.crm_cust_info'
BULK INSERT bronze.crm_cust_info
FROM 'P:\sql_data_warehouse_project\datasets\source_crm\cust_info.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK-- when data is load into the table the 'tablock' lock the data in the table
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'second';
print '>>---------'

set @start_time = GETDATE();
print'>> Truncating Table:bronze.crm_prd_info'
TRUNCATE TABLE bronze.crm_prd_info;
print'>> Inserting Data Into:bronze.crm_prd_info '
BULK INSERT bronze.crm_prd_info
FROM 'P:\sql_data_warehouse_project\datasets\source_crm\prd_info.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'second';
print '>>---------'

set @start_time = GETDATE();
print'>> Truncating Table:bronze.crm_sales_details'
TRUNCATE TABLE bronze.crm_sales_details;
print'>> Inserting Data Into:bronze.crm_sales_details'
BULK INSERT bronze.crm_sales_details
FROM 'P:\sql_data_warehouse_project\datasets\source_crm\sales_details.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'second';
print '>>---------'

print '-----------------------------------------------------'
print 'Loading ERP Tables'
print '-----------------------------------------------------'

set @start_time = GETDATE();
print'>> Truncating Table:bronze.erp_cust_az12'
TRUNCATE TABLE bronze.erp_cust_az12;
print'>> Inserting Data Into:bronze.erp_cust_az12'
BULK INSERT bronze.erp_cust_az12
FROM 'P:\sql_data_warehouse_project\datasets\source_erp\cust_az12.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'second';
print '>>---------'

set @start_time = GETDATE();
print'>> Truncating Table:bronze.erp_loc_a101'
TRUNCATE TABLE bronze.erp_loc_a101;
print'>> Inserting Data Into:bronze.erp_loc_a101'
BULK INSERT bronze.erp_loc_a101
FROM 'P:\sql_data_warehouse_project\datasets\source_erp\loc_a101.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'second';
print '>>---------'

set @start_time = GETDATE();
print'>> Truncating Table:bronze.erp_px_cat_g1v2'
TRUNCATE TABLE bronze.erp_px_cat_g1v2;
print'>> Inserting Data Into:bronze.erp_px_cat_g1v2'
BULK INSERT bronze.erp_px_cat_g1v2
FROM 'P:\sql_data_warehouse_project\datasets\source_erp\px_cat_g1v2.csv'
WITH(
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	TABLOCK
);
set @end_time = GETDATE();
print '>> Load Duration:'+ cast(DATEDIFF(second, @start_time,@end_time) AS NVARCHAR) + 'secondS';
print '>>---------'

SET  @batch_end_time = GETDATE();
PRINT '============================================'
PRINT 'Loading Bronze Layer is Completed';
PRINT ' -Total Load Duration:' + CAST(DATEDIFF(second,@batch_start_time,@batch_end_time) AS NVARCHAR) + 'seconds';
PRINT '============================================'
END TRY
BEGIN CATCH
PRINT '======================================================'
PRINT 'ERROR OCCURED DURING LOADING BRONZE LAYER'
PRINT 'ERROR MESSAGE' + ERROR_MESSAGE();
PRINT 'ERROR MESSAGE' + CAST(ERROR_MESSAGE() AS NVARCHAR);
PRINT 'ERROR MESSAGE' + CAST(ERROR_STATE() AS NVARCHAR);
PRINT '======================================================'
END CATCH
END


