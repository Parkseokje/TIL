# Build Event Pipeline using Kinesis

## Steps

- Create a Kinesis stream
- Create API Gateway points
- Create IAM Role from `API Gateway` type
- Attach `AmazonKinesisFullAccess` policy
- Copy the Role ARN from the role summary page and save it for future use.
- From API Gateway follow this [instructions](https://docs.aws.amazon.com/apigateway/latest/developerguide/integrating-api-with-aws-services-kinesis.html)
- Deploy API Gateway. [more](https://docs.aws.amazon.com/ko_kr/apigateway/latest/developerguide/how-to-deploy-api-with-console.html)
- Test API Gateway. [more](https://docs.aws.amazon.com/ko_kr/apigateway/latest/developerguide/api-gateway-export-api.html)

## To get more insights

- [How to build an Event Pipeline within 1 hour and minimum lines of code in AWS](https://medium.com/a-tale-of-2-from-data-to-information/how-to-build-an-event-pipeline-within-1-hour-and-minimum-lines-of-code-in-aws-eb1bd0bb6cd2)
- [Getting Started with Data Analysis on AWS](https://towardsdatascience.com/getting-started-with-data-analysis-on-aws-7b74ecbfe572)
- [TUTORIAL: Create a REST API as an Amazon Kinesis Proxy in API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/integrating-api-with-aws-services-kinesis.html)