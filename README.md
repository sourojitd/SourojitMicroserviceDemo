# Springboot-Microservice
A full fledged Springboot Microservice


# Used Eureka as Service Registry
 Used Eureka to register the microservices at one place. Helps with the names inplace of target urls for service calls.

# Used API Gateway
 Spring boot actuator - Lets us manage the application
 Gateway - Routes traffic to APIs available (here to our user and department service
 
# Used Hystrix circuit breaker in the gateway application
 Used hystrix libraries to identify and let us know which services are not running (and also to redirect to fallback controller) 
 and then to display in the hystrix dashboard.
 
# Used Config Server
 To load configurations of all the services from an external source. Highly used when we have a lot of microservices.
 Create a bootstrap.yml to load the cloud config first and then the app context from application.properties will be loaded.
 
 
# Used Zipkin and Sleuth for distributed logging
Download the Zipkin Server and note down the port it is running on. Implement zipkin client and sleuth in all the microservices.
Gives trace Id (Same accross all services for a particular flow) and span Id as well as the name and export flag along with the logs.


# Steps:

1. Create the Microservices you want.
2. Ensure that the API/service calls are getting proper response
3. Now, we need a service registry to register the services so that each service can talk to one another via service names.(No need of hostname and port).
   Basically we get to manage all our services from this common endpoint. We use Eureka for this purpose.
   
   Eureka Server is an application that holds the information about all client-service applications. 
   Every Micro service will register into the Eureka server and Eureka server knows all the client applications running on each port and IP address. 
   Eureka Server is also known as Discovery Server.
   
4. Once our service registry is up, our services can talk to each other by service names. Now we need an API gateway. How it helps?
   By using the api gateway we eliminate the need to give address/port specific to the service to which we are talking to.
   For example: If we need users, we will use port 9003/users/{id}, but if we need department we will use 9002/departments/{id}.
   But if we have a API gateway, we can use a common port and all our traffic will pass through it.
   We can also add different firewalls etc in the gateway and manage the traffic as per our wants.
   Here, we also use Spring Cloud Hoxton as the load balancer.
   
5. Once all these are done, we now need monitoring tools for our application and services.
   We use Hystrix circuit breaker to identify and let us know which services are not running (and also to redirect to fallback controller).
   We can also visualize this using hystrix dashboard. (We need to get the hystrix.stream from the api gateway and we can get all the details of the services.
   
   Hystrix is watching methods for failing calls to related services. If there is such a failure, it will open the circuit and forward the call to a fallback method.
   Beyond that, it leaves the circuit open.
   
6. Once the service check an dfallback methods are setup, we use a cloud config server to setup our common configurations in the cloud at one place. 
   So that we don't need to change the configs everywhere when needed.
   We use Spring Cloud config server for this purpose.
   
   Spring Cloud Config provides server-side and client-side support for externalized configuration in a distributed system. 
   With the Config Server, you have a central place to manage external properties for applications across all environments.
   
7. Finally we use zipkin and sleuth for distributed logging.
   We get a trace id and span id which are of relevance to trace a particular call and to check which service it uses respectively.
   
   A trace represents the whole journey of a request, and a span is each individual hop along the way, each request. Spans may contain tags, or metadata, that can be used to later contextualize the request. 
   
   Spring Cloud Sleuth is used to generate and attach the trace id, span id to the logs so that these can then be used by tools like Zipkin and ELK for storage and analysis. 
   Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in service architectures.