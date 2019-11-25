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
			sh "sed -i '' 's///target//target//test-output/../g' target/test-output/sparkReport/index.html"
			//publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'target/test-output/sparkReport', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: 'Test Report'])
			archiveArtifacts artifacts: 'target/test-output/**'
			sh "docker-compose down"
		}
	}
}