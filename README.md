# React simple app

This repository is used for a CICD jenkins process to scan a react code and deploy an app in a K8S cluster. 

## About the process:
- Create a virtual machine and install Jenkins, Docker, and kubectl on it. 
- Crate a SonarQube container with SonarQube application. (Dashboard):  docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube 
- Create a Jenkins pipeline to:
  - Pull the React code from git repository. https://github.com/aditya-sridhar/simple-reactjs-app.
  - Create a SonarQube scanner container to scan the code and check quality and security.
  - Create an image from a Dockerfile. 
  - Upload the image to Docker Hub repository. https://hub.docker.com/u/gastonkanze
  - Create a deployment and deploy the image created on K8S. If you want to work locally with K8S you can use microk8s.

## Files:
- Jenkinsfile.groovy : File used for the jenkins pipeline , in this file you can find all the process. 
- Dockerfile : File used to build the React image
- simple-react-app-service.yml : Yaml file with the infrastructure definition to deploy in a K8S cluster. 

## Screenshots: 

###### Pipeline:

![image](https://user-images.githubusercontent.com/12170121/110133700-468bb880-7dd5-11eb-8594-d16aeb59b860.png)

###### Jenkins credentials:

![image](https://user-images.githubusercontent.com/12170121/110133788-64591d80-7dd5-11eb-8823-63480e012c27.png)

###### SonarQube:

![image](https://user-images.githubusercontent.com/12170121/110133958-90749e80-7dd5-11eb-80ee-1321b1857d21.png)

###### K8S:

![image](https://user-images.githubusercontent.com/12170121/110134093-b69a3e80-7dd5-11eb-99cf-7868abafe39b.png)

###### Dockerhub: 

![image](https://user-images.githubusercontent.com/12170121/110134553-30322c80-7dd6-11eb-8f34-b4aec506e3de.png)


###### Application:

![image](https://user-images.githubusercontent.com/12170121/110133878-7a66de00-7dd5-11eb-9e6f-a8f671988c3a.png)

