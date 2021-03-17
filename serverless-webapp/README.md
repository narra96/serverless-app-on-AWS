# SERVERLESS WEB APPLICATION 

***Serverless Computing*** allows to build and run application without provisioning , scaling and manging any servers.
Platforms handles the server completly with high availability that makes to focus on core product.

## Architecture

***insert image of system design and functionality***

1. **AWS S3 Bucket**   : It is simple storage service - html file is stored here  

2. **AWS API Gateway** : To expose the rest services to the outside world.
Authentication of the user , validating the input user passing to the API are performed here .

3. **AWS Lambda**	   : Actual serverless function where the business logic runs.
even based function that means it needs even to trigger, API Gateway is the one of the trigger for lamda to execute. 

4. **AWS DynamoDB**		: It is a NoSQL DB , where the data for the application is stored. 

## Working : 
When submit button is clicked after filling the Employee Web Application data .
It calls a POST API in API Gateway where the employee details are saved.
API gateway dont have any business logic it is created in lambda.
The POST API function triggers the AWS Lambda function where the business logic of API runs and connects to dynamoDB.
After storing our data in DynamoDB , and get data using email id of te employee.

## Build Process 
IAM user is used for better understanding of pocilies and permission throught the process.

**Step-1 :** Intially GET API is created in API Gateway and returns mock responce to check API Gateway working in appropriate way as designed.

**Step-2 :** After ensuring  API Gateway working properly, then API gateway is connected to lambda function . 
and then returns mock responce from lambda function and test again using POSTMAN.
 
**Step-3 :** After getting dat from lambda we create atable in DynamoDB and configure the sample data.

**Step-4 :** Lambda is connected to DynamoDB and test the API , now checks GET is working weither the data from DynamoDB is acquired or not. 
It is first API GET and later it is repeated for POST 

**Step-4 :** Once these three services are ready , now html file created is placed in AWS S3 which is connected to API Gateway.
This time instead of using POSTMAN here SUBMIT button is used and get the employee details. 

## Prerequisite : 

- AWS free tier account 
- Basic knowledge of the AWS service functionality 
- Basic knowledge of using POSTMAN 

## Implementations 

- API GATEWAY > New API > Add name and description of API 
- ACTION > Create Resource > Add resource name >check the enable API Gateway CORS

CORS (cross origin resource sharing )-it enables the access for connected from another domain.
Here it is enabled because in this project API is connected to S3 bucket which will be in different domains. 

After creating the resource 
- ACTION > Create Method 

All the possible http methods can be seen to perform the CRUD operations

>GET is selected > Integration type-Mock data is returned at first. 

Execution flow can be seen after creating to check the working functionality 
Select the >Integration responce > Body Mapping Templates >select the content type displayed 

Now generate the template existing or write a custom template (JSON) like below for verification :

{

"FirstName" : "Keerthi Reddy"

"LastName"  : "Narra"

"Email"     : "keerthireddynarra22@gmail.com"

}

Save it and need to deploy after any kind of modifications.

- To deploy >ACTION >Deploy API >Add stage name and description and deploy it 

URL can be seen - checked in postman when its directly checked missing authetication error token is seen because its a root URL need to add the get http method created.
URL/resourcename

- Lambda > Create function > Author from Scrach >function name >select role : 

Permissions based on role is selected.
Here instaed of creating any role - A role is created  in  IAM - for security purpose and attached policies as required full access to Lambda and DynamoDB. 

Now need to attach the role created to the lambda function.

> existing role - select the role created > create function 

Now the function is created and can see a sample function code . 
Now to check the lamda functionality mock JSON data is added to index.js file and connect the lambda to API. 

> Save and Test 

To connect one aws service with another ARN(Amazon Resource Name ) is required.
- copy the ARN from lambda function 

And deploy the API need to get the data from lamda not from the previous mock function. 

Delete the mock template created in API and then change the integration type as lambda and add the lamda created .Test in the postman. 



- Now to connect DynamoDB with Lambda 
>DynamoDB >create table >add table name and primary key >create 

Next need to add the sample data to test weither able to get data from DynamoDB.

After POST API is ready - then sends data from frontend to DynamoDB 

>create item >can see the partion key enter the value>
add other partion keys(+) >Insert> string type is used here >save 

Testing dynamo DB 

Need to add code to connect DynamoDB with Lambda Function. Need not install npm when code is written in lambda when it written outside npm is needed. Here amazon will takecare of the packages necessary. 

const AWS = require('aws-sdk'); 

//creating docclient

var docclient = new AWS.DynamoDB.DocumentClient();

var tableName ="CustomerDetails";

exports.handler =  (event, context, callback) => {

var params = {

    TableName : tableName,

    //key here should be exactly same as DynamoDB it is case sensitive

    Key:{

        "EmailID" :event.EmailID //data passing from json structucture is email id 

    }
}

//now created params  code docclient.get which will connect to dynamoDB will pass this API get function 

docclient.get(params, function(err,data)

{
     callback(err,data);  
})
   
 };

- >configure test events 
//added 

{
    
  "EmailID": "keerthireddynarra22@gmail.com"
  
}

- Now need to check from API Gateway>funtion created>get  

//can configure query string so that cannot accessed by others without this will get error back 

>GET >Method Request >URL Query String Parameters 

>add query string -here i am passing EmailID -enter okay and check required 

and now add  >Request Validator -Validate query string parameters and headers 

API template body mapping concept makes to map the body as wanted that is input parameter that is passing .

In this case Lambda function is expecting EmailID alone and user is sending the other data along with request can skip data and just pass EmailID is done here. 

>integration request  > mapping templates 

>when no no templates designed >application/json write json code

{
"EmailID" : "$input.params('EmailID')"
}

 >ACTION > deploy


 








## Future Scope


