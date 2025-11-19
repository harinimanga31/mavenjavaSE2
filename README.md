this is a maven java project
checking webhook.

checking for auto build trigger on commit


code == 
***************************
pipeline {
    agent any

    environment {
        // Set JAVA_HOME if needed
        JAVA_HOME = "C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.17.10-hotspot"
        PATH = "${env.JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bommidivyshnavi/MavenJavaDemo.git'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
                bat "mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                bat "mvn test"
            }
        }
    }

    post {
        always {
            echo "Build finished"
        }
        success {
            echo "Build and tests succeeded!"
        }
        failure {
            echo "Build or tests failed!"
        }
    }
}


*********************************************************
FROM tomcat:9.0

# Remove default webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy your WAR file to Tomcat webapps as ROOT.war
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

# Correct Tomcat startup command
CMD ["catalina.sh", "run"]
////////////////////////////////////////////////////////////
FROM tomcat:9-jdk11
COPY target/*.war /usr/local/tomcat/webapps
///////
FROM nginx:alpine
COPY . /usr/share/nginx/html
///////
sudo docker run -d -p 9090:8080 mavenproj
/////////
minikube start --driver=docker

minikube status
minikube kubectl -- get pods -A
minikube dashboard
minikube version
minikube logs
minikube update-check
minikube update
kubectl create deployment mynginx --image=nginx
kubectl set image deployment/mynginx nginx=nginx:latest
kubectl get deployments
kubectl get pods
kubectl describe pods
kubectl expose deployment mynginx --type=NodePort --port=80 --target-port=80
kubectl get service mynginx
kubectl scale deployment mynginx --replicas=4
kubectl port-forward svc/mynginx 8081:80
minikube tunnel
minikube service mynginx --url
kubectl delete deployment mynginx
kubectl delete service mynginx
minikube stop
minikube delete
docker pull jasonrivers/nagios:latest
docker run --name nagiosdemo -p 8888:80 jasonrivers/nagios:latest
docker stop nagiosdemo
docker rm nagiosdemo
docker images

docker rmi jasonrivers/nagios:latest
/////////////////////////////////////




