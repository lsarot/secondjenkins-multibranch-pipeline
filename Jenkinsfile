/*
pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
}
*/
pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName:'sonarqube') {
                        sh 'mvn clean package sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}