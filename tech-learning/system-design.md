# System Design
https://rubygarage.org/blog/monolith-soa-microservices-serverless

## Architecture

### Monolith

#### Pros
- Single self-contained
- Simpler
    - deployment
- Fewer cross-cutting concerns
- Better performance
    - no need for 40 API calls between services

#### Cons
- Codebase becomes sphaghetti
    - tight coupling
    - harder to add new features
    - hard to onboard new devs
- Difficult to adopt new technologies
    - can break things if you update the Django version
- less reliable
    - breaking one thing can break everything

#### What it looks like

* Front End: React
* Monolithic with all the business logic
* DB

#### When to use monolith

- Etsy
- Forma
    - to get stuff working asap

### SOA: Service Oriented Arch

* Reusable components

* Enterprise Scope. Shared ESB. Uses SOAP, AMQP, MSMQ

#### Pros

- Reusability of services
- Better maintainability
    - modules that can be maintainted without knowing the whole system
- Higher reliability
- Parallel development

#### Cons

- Complex management
- High investment costs
- Extra overload

Architecture:

Front End - Angular?

Elastic Load Balance

AWS API Gateway

Services:

Deploy on EC2 (sever) or AWS Lambda (serverless)

Ex for farming sector:

\- Soil lab 1

\- Soil lab 2

\- Farm

\- Accountant

\- Market

RDS/Redshift,Redis,DynamoDB S3, Glacier

Caching

CDN

Kafka

Sharding

Fraud Detection

Microservice - Reusable components. Application Scope. Uses REST, JMS

Pros:

Easy to develop, test, and deploy

Increased agility

Ability to scale horizontally

Cons:

Complexity

Security concerns

Different programming languages

Architecture:

Front End - Angular?

Elastic Load Balance

AWS API Gateway

Microservices:

Deploy on EC2 (sever) or AWS Lambda (serverless)

Ex for Instagram:

\- Upload

\- View

\- Search

\- Account

\- Follow

\- Trending

\- Monitoring

RDS/Redshift,Redis,DynamoDB S3, Glacier

Caching

CDN

Kafka

Sharding

Fraud Detection

Serverless - Cloud computing, no infrastructure management. Uses FaaS (Frontend as a service) and BaaS (Backend as a Service). Accomplishing one-time tasks and auxiliary processes

Pros:

Easy to deploy

Lower costs (No DB, some logic, servers)

Enhanced scalability

Cons:

Vendor lock-in

Not for long-term tasks

Web Service Communication Protocols:

SOAP - ACID compliant, security, stateful

REST - Performs better, caching, less refactoring headache, stateless

graphQL - Quickly evolving product iterations, over/under fetch, stateless

Services May Include Machine Learning:

https://duckduckgo.com/?q=sagemaker+pipeline&t=brave&iax=images&ia=images&iai=https%3A%2F%2Fdatabricks.com%2Fjp%2Fwp-content%2Fuploads%2F2020%2F06%2Fblog-aws-sessions-1.png

Preprocess using PySpark, Build and Train Using Sagemaker, Deploy to EC2

Classifier:

Random Forest -> Easy to overfit

Logistic Regression

Gradient Boost -> Longer to run, overfit

NN -> long train time, need lots of data. Complex hyperparameter

SVC

Naive Bayes

Regression:

RFR

LR

Decision Tree

Gradient Boosting

NN

Recommendation:

SVD -> Collaborative. Example: TasteWright.

Cosine Similarity -> Content. Example: Amazon Products

Hyrbid -> Use both. Example: Netflix

Clustering:

K-means

Images:

CNN

Text:

LDA

NN -> LSTM, CNN, Transformers

Exaples:

Banking (SOA, SOAP):

https://www.dragon1.com/images/ibm-reference-soa-for-banking.png

Farming (SOA, SOAP):

https://www.researchgate.net/figure/Three-layered-SOA-architecture-with-some-illustrative-examples-of-components-from-the\_fig3\_221953757

Uber (Microservice, REST):

https://media.geeksforgeeks.org/wp-content/cdn-uploads/20201120210648/Uber-System-Design-High-Level-Architecture.png

Instagram (Microservice, REST):

https://www.thetechplatform.com/post/system-design-instagram

Shopping (Microservice, GraphQL):

https://miro.medium.com/max/4000/0*VNcIhiztbake81ex.png

Random (Microservice, GraphQL):

https://cdn-images-1.medium.com/max/2000/1*up1Yb8Kn1rWJGCn1bFYKxg.png

Medical Image Analysis Machine Learning (Serverless):

https://d2908q01vomqb2.cloudfront.net/c5b76da3e608d34edb07244cd9b875ee86906328/2020/12/09/Picture3-2.png

Pipeline Automation Machine Learning (Serverless):

https://miro.medium.com/max/2400/1*3mB27NYBVWEmwhus-w3ULw.png

Sagemaker VS Databricks

Databricks is a better platform for Big data(scala, pyspark) Developing.(unbeatable notebook environment)

SageMaker is better for Deployment. and if you are not working on big data, SageMaker is a perfect choice working with (Jupyter notebook + Sklearn + Mature containers + Super easy deployment).

SageMaker provides "real time inference", very easy to build and deploy, very impressive. you can check the official SageMaker Github. https://github.com/awslabs/amazon-sagemaker-examples/tree/master/sagemaker-python-sdk/scikit\_learn\_inference_pipeline