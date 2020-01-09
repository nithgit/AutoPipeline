
pipeline {
    agent any
    
    tools {
        maven 'localmaven'
    }
    
    parameters {
        string(name: 'tomcat_stg', defaultValue: 'localhost:8090', description: 'staging server')
        string(name: 'tomcat_prod', defaultValue: 'localhost:9090', description: 'production server')
    }

    triggers {
        pollSCM('* * * * *')
    }
    
    stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deployments') {
	    parallel{
	        stage ('Deploy to Staging'){
	            steps {
		        bat "cp **target/*.war /c/users/500983245/apache-tomcat-8.5.50-stg/webapps"
                    }
                }
	        stage ('Deploy to Production'){
                    steps {
		        bat "cp **target/*.war /c/users/500983245/apache-tomcat-8.5.50-prd/webapps"
		    }
                }
            }
        }
    }
}
