pipeline {
	agent any
	stages{
		stage('clone and clean repo'){
	

	           steps {
                cleanWs()
		       	bat "git clone -b master https://github.com/sadek-selmi/Devops.git"
		       			      dir("DevOps") {
		          	bat "mvn clean "
}

			 }

		}
		stage('Testing'){

		   steps{ 
		dir("DevOps") {
		   bat "mvn test -Dmaven.test.skip"
                        }
			}}
		stage('Deploy'){
		   steps {
         dir("DevOps") {
			bat "mvn package -Dmaven.test.skip"
         
  
			bat "mvn sonar:sonar -Dmaven.test.skip"

			bat "mvn deploy -Dmaven.test.skip"
       
		
}
	}
}
		stage('Docker'){
		   steps {
		dir("DevOps") {
			bat "docker build -t dev ."
			// 
			bat "docker tag dev  sadekselmi/devop:1"
			bat"docker login -u sadekselmi -p admin1234"
			bat "docker push  sadekselmi/devop:1"			
			
			
        }
        
    }}
        stage('email'){
            	           steps {

            mail bcc: '', body: 'Hello , this is a Pipeline DevOps', cc: '', from: '', replyTo: '', subject: 'DevOps Pipeline', to: 'selmisadekk@gmail.com'
    }}
    
}}
