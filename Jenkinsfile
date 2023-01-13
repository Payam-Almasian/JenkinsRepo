pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        
        stage('checkout')
        {
            steps{
                git 'https://github.com/OctopusSamples/RandomQuotes-Java.git'
                sh "ls -lah"
                //sh "./mvnw -N wrapper:wrapper"
            }
        }
        stage('test'){
            steps {
                sh(script: './mvnw --batch-mode -Dmaven.test.failure.ignore=true test')
                //junit 'reports/**/*.xml' 
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
