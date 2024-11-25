Integrations with other AWS services:

API Gateway -> Lambda  (REST APIs)
S3 -> Lambda (Data processing)
SQS -> Lambda (Message Buffering & Processing)
SNS -> Lambda (Message Processing)
Step Functions -> Lambda (Workflow Orchestration)
DynamoDB -> Lambda (Change Detection)
---------------------------------------------------------------------------------------------------------------------------------------
1. Lambda@Edge

Lambda@Edge enables the deployment of Lambda functions in multiple AWS edge locations globally. This ensures low-latency responses by executing code close to the end-user. Common use cases include caching, request/response manipulation, and user authentication at CloudFront's edge.

Key points to mention:

    Used with Amazon CloudFront.
    Supports global availability and low latency.
    Ideal for request/response transformations and content delivery.

2. Lambda Destinations

Lambda Destinations provide a native way to route the asynchronous execution results of a Lambda function (both successes and failures) to other AWS services like Amazon SQS, SNS, EventBridge, or another Lambda function.

Key points to mention:

    Simplifies event-driven architecture by managing success and failure paths.
    Reduces the need for additional monitoring or custom retry logic.
    Example: Send a failed event to an SQS queue for later processing.

3. Lambda Layers

Lambda Layers allow you to share libraries, custom runtimes, or dependencies across multiple Lambda functions. Instead of bundling dependencies within each function, they can be added as separate layers to reduce deployment size and improve maintainability.

Key points to mention:

    Reusable across multiple functions and accounts.
    Helps separate code from dependencies.
    Example: Packaging Python libraries or Node.js modules as a shared layer.

4. Provisioned Concurrency (Cold Start Optimization)

Provisioned Concurrency ensures that a predefined number of function instances are initialized and kept ready to handle requests immediately. This eliminates cold starts, where Lambda functions experience latency when invoked for the first time or after a period of inactivity.

Key points to mention:

    Reduces startup latency (cold start) for critical workloads.
    Ensures consistent performance for high-throughput or low-latency applications.
    Useful for APIs, real-time data processing, and synchronous workloads.
--------------------------------------------------------------------------------------------------------------------------------------------------------------
Invoke lambda from another lambda

https://www.datacamp.com/blog/aws-lambda-interview-questions
