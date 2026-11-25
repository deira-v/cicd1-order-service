OrderService

Port: 8082

Catalog Repo: https://github.com/deira-v/cicd1-catalog-service

Endpoints: localhost:8082/swagger-ui/index.html 


* productId refers to a product owned by Catalog, no network call exists yet.

## **Lab 7**  
* Maven package must run before docker build because the Dockerfile expects the .jar file to already exist.  
* A Docker Image is a packaged, read-only template containing everything your application needs to run.  
A Container is a running instance of a Docker image that provides an isolated environment for the application.
* 8082:8082 is a Docker port mapping. It connects port 8082 on Windows (host) to port 8082 inside the container.  
EXPOSE 8082 alone does not make it accessible from Windows.
* A Feign request to localhost:8081 fails because localhost refers to the Order container itself, not the Catalog container. The Catalog service name should be used instead, e.g. http://catalog:8081.
* The Catalog Product survived because the data was stored in persistent storage, such as a Docker volume, which is not removed by docker compose down by default. 
With an in-memory H2 database, the data would be lost when the application stops.

![Catalog and Order Docker images](images/docker-images.png)

