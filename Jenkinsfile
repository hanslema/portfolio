pipeline {
    agent any
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git CHeckout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'c0dace21-74d6-4fec-9846-e2049ef4a9e1', poll: false, url: 'https://github.com/hanslema/portfolio.git'
            }
        }
        stage('COMPILE') {
            steps {
                sh "mvn clean compile -DskipTests=true"
            }
        }
        stage('OWASP Scan') {
            steps {
                dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        stage('Sonarqube') {
            steps {
                withSonarQubeEnv('sonar-server'){
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=my-project \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=my-project '''
                }
            }
            
        }
        
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests=true"
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'aa97c91b-923b-4925-b818-deecd81ba2bb', toolName: 'docker') { 
                        sh "docker build -t my-project -f docker/Dockerfile ."
                        sh "docker tag my-project michy22/my-project:latest"
                        sh "docker push michy22/my-project:latest"
                    }
                }
            }
        }
        
        
    }
}
