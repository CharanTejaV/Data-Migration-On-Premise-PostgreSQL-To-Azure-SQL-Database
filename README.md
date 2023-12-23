# Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database
This project focuses on migrating an on-premise PostgreSQL database to Azure SQL Database using Azure Data Factory. The project seamlessly transfers tables, schemas, and views using Azure Data Lake Gen2 as a staging layer, leveraging the AdventureWorks open-source dataset for efficient migration.

# Project Overview
This project orchestrates the seamless transfer of data from an on-premise PostgreSQL database to Azure SQL Database, leveraging the capabilities of Azure Data Factory (ADF). The Adventure Works dataset serves as the data source, and despite its relatively big in size, the decision to utilize cloud services is driven by scalability, cost-efficiency, and the strategic advantages of cloud computing. The project design incorporates a carefully crafted architecture, with Azure Data Lake Gen2 functioning as a staging layer to replicate the existing schema and table hierarchy. This staging layer not only ensures structural integrity but also provides a flexible foundation for potential future transformations.

The step-by-step execution involves setting up the on-premise PostgreSQL server, configuring ADF with linked services and self-hosted integration runtime, and installing the necessary components for the migration. The use of dynamic parameterization, coupled with ADF's powerful functions like Get Metadata and Lookup, execute pipeline, facilitates an automated and scalable approach to schema and table retrieval. The introduction of a For Loop mechanism enhances the project's adaptability, allowing it to efficiently handle a diverse range of tables within the dataset. Finally, the implementation of triggers ensures a controlled and timely execution of the migration process, following thorough testing and evaluation. This project showcases the benefits of cloud-based data migration, even for smaller datasets, and the strategic use of Azure services to streamline the process while maintaining data integrity.

