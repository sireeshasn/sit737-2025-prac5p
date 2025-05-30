# sit737-2025-prac5p
SIT737-2025-prac5p: Containerisation of a Simple Web Application Using Docker
Overview
This repository contains a Node.js-based calculator microservice developed to demonstrate cloud-native application development concepts. The primary objective is to containerize this microservice using Docker, manage deployment using Docker Compose, implement health checks, and push the container image to Docker Hub. The application exposes RESTful API endpoints capable of performing various arithmetic operations such as addition, subtraction, multiplication, division, exponentiation, square root, and modulo.

Application Features
The enhanced calculator microservice supports seven arithmetic operations via clearly defined API endpoints:

Addition (/add?num1=10&num2=5)

Subtraction (/subtract?num1=10&num2=5)

Multiplication (/multiply?num1=10&num2=5)

Division (/divide?num1=10&num2=5)

Exponentiation (/power?num1=2&num2=3)

Square Root (/sqrt?num=16)

Modulo (/modulo?num1=10&num2=3)

All endpoints accept numeric input parameters and return JSON-formatted results, alongside descriptive logging handled by the Winston logging library for easier monitoring and debugging.

Dockerization Approach
Docker simplifies software delivery by packaging applications into portable containers. To containerize the calculator microservice, a Dockerfile specifying the base Node.js image (node:20-alpine) was created. Dependencies from package.json are installed within the Docker image, followed by copying the application’s source code. The Dockerfile exposes port 3000, the application’s runtime port, ensuring accessibility outside the container. The Docker image can be built quickly and reproducibly using the following command:



docker build -t enhanced-calculator-app .
Docker Compose and Health Checks
Docker Compose automates the deployment and management of multiple containerized services, simplifying orchestration tasks. The docker-compose.yml file specifies service configurations, container naming, port mappings (3000:3000), and robust health check instructions. These health checks periodically validate service responsiveness, querying a specific endpoint (/power?num1=2&num2=3) every 30 seconds. If the health check fails three consecutive times, Docker automatically restarts the affected container. The application is deployed and started easily using:

docker-compose up -d
This simplifies scalability and ensures continuous service availability through automatic restarts.

Testing and Validation
Comprehensive testing verifies the successful deployment and operational status of the application. Users can test endpoints using browsers, Postman, or curl. For instance, the following curl command tests the exponentiation functionality:

http://localhost:3000/power?num1=2&num2=3
The expected response is a JSON object confirming the successful calculation:

{
  "operation": "power",
  "result": 8
}
Docker Hub Integration
The containerized application was published to Docker Hub to enable public accessibility and distribution. After authenticating via the Docker CLI (docker login), the Docker image was tagged and pushed to Docker Hub as follows:

docker tag enhanced-calculator-app sireeshasn/enhanced-calculator-app:latest
docker push sireeshasn/enhanced-calculator-app:latest
The publicly accessible Docker image can now be pulled directly from Docker Hub:

Docker Hub URL: https://hub.docker.com/r/sireeshasn/enhanced-calculator-app
