### Rest API


**REST** - Reprensentational State Transfer

*   Client sends the request and server returns the response in some format (JSON or XML)
*   We create object of values and return them then using some library in golang(respondWithJSON) or java, convert it to JSON or XML. This is called **State transfer** from object to some format.
*   In Javascript, we can directly create array object and send them it gets returned as JSON

In Spring Boot or JavaScript, response object gets converted to JSON automatically, you don't have to do anything. 

*   [Java] Spring MVC converts the response object to JSON.
*   [Java] Fact you annotated the class as REST Controller means that whatever you return that gets converted automaticlly to JSON and send back as in HTTP response.

REST is Stateless

#### Stateful - 

#### Stateless -