
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
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }
    stages{
        stage('Build') {
            steps{
               echo "Build"
               echo "BUILD PATH: $PATH"
               echo "BUILD NUMBER: $env.BUILD_NUMBER"
               echo "BUILD ID: $env.BUILD_ID"
               echo "JOB NAME: $env.JOB_NAME"
               echo "BUILD TAG: $env.BUILD_TAG"
               echo "BUILD URL: $env.BUILD_URL"
            }
        }
        stage('Test') {
           steps{
               sh "mvn --version"
               sh "docker version"
               echo "Test"
           }
        }
        stage('Integration Test') {
           steps{
               echo "Integration Test"
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