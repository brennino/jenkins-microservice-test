
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
    agent any
    stages{
        stage('Build') {
            steps{
               echo "Build"
            }
        }
        stage('Test') {
           steps{
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
    }
}