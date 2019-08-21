pipeline {
    /* insert Declarative Pipeline here */
   agent { node {label 'qa'}}
   stages {
        stage('Build') {
            steps {
                sh 'composer install'
            }
        }
        stage('Test') {
            steps {
                sh 'vendor/bin/phpunit'
            }
    post {
       failure {
             emailext(
                 subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                 body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
                 recipientProviders: [[$class: 'DevelopersRecipientProvider'],
                 [$class: 'RequesterRecipientProvider']]
             )
       }
       success {
             emailext(
                 subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
                 body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
                 to: "jackson@schoolofnet.com"
             )     
            }     /*emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'*/
        }
    }
        }    
        }