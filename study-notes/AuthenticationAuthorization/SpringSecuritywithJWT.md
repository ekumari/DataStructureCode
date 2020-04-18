## Overview of Security and Basic Auth and JWT

**Rest Service is not secure**
In Sping, Restful services -

*   spring-boot-starter-web
*   spring-boot-spring-security
Use Spring Security as dependency to support JWT or Basic Auth.

### Basic Auth

*   Sending username and password first to login
*   Sending username and password with every request is not safe as anyone can hack and get the credentials
*   Add userid and password in headers (Authorization) as **basic auth** that needs to send with every request
*   401 - unauthorized

Spring Boot Security  -

**WebSecurityConfigureAdaptor** is a class which contains default security configuration for spring security

*   It has configure method()
*   Extend WebSecurityConfigureAdaptor in custom class
* Override configure method
*   @Configuration(spring confuguration) ans @EnableWebSecurity(web security)

    
    ```
    public class YourCustomClassForSecurity extends WebSecurityConfigureAdaptor{
    void configure(HttpSecurity http) throws Exception
    {
        http.csrf().disable() //disable csrf
        .authorizeRequests()
        .anyMatcher(HttpMethod.OPTIONS,"/**").permitAll() // allow all request
        .anyRequest().authenticated().and().httpBasic();
    }
    } 
    ```

### CSRF: Cross site forgery request

### CORS: cross origin
No Access-Control-Allow-Origin header
Why CORS ?

*   When calling service from frontend app. is hosted on different server.
*   We need to tell spring boot to all request from different server.
@CrossOrigin - To allow request from other domain
```
@CrossOrigin(origins="http://localhost:4200") - enable cross origin
@RestController
@RequestMapping("/account")
public class AccountController {
 
    @CrossOrigin("http://example.com")
    @RequestMapping(method = RequestMethod.GET, "/{id}")
    public Account retrieve(@PathVariable Long id) {
        // ...
    }
 
    @RequestMapping(method = RequestMethod.DELETE, path = "/{id}")
    public void remove(@PathVariable Long id) {
        // ...
    }
}

```


### JWT: Json Web Token

*   Standard
*   Can contain User Details and Authorization
*   ACS in sofy-project as microservice.



