# SpotifyETL2
It is an end to end project from getting data from Spotify API to having it on Snowflakes 



# Spotify Data Pipeline with AWS and Snowflake

## Overview

This project aims to create a data pipeline to extract, transform, and load (ETL) Spotify's top 100 Hindi songs data into Snowflake data warehouse using various AWS services such as Lambda, S3, Glue, and Snowpipe. The pipeline utilizes Apache Spark for transformation to explore its capabilities in distributed processing.

## Prerequisites

Before setting up the pipeline, ensure you have the following:

- Access to AWS services
- Access to Snowflake data warehouse
- Spotify Developer account for API keys
- Basic knowledge of AWS Lambda, S3, Glue, Snowflake, and Apache Spark

## Architecture

<img width="524" alt="image" src="https://github.com/viraniriaz/SpotifyETL2/assets/82742908/44750134-ee33-4274-a484-b6a0baf5b9ad">

The architecture of the data pipeline is as follows:

1. **Spotify API Integration**: Retrieve API keys from Spotify Developer account.
2. **Lambda Function**: Use Lambda to extract data from Spotify API and fetch the top 100 Hindi songs.
3. **S3 Bucket**: Store the extracted data in an S3 bucket.
4. **AWS Glue**: Utilize Glue for transformation using Apache Spark code.
5. **Snowflake Integration**: Load transformed data into Snowflake data warehouse using Snowpipe.
6. **Event Notification**: Set up event notifications from Snowpipe to S3 bucket for continuous data loading into Snowflake tables.

## Setup Instructions

1. **Spotify API Keys**:
   - Sign up or log in to the Spotify Developer Dashboard.
   - Create a new application to obtain API keys (Client ID and Client Secret).

2. **AWS Configuration**:
   - Set up Lambda function to extract data from Spotify API.
   - Create an S3 bucket to store extracted and transformed data.
   - Configure Glue job to perform transformation using Spark code.
   - Set up Snowflake integration using AWS S3 storage integration.

3. **Code Deployment**:
   - Deploy the Lambda function code for data extraction.
   - Upload Apache Spark code for transformation to Glue job.
   
4. **Snowflake Configuration**:
   - Configure Snowflake to utilize AWS S3 as an external stage.
   - Set up Snowpipe to load data from S3 bucket into Snowflake tables.

## Usage

1. **Data Extraction**:
   - Lambda function will trigger data extraction from Spotify API periodically.
   - Extracted data will be stored in the configured S3 bucket.

2. **Transformation**:
   - Glue job will automatically run Spark code for data transformation.
   - Transformed data will be stored back in the S3 bucket.

3. **Data Loading**:
   - Snowpipe will continuously load transformed data from S3 bucket into Snowflake tables.
  
     
## Transformation Process

The transformation process is implemented using Apache Spark in AWS Glue. Below are the key steps involved in the transformation:

1. **Extracting Albums Information**:
   - The `process_albums` function extracts information about albums from the Spotify data.
   - It selects relevant attributes such as album ID, name, release date, total tracks, and URL.
   - Duplicate albums are removed based on their unique ID.

2. **Extracting Artists Information**:
   - The `process_artists` function extracts information about artists from the Spotify data.
   - It explodes the array of artists within each track to create a row for each artist.
   - Relevant attributes such as artist ID, name, and external URL are selected.
   - Duplicate artists are removed based on their unique ID.

3. **Extracting Songs Information**:
   - The `process_songs` function extracts information about songs from the Spotify data.
   - It explodes the array of items to create a row for each song.
   - Relevant attributes such as song ID, name, duration, URL, popularity, and added date are selected.
   - Duplicate songs are removed based on their unique ID.
   - The added date is converted from a string to a date type.

4. **Writing Transformed Data to S3**:
   - The `write_to_s3` function converts the transformed DataFrame back to a DynamicFrame.
   - Transformed data is written to S3 in CSV format, partitioned by date.
  
     
## Contributors

- Riaz Virani, Darshil Parmer




