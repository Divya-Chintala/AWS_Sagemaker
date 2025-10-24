**Stream-based taxi fare prediction using AWS Kinesis Data Streams, Kinesis Data Analytics (Apache Flink) and Amazon SageMaker.**  


Taxi Fare Prediction -  Real-time ML with AWS Kinesis & SageMaker project uses a subset of the **NYC Taxi & Limousine Commission (TLC) Trip Record Data**, Features include pickup/dropoff timestamps, locations, passenger count, fare amount, etc. This project trains regression model (SageMaker Linear Learner), deploys it to a SageMaker endpoint, streams synthetic taxi events into Kinesis, invokes the endpoint asynchronously from a Flink (KDA) app, and stores predictions in S3. 

---

## Overview

The pipeline performs **real-time inference** on streaming taxi trip records:

1. A data generator emits taxi trip records into an **Amazon Kinesis Data Stream**.  
2. **Kinesis Data Analytics (Apache Flink)** reads the stream and for each record performs an asynchronous HTTP call that triggers a **Lambda + API Gateway** which invokes the **SageMaker endpoint**.  
3. The prediction: predicted fare is saved to an S3 `resultset/` location, paired with the input record for later analysis.

Key AWS components used:
- Amazon SageMaker -> Linear Learner algorithm
- Amazon S3 (for data, artifacts, .jar , resultset)
- Amazon Kinesis Data Streams
- Amazon Kinesis Data Analytics -> Apache Flink
- Amazon API Gateway + AWS Lambda
- Cloud9 to run the data generator
