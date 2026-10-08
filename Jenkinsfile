pipeline {
    agent any

    tools {
        'hudson.plugins.sonar.SonarRunnerInstallation' 'sonar'
    }

    stages {
        stage('Checkout GitHub Repository') {
            steps {
                checkout scm
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonar'

                    withSonarQubeEnv('SonarQube') {
                        sh """
                            "\${scannerHome}/bin/sonar-scanner" \
                              -Dsonar.projectKey=mayavi-cloud-project \
                              -Dsonar.projectName=Mayavi \
                              -Dsonar.projectVersion=1.0 \
                              -Dsonar.sources=mayavi,tvtk \
                              -Dsonar.sourceEncoding=UTF-8
                        """
                    }
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
