# REAL TIME -  USE CASE

## user registration process. 

Assuming  that  user opens the phone, 
downloads the application and 
wants to test it for the first time.

 The client application would contact its back-end as follows:
   
    1. The user opens the homepage of the application, which displays the latest jobs. The jobs component is served by two replicas behind a load balancer.

    2. The user needs to search for a suitable job. Only registered users can do that, so the jobs component redirects the client to the registration component.

    3. The registration service is handled by two application instances behind a load balancer. The user enters her information and credentials. The client posts the data to the registration service.

    4. The registration service stores the data to a stateful component that saves the user information and redirects the user to the login page (the login app).

    5. The user supplies the newly created credentials to the login app, the login app creates an authentication token and stores it on another stateful service.

    6. Finally, the login app redirects the user to the home page where she can search for jobs.
