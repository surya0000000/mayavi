pipeline {
    agent any

    tools {
        sonarRunner 'SonarScanner'
    }

    stages {
        stage('Checkout GitHub Repository') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=mayavi-cloud-project \
                          -Dsonar.projectName=Mayavi \
                          -Dsonar.projectVersion=1.0 \
                          -Dsonar.sources=mayavi,tvtk \
                          -Dsonar.sourceEncoding=UTF-8 \
                          -Dsonar.host.url=$SONAR_HOST_URL
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Mayavi SonarQube analysis completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
