# Cloud Native Appliction 

Cloud Native application is an approach to design , build and run scalable application on modern dynamic environment.

## Cloud Native Computing Foundation 
K8 ==> Orchestration , Prometheus ==> Monitoring , 
Open Tracing ==>Distributed tracing API , FluentD ==> Logging , Linkerd ==>Service Mesh , GRPC ==> Remote Procedure Call , Core DNS ==> Service Discovery , ContainerD ==> Container Runtime , CNI ==> Networking API , Envoy ==>Service Mesh , Jaeger ==> Distributed Tracing 

## Cloud Native Application vs   Traditional Application 
- In cloud native applictaion(CN App) need not worry about manitance of OS and Architecture which  will managed by the platform teams.
In case of traditional application it is OS dependent. 
- CN App is preditictable and it is right size capacity  where in traditional application is unpredictable and oversized capacity.
- CN app enables autoscaling and continous delivery with true agile model as it follows 12 factor application.
- Traditional application is waterfall model where the recovery rate is low when compared with CN App and manual scaling is exercised in it. 

## Why Cloud Native Appliction?

- Modularity 
- Observability
- Replacability
- Deployability 
- Testabilty 
- Disposibility 

## Introduction to the basic terms 

### Microservice
Microservice is an architectural style to build application in the form of small autonomous service.
Each microservice can have individual CRUD operations based on need 
### API
API is Application program Interface through which two or more applications communicate with each other to process the client request.
CRUD operations are used to communicate with client wrt to application feature and functionality. 

It is basically a set of  proceduer and functions which allows the consumer  to use the underlaying services of the application.

API acts as mediator between the client and function/feature of the app. Each service has its own API to communicate with client request service.It is a part of microservice. 

### REST API (Represented State Transfer) 
To retrieve the data lot of methods need to be used, in order to avoid this REST API  comes into picture.
REST API is an architectural style of an approach for communication that often used in web services development.

## Principle 

- Using microservices approach to build applications. 
- Package  micro services as containers.
- Use DevOps approach to deploy the infrastructure.
- Continuously delivery of application through pipeline for the end customer.

## Benifits
- Improves speed 
- Scalability 
- Management costs 

## Roadmapping strategies towards  Cloud Native Application 

- From technical point of view  the organization is in charge of building and running scalable applications. 

- Principles of CN App are considered as four major pillars where CN App assumes te organisation is already shifted to DevOps and CI/CD. 

**Scenario1:** In case of BAD assumption (assumption is incorrect).
Company : Non-Software Company - considering IT treated as call center rather than innovation hub. 

In the above case the business counter who are looking to modernize the business parts need a look and assess digital transformation 

- Goal: Client priority 

- Technical Impact :
 
This resonates very well with the technical side of the house, which needs to be able to ship code quickly, communicate effectively, and be able to run experiments. The principles of Devops helps not just modernise the infrastructure but also the business.  architectural perspective it gives you the opportunity to start on a journey to modernize your infra. There are plenty of startups that use Kubernetes to either build or power all of their technologies. There are also plenty of enterprises that build their new application stack on Kubernetes and also take steps to move the existing infrastructure to the Kubernetes environment. 

- Architectural perspective: 

Opportunity modernize your infra using Kubernetes.Many startups that use Kubernetes to either build or power their technologies. Some enterprises build their new application stack on Kubernetes and also take steps to move the existing infrastructure to the Kubernetes environment. 

## Realtime case study : NORDSTROM  

Department store in America where people often buy jeans 

**Challenge**: To increase the speed and efficiency of technology operations 

**Application**: Building on CI/CD project , providing container tecnologies  to DevOps teams

**Solution**: K8 
 
Engineering team : Early container adopters 

This increased their development velocity and decreased their time to commit enabling their reduced their release-to-production time from three months to 30 days. 
The first application deployed on Kubernetes was their internal Jira server. 

Jira is a common bug tracking software used by many companies,
 and it's fascinating that Nordstrom started with this specific use case to make
 the shift to Kubernetes to manage software more efficiently. 

Using Kubernetes to ship software allows to standardize across the groups and build bridges between the teams.

- Operation Prespective :

1. Ability to handle the infra in agile manner 

2. Scaling the infra in simple way

3. Platform features allows operation team to be more resilient to recover from app failure. Allows the ops team to allocate more time on building better infra.

- Lead time will be reduced 
- Shipping code faster to Customer : 

Enables the organization jumped  into to cloud native will have a natural alignment between business and technology, and different technology teams. 

This is very much similar to common and famous case study  **Box**

The impact of Kubernetes has allowed the company to shift microservices in a week, as opposed to six-month release cycles.

## Overcoming Challenges 

1. Business justification for using cloud native : 

Issue: Architects - hard time selling Kubernetes and the cloud native stack internally

Strategy : Getting buy-in

To partner with business teams looking for new processes or technologies, 
or allying with the digital transformation initiative.

The requirements for both of these efforts are complimentary and cloud native will help you accelerate the transformation. 

2. To be a cloud native necessary need to use DevOps , CI/CD , Containers and Microservices  : 

Not very necessary to have DevOps, the mindset, tooling and expertise learned from the DevOps side of the house is immensely useful. 

DevOPs or SRE personnel are required to debug issues related to worker nodes and maintaining Kubernetes cluster. 

It's vital to have a continuous integration pipeline, to build and push container images in order to automate parts of the pipeline. 

Continuous delivery - committing to this principal after couple of Kubernetes production deploys.

This allows you to know the existing processes and then continuously deploy the applications to the customers.

3. K8 or Serverless

Both are fast growing with high adoption curve.

Small team / organisation : Serverless

Large team / organisation : K8

Issues raised by the CNCF in their survey in 2018.

**Primary challenges:**

- Cultural challenges

- Lack of security 

- Lack of training . 

**Secondary Challenges:**

- Monitoring 
- Storage 
- Networking 

## Accessing existing infra 


- Cloud Native technologies on premise, or in the public cloud. 

To run infrastructure in the public cloud, adding K8 easier .

Method 1: both the control plane and data plane

Method 2: Using the managed service provided  by the provider like EKS on AWS, GKE on Google Cloud, AKS on Azure.


















