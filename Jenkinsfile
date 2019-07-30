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

    environment {
                EMAIL_TO = 'satnam.malhotra@3pillarglobal.com'
    }

    post{
        always{
         // Cleaning workspace
            cleanWs()
        }
        success{
            mail to: EMAIL_TO, from: 'Jenkins_Build',
            subject: 'Build passed in Jenkins: env.BUILD_NUMBER',
            body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}'
        }
        failure{
           mail to: EMAIL_TO, from: 'Jenkins_Build',
           subject: 'Build failed in Jenkins: env.BUILD_NUMBER',
           body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}'
       }
    }
}