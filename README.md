***
***
## CDK Stack for QuickSight Dashboard
### Purpose:
This CDK stack creates a **QuickSight** dashboard, enabling front end users to check their past activities.

### Included Services:
- **Kinesis Data Stream & Firehose**
- **Lambda**
- **S3 Bucket**
- **Glue Crawler & Table**
- **IAM Roles**
- **KMS**

### Description
The **QuickSight** Dashboard CDK stack creates a **Kinesis Data Stream** captured by **Kinesis Firehose**. 
A **Lambda** function transforms the processed stream between **Firehose** and its connected **S3** bucket (KMS enabled). 
A **Glue Crawler** crawls the processed data from S3 into its **Glue table**. 
**Quicksight** then, uses Athena as a query service to query the **Glue table** and creates the dashboard (not included in this CDK stack).

The CDK stack takes care of all connections, **IAM** roles and **KMS** encryption settings.

### Important Note:
The Kinesis Data Stream captures data from DynamoDB. The presented CDK stack is missing a direct dependency between DynamoDB and Kinesis Data Stream (not yet included in CDK in general). 
As a workaround, please create this dependency using the following CLI command: 
```console
  enable-kinesis-streaming-destination
--table-name <value>                    //Name of DynamoDB table
--stream-arn <value>                    //ARN for Kinesis Data Stream
[--cli-input-json | --cli-input-yaml]   //Reads arguments from the JSON string provided
[--generate-cli-skeleton <value>]       //Prints a JSON skeleton to standard output without sending an API request
```
