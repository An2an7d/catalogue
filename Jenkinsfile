pipeline{
    agent{ label 'AGENT-1'}
    environment{
        packageVersion=''
    }
    stages{
        stage('Get Version'){
            steps{
                def packageJson = readJson(file: 'package.json')
                def packageVersion = packageJson.version
                echo "version: ${packageVersion}"
            }
        }
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
        stage('Sonar Scan'){
            steps{
                echo "sonar scan done"
            }
        }
        stage('build'){
            steps{
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }

        stage('SAST'){
            steps{
                echo "SAST done"
            }
        }
          stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '54.237.18.140:8081/',
                    groupId: 'com.roboshop',
                    version: "$packageJson",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }
        stage('Deploy'){
            steps{
                echo "Deployment"
            }
        }
    }
    post{
        always{
            echo 'cleaning up workspace'
            deleteDir()
        }
    }
    
}