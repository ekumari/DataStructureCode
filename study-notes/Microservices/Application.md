## Create Microservice Application Through SpringBoot

- @SpringBootApplication: Tells spring that it is springboot project
- Web as dependencies: Start Tomcat server

Movie Catalog Resource:
- An API at /catalog/{userid} that returns payload with list of movie details.
    - Create REST Resource MovieCatalogResource by @RestController
        - Mapping for List of Movie getCatalog(userId)

Movie Info Resources:
- An API at at /movies/{movieId} that returns payload with list of movie details.
    - Create REST Resource MovieInfoResource by @RestController
        - Mapping for List of Movie getMovieInfo(movieId)

Rating Data Resources:
- An API at at /rating/{movieId} that returns payload with list of movie details.
    - Create REST Resource MovieInfoResource by @RestController
        - Mapping for List of Movie getRating(movieId)

        
- Models
    - CatalogItem
        - name: String
        - desc: String
        - rating: int
    - Movie
        - name: String
        - movieId: String
    - Rating
        - movieId: String
        - rating: int

How to make REST call from your code?
- Using a REST Client
- SpringBoot comes with a client already - RestTemplate(Deprecated in SpringBoot 5)

Spring Framework 5 introduces WebClient, a component in the new Web Reactive framework that helps build reactive and non-blocking web applications

RestTemplate:
- Call an API and return an object
- But calls are synchronous
- Using web client, you can make these call to asynchronous