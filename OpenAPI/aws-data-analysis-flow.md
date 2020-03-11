# AWS Data analysis flow

## Data Analysis flow

1. Collect / Ingest Data

   - Needs Event Pipeline
   - Event Pipeline Approach #1

     API Gateway Call a Lambda for every API call and then upload the payload into an S3 bucket.

     - Pros: Simple
     - Cons: It gets costly when throughput increases.

   - Event Pipeline Approach #2

     Directly invoke the Kinesis Firehose from an API Gateway.

     - Pros: Avoid cost of Lambda and S3 request.
     - Cons: 
     - [Get Started](./build-event-pipeline-kinesis.md)

2. Store

   - S3
   - RDS

3. Process / Analyze

   - EMR (Redshift, Spark)

4. Visualize / Report

## To get more insights

- [야생의 땅 듀랑고의 데이터 엔지니어링 이야기](https://www.slideshare.net/ssuser380e9c/ndc18-95524337)
- [Kinesis와 Lambda를 이용한 비용 효율적인 센서 데이터 처리](https://www.slideshare.net/awskr/kinesis-lambda-77400693)
- [Data Analytics Flow & Components](https://aipkds.tistory.com/?page=9)
- [AWS를 통한 빅데이터 기반 비지니스 인텔리전스 구축](https://www.slideshare.net/awskorea/1-bigdata-bi-configuration)
- [Build Serverless Real-Time Analytics Pipelines for Mobile Gaming](https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/serverless-analytics-for-mobile-gaming.pdf?did=wp_card&trk=wp_card)
- [How to build an Event Pipeline within 1 hour and minimum lines of code in AWS](https://medium.com/a-tale-of-2-from-data-to-information/how-to-build-an-event-pipeline-within-1-hour-and-minimum-lines-of-code-in-aws-eb1bd0bb6cd2)
