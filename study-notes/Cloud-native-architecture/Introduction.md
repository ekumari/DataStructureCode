## Cloud-Native Architecture:

**Project**: 

*   My project is based on cloud-native architecture and it follows Software as a service (SAAS cloud model) where you don't have to worried about how backend is working, where it is deployed, how much resources allocated..etc. End users can simply use the services.

Benefit of SAAS:

*   Need high speed internet to utilize the software
*   No need to install on personal computer
*   No need to maintain, cloud provider will take care of maintaince, and any issue related to software.
*   Platform independent   

Real Life Example of SAAS: Online Food Order 

*   Don't know who is cooking and taking order and who is delivery boy?

**Architecture of Project**:
```
    cloud
    {   
        common service
            - Authentication & Authorization
            - Monitoring
            - Billing
        Meeting App{.. Rest API..}
    }
```
### SofyACS: Sofy Access Control Service
Contains:-

*   Ambassador
*   Keyclock(Generate jwt token)
*   Authentication and Authorization by Keyclock
*   API Security

Sofy has micro-services, cloud-native architecture.

### Cloud Importance

1. Old Web Application: (Monolithic)Layered Structured 
    - Web -> Business -> Data layer
    - Model/View/Controller

    Techology: Jsp/Servlet, Spring MVC

2.  Web Services: Provide service over web
    - SOAP: wsdl/ Service oriented architecture
    - REST: swagger ui

3. Microservices:
    - Having multiple service
    - Easy to integrate with other services
    - Instead of having everything in one project, we can create multiple service like authentication/authorization, analytics etc which can plug to any other project.
    - Maintaince is the big headache as we have to maintain all these services

4. Cloud:   
    -   In microservices, we had face maintaince problem of all the services. So to handle that issuse, cloud comes into picture.
        - On-Demand provision of resources(AWS/GCP)
        - Infrasture
        - Auto-scaling etc
        - Load Balancing
        - Restart machanisms in case of failure.



