### Docker

* Docker is an open-source centralized platform designed to create, deploy, and run applications.
* It packaged the software and resolve the dependency issue while installing in different platform.
* Docker uses container on the host's operating system to run applications
* Docker uses Host o.s
* Docker installs docker engine on host machine and deploy containers. Save Resources.  
* Components such as Docker client, Docker server, Docker machine, Docker hub, Docker composes

### Docker Containers
* Docker containers are light weight.
* It allows developers to package up the application with all its libraries and dependencies, and ship it as a single package.
*  Docker containers automatically generates storage and space according to the application requirement.

### Virtual Machine

*  Virtual Machine doesn't uses Host machine o.s, it creates guest o.s on top of Host machine.
* Wastage of memory

## Docker Java Application Example:

Java file:
```
    class Hello{  
    public static void main(String[] args){  
    System.out.println("This is java app \n by using Docker");  
    }  
    }  
```
Create Dockerfile for java file.
```
    FROM java:8  
    COPY . /var/www/java  
    WORKDIR /var/www/java  
    RUN javac Hello.java  
    CMD ["java", "Hello"]  or ENTRYPOINT [java -jar Hello.jar]

```
Either RUN javac Hello.java  
    CMD ["java", "Hello"]

OR

ENTRYPOINT [java -jar Hello.jar]

*Build Docker File*

```
$ docker build -t java-app .   
```

*Run Docker Image*
```
docker run java-app
```

*Docker commands* -

    docker images - view images
    docker ps - view containers