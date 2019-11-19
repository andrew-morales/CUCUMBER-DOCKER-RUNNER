pipeline{
	agent any
	stages{
		stage("Pull Latest asmorales/cucumber-docker Image"){
			steps{
				sh "docker pull asmorales/cucumber-docker:latest"
			}
		}
		stage("Start Grid"){
			steps{
				sh "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run The Test"){
			steps{
				sh "docker-compose up bdd-tst"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: './target/test-output/**'
			sh "docker-compose down"
		}
	}
}