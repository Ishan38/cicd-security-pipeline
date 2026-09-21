pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building CI/CD Security Pipeline..."'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t cicd-security-app:jenkins .'
            }
        }

        stage('Docker Push to Nexus') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'nexus-credentials',
                    usernameVariable: 'NEXUS_USER',
                    passwordVariable: 'NEXUS_PASS'
                )]) {
                    sh '''
                        echo "$NEXUS_PASS" | docker login nexus:8082 -u "$NEXUS_USER" --password-stdin
                        docker tag cicd-security-app:jenkins nexus:8082/cicd-security-app:jenkins
                        docker push nexus:8082/cicd-security-app:jenkins
                        docker logout nexus:8082
                    '''
                }
            }
        }
    }
}
