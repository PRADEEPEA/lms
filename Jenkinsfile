pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'Analyze Code..'
		sh 'cd webapp && sudo docker container run --rm -e SONAR_HOST_URL="http://3.19.67.247:9000" -e SONAR_LOGIN="sqp_5a374423f9a6937d9d3913b8d392248f94e4a6da" -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
		sh 'cd webapp && npm install && npm run build'
            }
        }

	 stage('Release LMS') {
	    steps {
	        script {
		    echo "Releasing.."
		    def packageJSON = readJSON file: 'webapp/package.json'
		    def packageJSONVersion = packageJSON.version
		    echo "${packageJSONVersion}"
		    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
		    sh "curl -v -u admin:pradeep123 --upload-file dist-${packageJSONVersion}.zip http://3.19.67.247:8081/repository/lms/"
            }
	}    

        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
