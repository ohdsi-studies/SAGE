# SAGE

Requirements
============

- A database in [Common Data Model version 5](https://github.com/OHDSI/CommonDataModel) in one of these platforms: SQL Server, Oracle, PostgreSQL, IBM Netezza, Apache Impala, Amazon RedShift, Google BigQuery, or Microsoft APS.
- R version 4.0.0 or newer
- On Windows: [RTools](http://cran.r-project.org/bin/windows/Rtools/)
- [Java](http://java.com)
- 25 GB of free disk space

How to run
==========
1. In RStudio, select 'Build' then 'Install and Restart' to build the package.

2. Once installed, you can execute the study by modifying and using the code below. For your convenience, this code is also provided under `extras/CodeToRun.R`:

	```r
	library(SAGE)

	# The folder where the study intermediate and result files will be written:
	outputFolder <- file.path("outputFolderDir")

	connectionDetails <- DatabaseConnector::createConnectionDetails(
	  dbms = 'postgresql',
	  server = 'myserver',
	  user = 'joe',
	  password = 'secret',
	  pathToDriver = 'S:/jdbcDrivders'
	)


	# The name of the database schema where the CDM data can be found:
	cdmDatabaseSchema<-'CDM_mydb.dbo'

	# The name of the database schema and table where the study-specific cohorts will be instantiated:
	cohortDatabaseSchema <- 'mydb.dbo'
	cohortTable <- "SAGE"

	# Some meta-information that will be used by the export function:
	databaseName <- 'MYDATABASE'


	execute(connectionDetails = connectionDetails,
	        cdmDatabaseSchema = cdmDatabaseSchema,
	        cohortDatabaseSchema = cohortDatabaseSchema,
	        cohortTable = cohortTable,
	        outputFolder = outputFolder,
	        databaseName = databaseName,
	        createCohorts = TRUE,
	        runPrescriptionNum = TRUE,
	        runDUR = TRUE,
	        resultsToZip = TRUE,
            yearStartDate = as.Date("2018-01-01"),
            yearEndDate = as.Date("2022-04-30"),
            monthStartDate = as.Date("2018-01-01"),
            monthEndDate = as.Date("2022-04-30"))

	```

3. Share the file ```drugCohort_<DatabaseId>.zip``` in the output folder to the study coordinator

Development
===========
SAGE package is in development
