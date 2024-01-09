/////////////////////////////////////////////// Scripted Pipeline ///////////////////////////////////////////////

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

/////////////////////////////////////////////// Declarative Pipeline ///////////////////////////////////////////////

// Declarative Pipeline Syntax - New Way
// stage blocks are optional ( not mandatory )
// Notice in a Declarative Pipeline after the BUILD - first thing will be Automatically Checkout SCM


pipeline {
	// agent any        
	// if we want to run a docker agent 
	agent { docker { image 'maven:3.9.6'} }		// It will pull the image from dockerhub and run it as a container and all the stages will run inside container.
	agent { docker {image 'node:18.18.2'} }
	stages {
		stage ('Build') {
			steps {
				// sh 'mvn --version'
				sh 'node --version'
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
		stage ('Final Test') {
			steps {
				echo "Final Test"
			}
		 } 		 
	}

	post {
		// AFTER ALL THE STAGES - WE CAN SAY WHAT TO DO IF ONE OF THE STAGES FAILS OR SUCCESS DO SOME THING etc. 
		// post build script help us in doing cleanups. 
		// 5 POST ACTIVITIES 
		always {
				echo 'I am awesome.. I run always'
			}
		success {
				echo 'I run when you are successful'
			}
		failure {
				echo 'I run when you are unsuccessful'
			}
		changed {
			echo 'I run when the status of the build changes - for example fail to success etc.'
		}	
		unstable {
			echo 'I run when a test failure happens'
		}
		}
}