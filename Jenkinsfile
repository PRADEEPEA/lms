pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'Analyze Code..'
		sh 'cd webapp && sudo docker container run --rm -e SONAR_HOST_URL="http://18.217.140.118:9000" -e SONAR_LOGIN="sqp_5a374423f9a6937d9d3913b8d392248f94e4a6da" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
