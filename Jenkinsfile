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

	  }
	}