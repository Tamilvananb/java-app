pipeline {
    agent any
    stages {
        stage ('checkout') {
            steps {
		checkout scm
            }
        }
        stage ('Build') {
            steps {
		    sh '${m2_home}/usr/local/src/apache-maven/bin/mvn -f java-sample-app/pom.xml clean install' 
            }
        }
    	stage ('Deploy to tomcat') {
		steps {
			sshagent(['tomcat-dev']) {
            			sh 'scp -o StrictHostKeyChecking=no target/*.war root@192.168.1.104:/var/lib/tomcat/webapps/manager/'
			}
		}
	}
    }
}
