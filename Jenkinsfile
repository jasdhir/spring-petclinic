pipeline {
    agent any
	//triggers {pollSCM('* * * * *')}
     stages {
          stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/jasdhir/spring-petclinic.git'
            }
          }
        stage('Build') {
            steps {
                     sh 'chmod a+x mvnw'
                      sh './mvnw clean package'
            }

          post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                always {
                   // junit '*target/surefire-reports/*.xml'
                    junit allowEmptyResults: true, testResults: '*target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
              //  }
				//changed{
				//	emailext attachLog: true, body: 'Please go to ${BUILD_URL} and verify the build',
				//	compressLog: true, to: "test@jenkins", recipientProviders: [upstreamDevelopers(),requestor()],
				//	subject: 'Job ${JOB_NAME}(${BUILD_NUMBER}) is waiting  input'
				}
            }
        }
    }
}

