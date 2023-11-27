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

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project
GoMart is an online supermarket build using AWS and offers that offers high availability, scalability, and robust security features
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
The second component, Amazon SageMaker, is used to create and train the machine learning model using K Nearest Neighbours using features from the supermarket items such as price and categories. SageMaker provides prebuilt Docker images that install the scikit-learn and Spark ML libraries.

### SageMaker endpoint
The third component, SageMaker endpoint, is used to deploy the trained machine learning model. The endpoint provides a REST API that can be used to perform real-time predictions on new data.

### AWS Lambda
Finally, the AWS Lambda function is used to integrate the machine learning pipeline with other parts of the system. The Lambda function is triggered when an API request is made to the SageMaker endpoint.

<p align="right">(<a href="#top">back to top</a>)</p>



