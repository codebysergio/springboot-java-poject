pipeline {   
    agent any 
    tools{
        jdk 'jdk11'
        maven 'maven3'
    }

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/codebysergio/springboot-java-poject.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
                 }
        }
        
        stage('Package') {
            steps {
                sh "mvn clean package"
                
                 }
        }
        
        stage('Dependecny-check') {
            steps {
                dependencyCheck additionalArguments: '--scan target/', odcInstallation: 'owasp' 
                     dependencyCheckPublisher pattern: '**/dependency-check-report xm1'
            }
        } 
        
        stage('Tomcat Deploy') {
            steps {
                sh "sudo cp target/spring-boot-web.jar /opt/apache-tomcat-9.0.65/webapps"
        
            }        
        }
    }
} 
