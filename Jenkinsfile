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
                sh(script: './mvnw --batch-mode package -DskipTests')
            }
        }


    }
    post { 
        always { 
            junit(testResults: 'target/surefire-reports/*.xml', allowEmptyResults : true)
        }
    }
    
}
