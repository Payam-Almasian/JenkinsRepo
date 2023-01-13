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
        always { 
            junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true)
        }
    }
    
}
