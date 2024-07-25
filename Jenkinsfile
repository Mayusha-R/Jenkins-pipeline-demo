pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'Maven-3.9.0'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Mayusha-R/Jenkins-pipeline-demo.git', branch: 'main', credentialsId: 'private-demo-cred'
            }
        }

        stage('Build') {
            steps {
                script {
                    withEnv(["PATH+MAVEN=${MAVEN_HOME}//bin"]) {
                        sh 'mvn clean install'
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    withEnv(["PATH+MAVEN=${MAVEN_HOME}//bin"]) {
                        sh 'mvn test'
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
