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
	agent any
	environment {    // GO INSIDE Manage Jenkins and get the names of both tools we set earlier (myDocker & myMaven)
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH =  "$dockerHome/bin:$mavenHome/bin:$PATH"      // add both tools to our path
	}   
	// if we want to run a docker agent 
	// agent { docker { image 'maven:3.9.6'} }		// It will pull the image from dockerhub and run it as a container and all the stages will run inside container.
	// agent { docker { image 'node:21-bullseye-slim'} }
	stages {

		// CHECKOUT IS AUTOMATIC - HERE WE CAN JUST PRINT THE USEFUL INFORMATION
		stage ('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				// sh 'node --version'
				echo "Build"
				echo "Path - $PATH"		                  // Jenkins agent path
				echo "Build Number - $env.BUILD_NUMBER"   // The current build number
				echo "Build ID - $env.BUILD_ID"			  // The current build ID
				echo "Job Name - $env.JOB_NAME"           // Name of the project of this build
				echo "Build Tag - $env.BUILD_TAG"		  // String of "jenkins-${JOB_NAME}-${BUILD_NUMBER}". All forward slashes ("/") in the JOB_NAME are replaced with dashes ("-"). Convenient to put into a resource file, a jar file, etc for easier identification.
			    echo "Build URL - $env.BUILD_URL"
			}
		}	

        // COMPILE THE JAVA CODE
		stage ('Compile') {
			steps {
				sh "mvn clean compile"	//Its download all the dependencies and also compile the java code (its same like npm instll)
			}
		}	

        // // UNIT TESTS
		// stage ('Test') {
		// 	steps {
		// 		//echo "Test"
		// 		sh "mvn test"		// it will run the unit tests located inside directory => cd src/test/java/com/in28minutes/microservices/currencyexchangeservice/resource/CurrencyExchangeControllerTest.java
		// 	}
		// }	
		
		// // INTEGRATION TESTS USING CUCUMBER
		// stage ('Integration Test') {
		// 	steps {
		// 		// echo "Integration Test"
		// 		sh "mvn failsafe:integration-test failsafe:verify"		// it will run the integration tests using cucumber located inside directory => cd src/test/java/com/in28minutes/microservices/currencyexchangeservice/cucumber/
		// 	}
		//  } 

        // CREATE A JAR FILE
		stage ('Package'){
			steps {
				sh "mvn package -DskipTests"                    // -DskipTests MEANS SKIP THE UNIT AND INTEGRATION TESTS
			}
		}

        // BUILD A DOCKER IMAGE
		stage ('Build Docker Image'){
			steps {
				// "docker build -t devopstech24/jenkins-devops-microservice:$env.BUILD_TAG"      // Primitive (OLD) Way
				script {
					dockerImage = docker.build("devopstech24/jenkins-devops-microservice:${env.BUILD_TAG}")
				}
			}
		}

        // PUSH THE DOCKER IMAGE
		stage ('Push Docker Image') {
			steps {
				script {         
					// to push the image to docker hub we need to put the wrapper (docker.withRegistry) around below (dockerImage.push)
					docker.withRegistry('','dockerhubID') {        // first parameter is empty because dockerhub is a default docker registry // second paramter is docker credentials ID that we just created
					    dockerImage.push();
					    dockerImage.push('latest');   // We can't push without Jenkins having Docker Hub Credentials (DockerID and Password)
					} // end of wrapper
				}
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