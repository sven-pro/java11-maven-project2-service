
currentBuild.description = "branchName: ${env.branchName}"
pipeline {
	agent { label 'build01'}
	options { skipDefaultCheckout true }
	stages {
		stage("CheckOut"){
			steps {
				script{
					checkout([$class: 'GitSCM', 
							   branches: [[name: "${env.branchName}"]], 
							   extensions: [], 
							   userRemoteConfigs: [[
				   			   		credentialsId: '9d02cccf-5f45-46d6-b4e5-81ff97809c12', 
				   			   		url: "${env.srcUrl}"]]])

				}
			}
		}

		stage("Build"){
			steps {
				script{
					sh "mvn clean package -DskipTests"

				}
			}

		}

		stage("Test"){
			steps{
				script{
					sh "mvn test"

				}
			}
		}

		stage("sonar scann"){
			steps{
				script{
				echo "11111111"	
				echo "${env.branchName}"
				name1 = "${env.branchName}"
				println("${name1.size()}")
				echo "============+++++++++++++----------------------------"
				echo "${params.branchName}"
				name2 = "${params.branchName}"
				println("${name2.size()}")

					withSonarQubeEnv(credentialsId: 'b8a196d0-e69a-4728-abf5-402ecea4139a') {						
						sh """
							sonar-scanner \
							-Dsonar.login=${SONAR_AUTH_TOKEN} \
							-Dsonar.host.url=${SONAR_HOST_URL} \
							-Dsonar.branch.name=${env.branchName}							

						"""
					}
				}
			}

		}

	}
}
