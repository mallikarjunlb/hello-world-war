pipeline {
	agent none
	stages {
	    
       stage('checkout') {
	       agent { label 'jenki' }
            steps {
                sh 'sudo rm -rf hello-world-war'
	sh 'git clone https://github.com/Urssharath/hello-world-war.git'	
              }
        }
	 stage('build') {
		 agent { label 'jenki' }
	
            steps {
                dir('hello-world-war'){
                  sh 'pwd'
                sh 'ls'
            
                sh 'docker build -t tomcat:${BUILD_NUMBER} .'  
			
                }
	    }
	 }
                stage('push') {
			agent { label 'jenki' }
	
            steps {
		    sh 'ls'
            sh 'docker tag tomcat:${BUILD_NUMBER} urssharath/myrepo:${BUILD_NUMBER}'
		    sh 'docker images'
                sh 'docker push urssharath/myrepo:${BUILD_NUMBER}'
         }
	 }
		 stage('deploy'){
		 agent { label 'test' }
	     steps{
	        sh 'docker rm -f mytomcat'
	         sh 'docker run -d --name mytomcat -p 7777:8080 urssharath/myrepo:${BUILD_NUMBER}'
	     }
	 }
	
    }
}
