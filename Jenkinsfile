pipeline{
    agent any
    environment {
        SONAR_HOME= tool "sonar"
    }
    
    stages{
        
        stage("Clonning code from the GitHub"){
            steps{
              git branch: 'ci_cd_sec', url: 'https://github.com/sid14581/wanderlust.git'
            }
        }
        
        stage("SonarQube Quality Analaysis "){
            steps{
              withSonarQubeEnv("sonar"){
                sh "$SONAR_HOME/bin/sonar-scanner -Dsonar.projectName=wanderlust -Dsonar.projectKey=wanderlust"
              }
            }
        }
        
        stage("OWASP Dependency Check"){
            steps{
             dependencyCheck additionalArguments: '--scan ./', odcInstallation: 'dc'
             dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
        
        
        stage("Quality Gate Scan"){
            steps{
              timeout(time: 2, unit: "MINUTES"){
                 waitForQualityGate abortPipeline: false
              }
            }
        }
        
        stage("Trivy File System Scan"){
            steps{
             sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
        
        
        stage("Deploying code using docker-compose"){
            steps{
             sh "docker-compose up -d --build"
            }
        }
        
        
        
    }
}
