pipeline {
    agent any
    tools{
        jdk 'jdk17'
        maven 'maven'
        
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'f54ed9bf-d547-4de6-bc24-5aa5d14e7ba2', poll: false, url: 'https://github.com/kaushal78038/Ekart.git'
            }
        }
        
        stage('Maven Complie') {
            steps {
                sh "mvn clean compile -DskipTests=true "
            }
        }
        
        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern:'**/dependency-check-report.xml' 
            }
        }
        
        stage('Maven Build') {
            steps {
                sh "mvn clean package -DskipTests=true "
            }
        }
        
        
    }
    
}