# Tools & Technologies
* Cloud - [Azure](https://azure.microsoft.com/en-us/free/search/?ef_id=_k_CjwKCAiA-P-rBhBEEiwAQEXhH2TmMccfTpk3ywwIKt4994lTYzscRnt3KKI0KDpwpeHu9OLhb7d8pBoCvckQAvD_BwE_k_&OCID=AIDcmm5edswduu_SEM__k_CjwKCAiA-P-rBhBEEiwAQEXhH2TmMccfTpk3ywwIKt4994lTYzscRnt3KKI0KDpwpeHu9OLhb7d8pBoCvckQAvD_BwE_k_&gad_source=1&gclid=CjwKCAiA-P-rBhBEEiwAQEXhH2TmMccfTpk3ywwIKt4994lTYzscRnt3KKI0KDpwpeHu9OLhb7d8pBoCvckQAvD_BwE)
* Data Storage - [Azure Data Lake Gen2](https://azure.microsoft.com/en-us/products/data-lake-analytics/?ef_id=_k_CjwKCAiA-P-rBhBEEiwAQEXhH0YMq88gk--X9G24_yjpUp_hhyBqgLcx8zHwAcGCaC_BykmHOied0RoCppkQAvD_BwE_k_&OCID=AIDcmm5edswduu_SEM__k_CjwKCAiA-P-rBhBEEiwAQEXhH0YMq88gk--X9G24_yjpUp_hhyBqgLcx8zHwAcGCaC_BykmHOied0RoCppkQAvD_BwE_k_&gad_source=1&gclid=CjwKCAiA-P-rBhBEEiwAQEXhH0YMq88gk--X9G24_yjpUp_hhyBqgLcx8zHwAcGCaC_BykmHOied0RoCppkQAvD_BwE)
* Data Orchestration - [Azure Data Factory](https://azure.microsoft.com/en-us/products/data-factory/?ef_id=_k_CjwKCAiA-P-rBhBEEiwAQEXhH24gZ1zmnilx1TrNMAgwpfVtz0jrCgfihBVkKLjaedrmGJGesKt9lxoCzoUQAvD_BwE_k_&OCID=AIDcmm5edswduu_SEM__k_CjwKCAiA-P-rBhBEEiwAQEXhH24gZ1zmnilx1TrNMAgwpfVtz0jrCgfihBVkKLjaedrmGJGesKt9lxoCzoUQAvD_BwE_k_&gad_source=1&gclid=CjwKCAiA-P-rBhBEEiwAQEXhH24gZ1zmnilx1TrNMAgwpfVtz0jrCgfihBVkKLjaedrmGJGesKt9lxoCzoUQAvD_BwE)
* Cloud Database - [Azure SQL Database](https://azure.microsoft.com/en-us/products/azure-sql/database/?ef_id=_k_CjwKCAiA-P-rBhBEEiwAQEXhH8HWOS7vMF4bASoTYCEvieKGnyW-NMo8mzkMuEn68gdl-_IiSQ3HHRoC4kUQAvD_BwE_k_&OCID=AIDcmm5edswduu_SEM__k_CjwKCAiA-P-rBhBEEiwAQEXhH8HWOS7vMF4bASoTYCEvieKGnyW-NMo8mzkMuEn68gdl-_IiSQ3HHRoC4kUQAvD_BwE_k_&gad_source=1&gclid=CjwKCAiA-P-rBhBEEiwAQEXhH8HWOS7vMF4bASoTYCEvieKGnyW-NMo8mzkMuEn68gdl-_IiSQ3HHRoC4kUQAvD_BwE)
* On-preimse Database - [PostgreSQL](https://www.postgresql.org/)
* Programming Language - [SQL](https://learn.microsoft.com/en-us/azure-data-studio/tutorial-sql-editor)

# Architecture

![Architecture](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/776dc862-60b8-429f-9864-eb089dac7000)

# Dataset used
The Microsoft Adventure Works PostgreSQL open-source dataset is a version of the popular Adventure Works database tailored for PostgreSQL environments. This dataset offers a comprehensive representation of a fictional company's operations, serving as an invaluable resource for testing and development purposes within PostgreSQL databases. To incorporate this dataset into the on-premise PostgreSQL environment, the process involved executing an Adventure Works OLTP install script. [Setup](https://github.com/lorint/AdventureWorks-for-Postgres/blob/master/README.md) , [Related Article](https://medium.com/@attila_toth/set-up-sample-database-for-postgresql-4c03b7502a7a)

[Data Source](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)

# Staging Layer and Hierarchy Replication
To maintain data integrity and structure, a staging layer in Azure Data Lake Gen2 is employed. This layer serves two key purposes:
  * **Hierarchy Replication**: Ensures the replication of the on-premise schema and table hierarchy in the final destination (Azure SQL DB).
  * **Transformations**: While the project scope did not necessitate transformations, the staging layer provides a foundation for incorporating transformations if future requirements emerge.

# Project Execution Highlights
  * **Dynamic Parameterization**: Utilized dynamic parameterization during data migration from ADLS Gen2 to Azure SQL DB, ensuring flexibility and adaptability.
  * **Metadata Retrieval**: Leveraged the power of Get Metadata and Lookup functions in ADF to dynamically retrieve schema and table information, allowing for an automated and scalable migration process.
  * **For Loop for Iteration**: Implemented a For Loop mechanism to automate the migration process, enabling the seamless handling of a large number of tables within the dataset.
  * **Execute Pipeline activity within a Pipeline**: The project incorporates the use of Execute Pipeline within a Pipeline, allowing for modular design and reusability. This is particularly valuable when dealing
    with a considerable number of tables, as it streamlines the execution process.
  * **Trigger Implementation**: Deployed triggers to automate the migration process after comprehensive testing and evaluation, ensuring a controlled and efficient data migration.

# Step-by-Step Workflow

## Step 1: Setting Up On-Premise PostgreSQL
  * Set up a local PostgreSQL server by installing PostgreSQL on-premise.
  * Import the Adventure Works database using the supplied OLTP installation script. Make sure that your on-premise device has Ruby and PostgreSQL libraries installed.

![AdventureWorksCLICode](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/aabe9e8e-4df6-4635-9ab2-0ae276bc05fb)

![AdventureWorksMetaData](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/b7a23cb0-a743-43c9-889d-1e6be3e4095c)

![image](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/14c6e70b-dff9-45fe-ad3c-d8b1d52da289)

## Step 2: Azure Data Factory, Storage and Database Setup
  * Open Azure Data Factory (ADF) and create linked services for on-premise PostgreSQL, Azure Data Lake Gen2 storage account and Azure SQL Database.
  * Set up a self-hosted integration runtime to establish a connection between ADF, PostgreSQL, and Azure Data Lake Gen2.

![All LinkedServices](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/7a31fd6d-bfb9-4d0c-b51a-1a65ce435c46)

## Step 3: Install Self-Hosted Integration Runtime
  * Download the Self-Hosted Integration Runtime from ADF
  * Download and install Oracle Java Runtime Environment [JRE](https://download.oracle.com/java/21/latest/jdk-21_windows-x64_bin.exe)
  * Configure JAVA_HOME Environment variables and paths on local system for connecting on-premise PostgreSQL to the Azure. [SetupGudie1](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/diepm/epm_set_java_home_104x6dd63633_106x6dd6441c.html#GUID-7D734C69-2DE8-4E93-A3C8-9C3F6AD12D1B) [SteupGudie2](https://docs.oracle.com/goldengate/1212/gg-winux/GDRAD/java.htm#BGBFJHAB)

![IR](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/c2dadfaa-ad8e-4865-a3e2-1db841880eed)

## Step 4: ADF Pipeline and Datasets Creation
  * Create a pipeline in ADF using Get Metadata, Lookup, Copy Data Functions.
  * Set up datasets for source (PostgreSQL and ADLS Gen2) and sink (ADLS Gen2 and Azure SQL DB).
    
![image](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/6b00ec10-944e-4368-b29f-fffaf2038d68)

## Step 5: Migrate Data to Azure Data Lake Gen2 with Dynamic Parameterization
  * Utilize lookup functions to dynamically retrieve schema and table names from postgreSQL using below script.
  * Implement dynamic parameterization in the copy data activity to insert data from PostgreSQL to ADLS Gen2, maintaining a hierarchy of folders for schemas and tables.
      ``` Dynamic Parameterization
    @{concat('SELECT * FROM ',item().schema,'.',item().table)}
  * Use ForLoop funciton and create copy data activity to insert data from PostgreSQL to ADLS Gen2, maintaining a hierarchy of folders for schemas and tables for every iteration.

![Copy Data From PostgreSQL 2](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/c363e79a-7acd-4a2f-ad04-0bc81724c571)

## Step 6: Staging Layer for Azure SQL DB
  * Leverage the ADLS Gen2 staging layer for any necessary transformations.
  * Migrate data from the staging layer to Azure SQL DB using copy data activities.
  * Use Get Metadata function to auto-generate schema and table names in Azure SQL DB, matching the structure of PostgreSQL.
 
![image](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/7b7be194-ddc0-4e04-9d1f-8e2aa17d670a)

## Step 7: Auto-Create SQL Tables with Pre-Script Execution
  * Auto-create SQL tables by dynamically parameterizing the outer loop output and inner loop output of the metadata function.
  * Utilize a pre-script to drop any existing tables with the same table and schema names before the migration process.
  ``` Dynamic Parameterization
  @concat('DROP TABLE IF EXISTS ',activity('Schema Metadata').output.childItems[0].name,'.',replace(item().name,'.txt',''))
  ```
![Copy Data To SQL Azure DB ](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/efaf53e3-a467-40f6-91a5-7a7fb6943cb0)

## Step 7: Validation, Data Migration
  * Validate the pipeline, schemas and table names to ensure consistency.
  * Debug with a sample or test tables and address any issues during the initial table migrations.
    
![image](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/39a67263-39f0-4a0e-90bf-c21b97366675)
    
## Step 8: Triggers for Automated Migration
  * Triggers are set up to automate the migration process after thorough testing and evaluation.
  * Triggers ensures that the data migration is initiated seamlessly, reducing manual intervention and enhancing the overall efficiency of the project.

![Triggers creation](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/5b303859-008e-4175-8301-c7e98683813a)

![image](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/e5e368e3-1b98-423c-a275-46b7967d74cc)


![SQL Output in ADS](https://github.com/CharanTejaV/Data-Migration-On-Premise-PostgreSQL-To-Azure-SQL-Database/assets/143735053/827f75f7-d788-4b64-88db-e0e7645a137c)

## Conclusion
This step-by-step guide demonstrates a seamless migration process from on-premise PostgreSQL to Azure SQL Database, incorporating Azure Data Lake Gen2 as a staging layer. The utilization of Azure services, dynamic parameterization, and Trigger Functions streamlines data movement, providing a scalable and efficient solution for cloud-based data storage and processing.

# THANK YOU

