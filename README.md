# aspnetcore-docker
Shows 2 options on how to use Dockerfile in a sample ASP.NET Core 2.1 web app

Pre-Requesite: since I wanted to create Windows container, I switched Docker desktop to Windows container.
Created Dockerfile by navigating to WebApp folder & then opening it in VS Code -> F1 -> Docker: Add File... -> Windows env

(1) Docker file for WebApp with references to Class Libraries:
Use Dockerfile (webapp.Dockerfile) from aspnetcore-docker\src folder & run below below Docker commands

(2) Docker file for WebApp with NO references to Class Libraries:
Comment out ClassLibrary1.csproj reference from src/WebApp/WebApp.csproj file & also comment out 2 lines having reference to ClassLibrary src/WebApp/Controllers/HomeController.cs
Use Dockerfile from aspnetcore-docker\src\WebApp\ folder & run below below Docker commands


Docker commands used for above 2 options: 
(1) Now create Docker image from Dockerfile:
$ docker build -t webapp:v1 .
OR (if some different docker file name)
$ docker build -t webapp:v1 -f WebApp.dockerfile .

(2) Create docker container from image:
$ docker run --name=webapp -d -p 8080:80 webapp:v1

(3) Now you can get ip address of docker container:
$ docker inspect webapp ----> at the end, check IPAddress field

Access webapp via (takes couple of seconds before you can access site) : http://127.0.0.1:8080 OR http://containerIPAddress
