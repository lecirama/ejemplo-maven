pipeline {
    agent any

    stages {
        
        stage('Compile_Code') {
            steps {
                        sh './mvnw clean compile -e'
                   }

        }
        
        stage('Test_Code') {
            steps {
                    sh './mvnw clean test -e'
                }
            }
        
        stage('Jar_Code') {
            steps {
                    sh './mvnw clean package -e'
            }
        }
        
	   stage('SonarQube analysis') {
   		 withSonarQubeEnv('sonar') { // You can override the credential to be used
      		 sh './mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    		}
  	     }
	    
        stage('Run_Jar') {
            steps {
                    sh 'nohup ./mvnw spring-boot:run &'
            }
        }

        stage('Testing_App') {
	           steps {
		          sleep 20
		          	   sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing'
	                }
             }
    }
   }
