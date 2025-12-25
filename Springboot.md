Springboot

#Springboot

##### What are web services?

Set of open protocols and standards that allow data to be exchanged between different apps or systems.
Web services can be used by software programs written in a variety of programming languages.


##### Why is the common format necessary?

Client and server could be written in many different languages (Java, JavaScript and Python). Common format is needed to communicate between the client and server. (XML or JSON)


##### JSON (JavaScript Object Notation) & XML(Extensible Markup Language) format: Readable format for structuring data.

**To make a web service platform-independent, we make the request and response platform-independent**


##### Service Definition:

1) Request/Response Format: Defines the request format made by consumer and response format made by web service
2) Request Structure: Defines the structure of the request made by the application
3) Response Structure: Defines the structure of response returned by the web service -- what kind of response it gives back
4) Endpoint: Defines where the services are available -- addressable location where an API can be accessed to perform a particular function or retrieve specific data

##### SOAP vs RESTful Web Services

* REST (Representational State Transfer): Architecture Style | Uses Simple Http Protocol | Supports JSON,XML,YAML | Widely used
* SOAP (Service Oriented Architecture Protocol) : Protocol Style | Uses SOAP envelope then HTTP/FTP/SMTP | Only XML | Slower Performance


##### Requests & Responses

Request to a resource is identified by a URI = Unified Resource Identifier

Every resource is UL-addressable

To change a system state, simply change a resource


URI Example:

* http://localhost:9999/restapi/books/{id}

	- GET - get the book whose id is provided

	- PUT/PATCH - update the book whose id is provided

	- DELETE - delete the book whose id is provided

	- POST - send data to the web server


PUT request - update the whole thing

PATCH request - only certain attributes are updated


##### REST characteristics

- Client-Server Architecture (Improves portability and Scalability)
- Cacheability (Responses can be cached to be reused)
- Statelessness (Server does not need to store any client session)
- Layered System
- Uniform Interface


###### Resources

Application state and functionality are abstracted into resources

**URI:** Every resource is uniquely addressable using specific syntax

To make RESTful applications uniform: HTTPS methods and Status Quotes(2xx, 3xx, 4xx, 5xx)



##### How to make new Spring Application?

1) Google start.spring.io

2) Select Maven Project, Java Language and add dependencies Spring Web & Spring Boot Dev Tools
	-Additional Dependencies (Update pom.xml):
		- H2 Database
		- Spring Data JPA

3) Generate Zip File and extract the file

4) Import Maven Project

5) Search Maven Repository on Google and enter the website
	https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-starter-webmvc-ui/2.7.0

6) Copy and Paste the dependency on pom.xml (Make sure to restart server when modifying dependencies in pom.xml)

7) Intermediate Steps (Packages and Classes)
   -----------------------------------------
   1) com.tcs.object
	- ObjectApplication.java (To Run SpringBoot Application)
   2) com.tcs.object.controller
	- ObjectController.java (Mapping for Users/Swagger to make requests)
   3) com.tcs.object.service
	- ObjectService.java (Business Logic For Validation etc.)
   4) com.tcs.object.repository
	- ObjectRepository.java (Methods to access database)
   5) com.tcs.object.model
	- Object.java (POJO)
   6) com.tcs.object.exception
	- GlobalAdvice.java (Reference File to get Advice)
	- NoObjectFoundException.java (Exception that extends Runtime Exception)

8) http://localhost:8080/swagger-ui/index.html (Access Swagger UI to test the GET/POST/PUT/PATCH/DELETE Methods)

9) Go to src/main/resources/application.properties and enter "spring.datasource.url=jdbc:h2:mem:ProjectDB"
	and enter server.port=3000

10) http://localhost:8080/h2-console/login.jsp?jsessionid=557e0c43895e44b660e94ca4d8518f26 (Access H2-Console to View Tables in DB)
	- Update the JDBC URL (jdbc:h2:mem:ProjectDB)


##### Additional References

*Open Source CSS Templates - https://getbootstrap.com/

*VS Code Shortcut for HTML - https://docs.emmet.io/cheat-sheet/

https://developer.mozilla.org/en-US/

https://docs.spring.io/spring-boot/tutorial/

https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html
