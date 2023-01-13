pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        
        stage('checkout')
        {
            steps{
                git 'https://github.com/Payam-Almasian/JenkinsRepo.git'
                sh "ls -lah"
                sh "whoami"

            }
        }
        stage('build') { 
            steps { 
                sh(script: 'docker build -t appjs .')
            }
        }
        
        stage('deploy') {
            when { branch "master" }
            steps { 
                sh(script: 'docker run -d -p 3000:3000 appjs')
            }
        }


    }
    post { 
        failure { 
            mail bcc: '', body: "<b>Test</b><br>\n</br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "ERROR CI: Project name -> ${env.JOB_NAME}", to: "foo@foomail.com";
        }
    }
    
}
