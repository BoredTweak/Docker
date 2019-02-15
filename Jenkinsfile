pipeline {
    agent any

	stages {
		stage ('Checkout') {
			steps {
				echo 'Checkout..'
				checkout scm
			}
		}
		stage ('Build & UnitTest') {
			steps {
				echo 'Build & UnitTest..'
				sh "docker build -t accountownerapp:B${BUILD_NUMBER} -f Dockerfile ."
				sh "docker build -t accountownerapp:test-B${BUILD_NUMBER} -f Dockerfile.Integration ."
			}
		}
		stage ('Integration Test') {
			steps {
				echo 'Integration Test..'
				sh "docker-compose -f docker-compose.integration.yml up --force-recreate --abort-on-container-exit"
				sh "docker-compose -f docker-compose.integration.yml down -v"
			}		
		}
    }
}