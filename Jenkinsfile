pipeline{
    agent{ label 'AGENT-1'}
    stages{
        stage('Install dependencies'){
            steps{
                sh 'npm install'
            }
        }
        stage('unit test'){
            steps{
                echo "unit testing is done here"
            }
        }
        // stage('Sonar Scan'){
        //     steps{
        //         sh 'ls -ltr'
        //         sh 'sonar-scanner'
        //     }
        // }
        stage('build'){
            steps{
                sh 'ls -ltr'
            }
        }
    }
    
}