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
                publishHTML([allowMissing: false,
                          alwaysLinkToLastBuild: false,
                          keepAll: false,
                          reportDir: '',
                          reportFiles: 'app/build/reports/tests/**/index.html',
                          reportName: 'HTML Report',
                          reportTitles: 'UT report'])
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
                echo 'Deploying...'
            }
        }
    }

    environment {
                EMAIL_TO = 'satnam.malhotra@3pillarglobal.com'
    }

    post{
        always{
         // Cleaning workspace
         deleteDir()
        }
        success{
            echo env.BUILD_NUMBER
            mail to: EMAIL_TO, from: 'Jenkins_Build',
            subject: 'Build passed in Jenkins:',
            body: 'Check console output'
        }
        failure{
           echo env.BUILD_NUMBER
           mail to: EMAIL_TO, from: 'Jenkins_Build',
           subject: 'Build failed in Jenkins:',
           body: 'Check console output'
       }

    }
}