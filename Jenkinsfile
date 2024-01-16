pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Release LMS') {
            steps {
                script {
                    echo 'Releasing..'
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "Version: ${packageJSONVersion}"
                    sh "zip -r webapp/dist-${packageJSONVersion}.zip webapp/dist"
                    sh "curl -v -u admin:pradeep123 --upload-file webapp/dist-${packageJSONVersion}.zip http://18.117.169.38:8081/repository/lms/"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
