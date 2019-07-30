pipeline {
    agent any

    stages {
        stage('Compile') {
          steps {
            // Compile the app and its dependencies
            sh './gradlew compileDebugSources'
          }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
                echo "Executed unit tests"
                junit '**/TEST-*.xml'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew assembleDebug'
                archiveArtifacts '**/*.apk'
                echo "The build stage passed..."
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
            mail to: 'satnam.malhotra@3pillarglobal.com', subject: 'New build available!', body: 'Check it out!'
            // Jenkins cleans the workspace
            cleanWs()
        }
    }
}