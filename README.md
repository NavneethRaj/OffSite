# OffSite
Quick Info

## Phase 1

# Batch/Schedule

1) Open Connection (Extract existing data)
    *  Establish connection between Dremio and PrimeNext RDBMS
          - PrimeNext team might need to open external connection to dremio
          - Once firewall is open, VEL team can setup connection to their RDBMS 
            - Reflection configs if needed
            - Metadata refresh config
            - Access control using AD groups
    *  Create PDS for queries
    *  Create VDS as per frequent query usage
2) Integrate with DGUpload (New data ingestion)
    *  Request the PrimeNext team to integrate with our DGUpload and share the docs
         - DGUpload in DEV might need a redeploy with stable code
         - Bruce had tried to integrate Ramen service, dont deploy this change rather deploy DGUpload without Bruce's change
    *  Create a path in HDFS for PrimeNext team
    *  All the new data should be ingested using DGUpload only 
    *  Once the new data is available in HDFS, VEL team will configure dremio to access PrimeNext's HDFS path
          - Reflection configs if needed
          - Metadata refresh config
          - Access control using AD groups
    *  PrimeNext team can start creating PDS for the same
    *  PrimeNext can start creating VDS as per requirements 
3) Aggreagte Step 1 (PDS/VDS) + Step 2 (PDS/VDS)
    * PrimeNext team can perform analytics/aggreagate operations on top of both the data sources
    * Create necessary reports as VDS
4) Start consuming the datasets
    * PrimeNext team can start integrating with dremio using available connectors
    * Once the connectors are integrated, PrimeNext team can start consuming the data


# Streaming
1) Open Connection (Streaming topics)
    * Open connection for PrimeNext streaming
        - Assuming PrimeNext wants to listen to external producer, we would want to open connection to this producer so that our kafka broker can listen
        - Firewall request might be needed on PrimeNext team's end
        - Once the connection is open, lets create a listerner in our infoplatform to listen to the topic
2) Establish Druid connection to Step-1 Kafka topic
     * Setup a new connection in Druid-DB to load the Step-1's kafka messages
     * Make the necessary config changes for the data if needed (optional)
     * Create the dataset in Druid
3) Query streaming data 
     * PrimeNext team can integrate with druid as per their needs 
     * PrimeNext team can use any druid interfaces to connect
     * PrimeNext team can run queries on top of their datasets
  
## Phase 2

# Batch/Schedule

1) Check the performance of RDBMS + HDFS queries
     * If the performance is slow then
         - We need to ingest the RDBMS data to HDFS (one time job)
         - Recommended approach will be extrating RDBMS to parquet -> upload to HDFS
              - Can be Spark JOB
2) TBD
