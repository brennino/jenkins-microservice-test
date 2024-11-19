
/*SCRIPTED PIPELINE
node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Test"
	}
}
*/

//DECLATATIVE PIPELINE
pipeline{
   // agent{ docker{ image 'maven:3.6.3' } }
    agent any
    environment{
        dockerHome = tool 'myDocker'
        mavenHome  = tool 'myMaven'
        JAVA_HOME = tool 'myJdk'
        PATH = "$dockerHome/bin:$mavenHome/bin:$JAVA_HOME/bin:$PATH"
    }
    stages{
        stage('Checkout and environment variables print') {
            steps{
               echo "Build"
               echo "BUILD PATH: $PATH"
               echo "BUILD NUMBER: $env.BUILD_NUMBER"
               echo "BUILD ID: $env.BUILD_ID"
               echo "JOB NAME: $env.JOB_NAME"
               echo "BUILD TAG: $env.BUILD_TAG"
               echo "BUILD URL: $env.BUILD_URL"
               sh "mvn --version"
               sh "docker version"
            }
       }
       stage('Compile') {
          steps{
              sh "mvn clean compile"
          }
       }
        stage('Test') {
           steps{
               sh "mvn test"
           }
        }
        stage('Integration Test') {
           steps{
               sh "mvn failsafe:integration-test failsafe:verify"
           }
        }
        stage('Package') {
           steps{
               sh "mvn package -DskipTests"
           }
        }

        stage('Build Docker image') {
           steps{
              //docker build -t "brennino/currency-exchange-devops-example:$env.BUILD_TAG"
              script{
                dockerImage = docker.build("brennino/currency-exchange-devops-example:${env.BUILD_TAG}")
              }
           }
        }
        stage('Push Docker image') {
           steps{
               script{
                    docker.withRegistry('','dockerhub'){
                        dockerImage.push();
                        dockerImage.push('latest');

                    }
               }
           }
        }
     }

    post{
        always {
            echo "I am awesome, I always run"
        }
        success {
            echo "I run on success"
        }
        failure{
            echo "I run on failure"
        }
        //changed{
        //   changed status run when going from a failure build to a sucecessful one and vice versa
        //}
    }
}