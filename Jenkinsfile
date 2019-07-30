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
         // Cleaning workspace
            cleanWs()
        }
        success{
            mail to: 'satnam.malhotra@3pillarglobal.com', from: 'Jenkins_Build', subject: 'New build available!', body: <b>'Check it out!'</b><br> Project: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER} <br>
        }
        failure{
            mail to: 'satnam.malhotra@3pillarglobal.com', from: 'Jenkins_Build', subject: 'New build available!', body: <b>'Build failed'</b><br> Project: ${env.JOB_NAME} Build Number: ${env.BUILD_NUMBER} <br>
        }
    }
}