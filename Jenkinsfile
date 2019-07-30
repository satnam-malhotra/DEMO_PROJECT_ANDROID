pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './gradlew assembleDebug'
                archiveArtifacts '**/*.apk'
                echo "The build stage passed..."
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
    post{
        always{
            echo "post-build will always run after build completed"
            // Jenkins cleans the workspace
            //cleanWs()
        }
    }
}