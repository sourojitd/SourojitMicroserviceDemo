# Springboot-Microservice
Springboot-Microservice


# Used Eureka as Service Registry
 Used Eureka to register the microservices at one place. Helps with the names inplace of target urls for service calls.

#Used API Gateway
 Spring boot actuator - Lets us manage the application
 Gateway - Routes traffic to APIs available (here to our user and department service
 
 #Used hysterisk circuit breaker in the gateway application
 Used hysterisk libraries to identify and let us know which services are not running (and also to redirect to fallback controller) 
 and then to display in the hysterisk dashboard.
 
 #Used Config Server as a microservice
 To load configurations of all the services from an external source. Highly used when we have a lot of microservices.
 Create a bootstrap.yml to load the cloud config first and then the app context from application.properties will be loaded.
 
 
# Used Zipkin and Sleuth for disctributed logging
Download the Zipkin Server and note down the port it is running on. Implement zipkin client and sleuth in all the microservices.
Gives trace Id (Same accross all services for a particular flow) and span Id as well as the name and export flag along with the logs.