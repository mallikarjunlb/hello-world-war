pipeline {
	agent none
	stages {
	    
       stage('checkout') {
	       agent { label 'jenki' }
            steps {
                sh 'sudo rm -rf hello-world-war'
	sh 'git clone https://github.com/mallikarjunlb/hello-world-war.git'	
              }
        }
	 stage('build') {
		 agent { label 'jenki' }
	
            steps {
                dir('hello-world-war'){
                  sh 'pwd'
                sh 'ls'
            
                sh 'docker build -t tomcat:ver1.1 .'  
			
                }
	    }
	 }
                stage('push') {
			agent { label 'jenki' }
	
            steps {
		    sh 'ls'
            sh 'docker tag tomcat:ver1.1 mallikarjun10/myrepo:ver1.0'
		    sh 'docker images'
                sh 'docker push mallikarjun10/myrepo:ver1.0'
         }
	 }
		 stage('deploy'){
		 agent { label 'test' }
	     steps{
	        sh 'docker rm -f mytomcat'
	         sh 'docker run -d --name mytomcat -p 7777:8080 mallikarjun10/myrepo:ver1.0'
	     }
	 }
	
    }
}
