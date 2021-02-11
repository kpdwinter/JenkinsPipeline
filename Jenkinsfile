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
            emailext body: "Jenkins job success. Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]' completed OK.",
                    subject: 'Jenkins CI job successfull',
                    to: 'kpdwinter@hotmail.com',
                    attachmentsPattern: '**/junitReportFile.html'
        }
        failure {
            echo 'Jenkins job failure - sending email notification.'
            emailext body: "Jenkins job failure. Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]' failure.",
                    subject: 'Jenkins CI job failure',
                    to: 'kpdwinter@hotmail.com'
        }
        unstable {
            echo 'Jenkins job unstable - sending email notification.'
            emailext body: "Jenkins job unstable. Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]'unstable.",
                    subject: 'Jenkins CI job unstable',
                    to: 'kpdwinter@hotmail.com'
        }
        changed {
            echo 'Jenkins job changed - sending email notification.'
            emailext body: "Jenkins job changed. Job '${env.JOB_NAME}[${env.BUILD_NUMBER}]'changed.",
                    subject: 'Jenkins CI job changed',
                    to: 'kpdwinter@hotmail.com'

        }
    }
}