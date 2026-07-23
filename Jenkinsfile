pipeline {                                          
    agent any                                       
    parameters {                                    
        choice(name: 'ENV', choices: ['a','b'])    
    }
    stages {                                      
        stage('Build') {                        
            steps {                               
                sh "echo Building for ${params.ENV}" 
            }
        }
        stage('Deploy') {
            when {                                 
                expression { params.ENV == 'b' }   
            }
            steps {
                sh 'echo Deploying'                
            }
        }
    }
    post {                                          
        success {
            echo 'Done'
        }
    }
}
