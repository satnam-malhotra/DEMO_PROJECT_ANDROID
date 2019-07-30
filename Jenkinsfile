pipeline {
    agent any

    stages {
        stage('Compile') {
          steps {
            // Compile the app and its dependencies
            sh './gradlew compileDebugSources'
            echo "Compile stage passed"
          }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
                echo "Test stage passed"
                junit '**/TEST-*.xml'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew assembleDebug'
                archiveArtifacts '**/*.apk'
                echo "Build stage passed"
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
            mail to: 'satnam.malhotra@3pillarglobal.com', from: 'Jenkins_Build', subject: 'New build available!', body: 'Check it out!'
            // Cleaning workspace
            cleanWs()
        }
    }
}