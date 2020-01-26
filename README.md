# Docker image + container for ASP.NET Core web app  

Shows 2 options on how to use Dockerfile in a sample ASP.NET Core 2.1 web app

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

Since I wanted to create Windows container, I switched Docker desktop to Windows container. However, I think you can use Linux container too.

### Tip
No need to create Dockerfile on your own, you can create Dockerfile by navigating to WebApp folder / or folder where you have your .csproj file & then opening it in VS Code:
```
VS Code -> F1 -> Docker: Add Docker Files to Workspace... 
```
(you will get couple of options like Windows or Linux env, at the end it creates 'Dockerfile' for you!)

### Option 1

Docker file for WebApp with references to Class Libraries:
Use Dockerfile (webapp.Dockerfile) from aspnetcore-docker\src folder & run below below Docker commands

### Option 2

Docker file for WebApp with NO references to Class Libraries:
Comment out ClassLibrary1.csproj reference from src/WebApp/WebApp.csproj file & also comment out 2 lines having reference to ClassLibrary src/WebApp/Controllers/HomeController.cs. Use Dockerfile from aspnetcore-docker\src\WebApp\ folder & run below below Docker commands:

### Docker commands (used for above 2 options)

(1) Now create Docker image from Dockerfile:

(applicable for Option 1: run below command from folder: aspnetcore-docker\src)
```
docker build -t webapp:latest -f WebApp.dockerfile .
```
OR (applicable for Option 2: run below command from folder: aspnetcore-docker\src\WebApp)
```
docker build -t webapp:latest .
```
(1.1) If docker build is successfull, you should see docker image webapp:latest by running
```
docker images
```

(2) Create docker container from image:
```
docker run --name=webapp -d -p 8080:80 webapp
```
(2.1) If docker run is successfull, you should see docker container webapp by running:
```
docker ps
```

(3) Now you can get ip address of docker container:
```
docker inspect webapp
```
at the end, check IPAddress field

(4) Access webapp via (took couple of seconds for me, before you can access site) :
```
http://127.0.0.1:8080
```
OR
```
http://containerIPAddress
```

### Docker commands to cleanup

(1) Stop running docker container:
```
docker stop webapp
```

(2) Remove docker container:
```
docker rm webapp
```

(3) Remove docker image:
```
docker rmi webapp
```


## Result / Output

![Image of Result](https://github.com/abhishek-pradhan/aspnetcore-docker/blob/master/HelloWorld.PNG)

