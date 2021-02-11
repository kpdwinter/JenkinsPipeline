pipeline {
    agent { label 'master' }
    stages {
        stage('Jenkins: Unit Tests') {
            steps {
                sh 'mvn verify -DskipITs=true'
            }
        }
        stage('Jenkins: Integration Tests') {
            steps {
                sh 'mvn verify -DskipUTs=true'
            }
        }
    }
    post {
        always {
            echo 'Cucumber reports...'
//          cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
        }
        success {
            echo 'Jenkins job successful - sending email notification.'
            emailext body: "Jenkins job success. Job '${env.JOB_NAME}' completed OK.",
                    subject: 'Test failed',
                    to: 'kpdwinter@hotmail.com'
        }
    }
}