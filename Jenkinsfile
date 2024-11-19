
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
    agent{ docker{ image 'maven:3.6.3' } }
    stages{
        stage('Build') {
            steps{
               echo "Build"
            }
        }
        stage('Test') {
           steps{
               sh "mvn --version"
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