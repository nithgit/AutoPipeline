
pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean TestPipeline'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
