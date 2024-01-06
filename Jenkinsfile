// Scripted Pipeline Syntax - Old way 
// node means machine where you run your pipeline
// stages will give you more visibility 
// In the Scripted pipeline stages are not mandatory

// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Integration Test"
// 	}
// }

///////////////////////////////////////////////

// Declarative Pipeline Syntax - New Way
// stage blocks are optional ( not mandatory )
// Notice in a Declarative Pipeline after the BUILD - first thing will be Automatically Checkout SCM


pipeline {
	agent any
	stages {
		stage ('Build') {
			steps {
				echo "Build"
			}
		}	
		stage ('Test') {
			steps {
				echo "Test"
			}
		}	
		stage ('Integration Test') {
			steps {
				echo "Integration Test"
			}
		 } 
	} post {
		// AFTER ALL THE STAGES - WE CAN SAY WHAT TO DO IF ONE OF THE STAGES FAILS OR SUCCESS DO SOME THING etc. 
			always {
				echo 'I am awesome.. I run always'
			}
			success {
				echo 'I run when you are successful'
			}
			failure {
				echo 'I run when you are unsuccessful'
			}
		}
}