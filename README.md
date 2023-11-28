<div id="top"></div>

<!-- PROJECT LOGO -->
<br />
<div align="center">
    <img src="images/Logo.jpg" alt="Logo" width="150" height="120">

  <h3 align="center">GoMart</h3>

  <p align="center">
    Supermarket Website build using AWS
  </p>
</div>

<!-- ABOUT THE PROJECT -->
## About The Project
GoMart is an online supermarket website build using AWS and offers high availability, scalability, and robust security features
<p align="right">(<a href="#top">back to top</a>)</p>

<!-- Solution Architecture -->
## Solution Architecture
![Solution Architecture](/images/Cloud_Solution.jpg)
<p align="right">(<a href="#top">back to top</a>)</p>

<!-- GETTING STARTED -->
## Getting Started

1. Change directory
   ```
   cd services
   ```
3. Start all services
   ```sh
   docker compose up
   ```

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- Built With -->
## Built With

<div align="center">
  <img src="/images/tech_stack.png" alt="Tech Stack">
</div>

### Frontend
* [Vue.js](https://vuejs.org/)
* [React.js](https://reactjs.org/)

### Backend
* [Flask](https://flask.palletsprojects.com/en/3.0.x/)
* [Docker](https://www.docker.com/)

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- Requirements-->
## Technical Requirements
| Category                | Description                                                                                           |
|-------------------------|-------------------------------------------------------------------------------------------------------|
| Reliability             | - Systems must have the ability to recover from failure within the RTO and have data loss not exceeding the RPO. <br> - Persistent and durable data storage to prevent data loss. We aim to eliminate as many single points of failure as possible. <br> - Having automated backups at least every 12 hours. |
| Performance Efficiency  | - Website can be displayed to at least 1,000 concurrent users in <1s. <br> - Order Validations should take <1s. <br> - Checkout Validation should take <3s. |
| Operational Excellence  | - Metrics, Logs, and Traces must be set up to ensure the company always meets SLAs. <br> - Automated Notifications should be present to alert the team of any spike in metrics or application failures within 20 mins. |
| Security & Network      | - Principle of least privilege will be implemented and AWS resources will be duly separated from one another, with appropriate authorization accounted for during the interaction with AWS resources. <br> - Firewalls and DDoS protection are set up to stop network attacks while protecting the system’s storage and data flow. <br> - Key services will not be accessible from the Internet. <br> - Data, including Personally Identifiable Information (PII), must be properly encrypted or masked in transit and at rest. |
| Cost Management         | - Proper resource management ensures that the company only pays for required resources, nothing more, with an automatic increase or decrease in usage depending on business needs. <br> - Metrics and Logs will measure the business output from workloads. |
| Maintainability         | - Small and frequent system changes should have zero downtime. <br> - Automated CI/CD pipeline completes within 30 minutes. <br> - Microservices architecture will be implemented so that changes to one component will have minimal impact on others. |

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- Machine Learning Pipeline -->
##  Machine Learning Pipeline
<div align="center">
  <img src="/images/ml_pipeline.png" alt="ML Pipeline">
</div>

### S3
The first component, S3, is used to store the raw data that will be used to train the machine learning model. The training data is from DynamoDB and is stored in a csv format in S3.

### SageMaker
The second component, Amazon SageMaker, is used to create and train the machine learning model using K Nearest Neighbours using features from the supermarket items such as price and categories. 

### SageMaker endpoint
The third component, SageMaker endpoint, is used to deploy the trained machine learning model. The endpoint provides a REST API that can be used to perform real-time predictions on new data.

### AWS Lambda
Finally, the AWS Lambda function is used to integrate the machine learning pipeline with other parts of the system. The Lambda function is triggered when an API request is made to the SageMaker endpoint.

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- Design Considerations -->
## Design Considerations
### Multi-AZ Deployment
<div align="center">
  <img src="/images/fargate.JPG" alt="Fargate" height="400" width="500">
</div>
Fargate tasks were deployed across 2 AZs (active-active setup) in the Singapore region to ensure high availability even if 1 AZ goes down 

### Elasticache
<div align="center">
  <img src="/images/ElasticCache.JPG" alt="ElasticCache" height="300" width="300">
</div>
Elasticache helps to increase the performance and responsiveness of Go Mart’s application by storing frequently accessed data in a cache, which can be quickly retrieved and served to the user, instead of having to make multiple repeated read requests to DynamoDB. This helps to ensure scale of up to the millisecond level, and that DynamoDB will not be swarmed with too many IOPs. We a cache read-through strategy and set the cache expire TTL to 5 min.

### CI/CD Pipeline
<div align="center">
  <img src="/images/CICD.JPG" alt="CICD" height="200" width="300">
</div>

<ins>3 Main Pipelines were implemented </ins> 

1) gomart-build-BE: Builds the necessary docker images and pushes it into ECR’s private repository. This uses a Continuous Delivery idea to give Go Mart developers the power to decide when to push to production, and also because no staging environment was set up, it would not be ideal to have all changes go directly into production - this puts Go Mart’s SLAs at risk.

2) gomart-deploy-BE: Deploy production-ready ECR images into the ECS services

3) gomart-deploy-FE: Builds necessary frontend files and pushes it to a s3 bucket that hosts Go Mart’s website. This pipeline is customised to be triggered whenever there is a change in the master branch.


<p align="right">(<a href="#top">back to top</a>)</p>


