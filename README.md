# React simple app

This repository is used for a CICD jenkins process to scan a react code and deploy an app in a K8S cluster. 

Jenkinsfile.groovy : File used for the jenkins pipeline , in this file you can find all the process. 
Dockerfile : File used to build the React image
simple-react-app-service.yml : Yaml file with the infrastructure definition to deploy in a K8S cluster. 

Some considerations: 
- You will need:
  - Jenkins installed
  - Docker
  - Kubectl
  - K8S cluster, if you want to work locally , you can use microk8s
  - To run the scan with SonarQube you will need the application running:  docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

Screenshots: 

Pipeline:

![image](https://user-images.githubusercontent.com/12170121/110133700-468bb880-7dd5-11eb-8594-d16aeb59b860.png)

Jenkins credentials:

![image](https://user-images.githubusercontent.com/12170121/110133788-64591d80-7dd5-11eb-8823-63480e012c27.png)

SonarQube:

![image](https://user-images.githubusercontent.com/12170121/110133958-90749e80-7dd5-11eb-80ee-1321b1857d21.png)

K8S:

![image](https://user-images.githubusercontent.com/12170121/110134093-b69a3e80-7dd5-11eb-99cf-7868abafe39b.png)

Dockerhub:

![image](https://user-images.githubusercontent.com/12170121/110134553-30322c80-7dd6-11eb-8f34-b4aec506e3de.png)


Application:

![image](https://user-images.githubusercontent.com/12170121/110133878-7a66de00-7dd5-11eb-9e6f-a8f671988c3a.png)

