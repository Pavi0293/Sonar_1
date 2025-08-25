    pipeline {
        agent any
        stages {
            stage('Build and SonarQube Analysis') {
                steps {
                    script {
                        withSonarQubeEnv('SonarQube') { // Use the name configured in Jenkins
                            // Example for Maven project
                            sh 'mvn clean package sonar:sonar -Dsonar.projectKey=your_project_key -Dsonar.host.url=http://13.51.178.104:9000/ -Dsonar.login=sqa_5ddd2717d8a553f10d3b6a5b9e97270ac728a3a0' 
                            // Adjust the command based on your build tool (e.g., Gradle, Ant) and project setup
                        }
                    }
                }
            }
           stage('Quality Gate Check') {
    steps {
        retry(3) { // Retry the entire block up to 3 times
            timeout(time: 15, unit: 'MINUTES') { // Keep the timeout
                waitForQualityGate abortPipeline: true
            }
        }
    }
}
        }
    }
