Using the power of Serverless and the serverless-domain-manager plugin, 
API Gateway's can be used for base path mappings to handle this.
Follow the instructions below to deploy your two services to the same domain.
## Prerequisite 
Need  have the  desired domain name registered through AWS.
Register a certificate for that domain through the AWS Certificate Manager.

## Deploying two services
Imagining an e-commerce store shopping single-page application that consumes a backend REST API. 
REST API is hosted at api.mycompany.com, with two services: 

- users 
- products

### Goal :
- users requests  need to accessed using  api.mycompany.com/users 
- products requests at api.mycompany.com/products
- deploying the two services independently 
- Modification to a products at endpoint without redeploying all the user functions 

## Implementation : 

Step1 : Two new directories for application and user  need to be created 

 >open terminal 

$ mkdir api-gateway-application

$ cd api-gateway-application

$ mkdir users-service

$ cd users-service

Step 2:Adding serverlessappliction.yml file to the user directory 

example : 

service: users-service

provider:

  name: aws

  runtime: python3.6

  stage: dev

  region: eu-west-1

  environment:

    SERVICE_NAME: ${self:service}

functions:

  hello:

    handler: handler.hello

    events:
      - http: GET hello


### adding handler.py:

import os

def hello(event, context):

    response = {

        "statusCode": 200,

        "body": "Hello from the {}!".format(os.environ.get('SERVICE_NAME'))

    }

    return response

### single endpoint (/hello) service for testing & deploying the service:

$ sls deploy
...

Service Information

service: users-service

stage: dev

region: eu-west- 1

stack: users-service-dev

api keys:

  None

endpoints:

  GET - https://n0benf6jn4.execute-api.us-east-1.amazonaws.com/dev/hello
functions:

  hello: users-service-dev-hello

- check the endpoint pasting it in browser

Step3: 
To fix the URL copying the users-service into a products-service director leveling up the directory 

$ cd ..

$ cp -r users-service/ products-service

$ cd products-service

### adding the  serverless.yml

service: products-service

provider:
  
name: aws
  runtime: python3.6

  stage: dev

  region: eu-west-1
  
environment:

    SERVICE_NAME: ${self:service}

functions:

  hello:

    handler: handler.hello

    events:
      - http: GET hello

To deploy run sls for the products-service and check the browser working or not.

Step4: 
Adding your services to your custom domain

// installing the serverless-domain-manager plugin

$ npm init -f

$ npm install serverless-domain-manager

// Configuration file need to be added

service: products-service

provider:

  name: aws

  runtime: python3.6

  stage: dev

  region: eu-west-1

  environment:

    SERVICE_NAME: ${self:service}

functions:

  hello:

    handler: handler.hello

    events:
      - http: GET hello

plugins:
  - serverless-domain-manager

custom:

  customDomain:

    domainName: 'api.mycompany.com' # Change this to your domain.

    basePath: 'products' # This will be prefixed to all routes

    stage: ${self:provider.stage}

    createRoute53Record: true

Step 5:

Registered the serverless-domain-manager in the plugins block in above example two sections are added.
Later configured the plugin through the customDomain section of the custom block.

Where the basePath attribute that are configuring will be prefixed to every route in our products-service.
 Thus, the  route that is registered as /hello will actually be located at products/hello.

previously it is not registered in this domain with API Gateway, now we need to register it:

$ serverless create_domain

It is one time setup cost when the domain is set up provisioning with AWS , deploy your service with sls deploy. 
Where endpoint will be available at api.mycompany.com/products/hello:

Step 6:Repeat the procedure in user service 

$ cd ../users-service

Installing the serverless-domain-manager plugin and add the configuration file.

service: users-service

provider:

  name: aws

  runtime: python3.6

  stage: dev

  region: eu-west-1
 
 environment:

    SERVICE_NAME: ${self:service}

functions:

  hello:

    handler: handler.hello

    events:
      - http: GET hello

plugins:
  - serverless-domain-manager

custom:

  customDomain:

    domainName: 'api.mycompany.com' # Change this to your domain.

    basePath: 'users' # This will be prefixed to all routes

    stage: ${self:provider.stage}

    createRoute53Record: true

In this case need to run serverless create_domain again. 
Since created the domain already, it's available for any services that want to use it.

Run sls deploy to deploy the users service and verify the browser 

# Multiple stages 

Assuming three stages:

- prod, which is accessible at api.mycompany.com;
- staging, which is accessible at staging-api.mycompany.com; and
- dev, which is accessible at dev-api.mycompany.co

For each of these domains need to get certification in Amazon Certificate Manager. 

To make this possible need to config the .yml file custom section 

custom:
  
stage: ${opt:stage, self:provider.stage}

  domains:

    prod: api.mycompany.com

    staging: staging-api.mycompany.com

    dev: dev-api.mycompany.com

  customDomain:
  
  basePath: ""

   
domainName: ${self:custom.domains.${self:custom.stage}}

    stage: "${self:custom.stage}"

    createRoute53Record: true+

For each stage a custom domain need to be created. 

$ sls create_domain --stage prod

$ sls create_domain --stage staging

$ sls create_domain --stage dev

deploy it 

## Certification  and Registering the domain with the AWS Certificate Manager

After creating a sls create_domain.

install the serverless-domain-manager plugin in each service.

plugins:
  
  serverless-domain-manager

custom:
  
customDomain:

    domainName: 'api.mycompany.com' # Change this domain.

    basePath: 'myprefix' # This will be prefixed to all routes

    stage: ${self:provider.stage}

    createRoute53Record: true

