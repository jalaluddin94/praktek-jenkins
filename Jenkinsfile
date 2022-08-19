pipeline {
    agent any
    tools{
        maven 'maven_3.8.6'
    }
	environment{
		LOCAL_IMAGE = 'student:latest'
		REPO_IMAGE = 'fajarstrtn/student:latest'
	}
    stages{
    	stage('environment'){
    	    steps{
    	        bat 'java -version'
    	        bat 'mvn -v'
    	        bat 'docker version'
    	    }
    	}
        stage('Build'){
            steps {
            	bat 'mvn clean compile install -Djasypt.encryptor.password=secret'
            }
        }
        stage('Test'){
            steps {
            	bat 'mvn test -Djasypt.encryptor.password=secret'
            }
        }
		
// 		stage('Deploy'){
//             steps {
// 				withCredentials([
//             		usernamePassword(credentialsId:'docker', usernameVariable:'username', passwordVariable:'password')
//             	]){
// 					bat 'mvn jib:dockerBuild'
// 					bat 'docker tag ${LOCAL_IMAGE} ${REPO_IMAGE}'
// 					bat 'docker push ${REPO_IMAGE}'
// 					bat 'docker rmi ${REPO_IMAGE}'
// 				}
//             }
//         }
    }
}
