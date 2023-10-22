pipeline{
    agent{ label 'AGENT-1'}
    environment{
        packageVersion=''
    }
    stages{
        stage('Get Version'){
            steps{
                script{
                    def packageJson = readJSON(file: 'package.json')
                    packageVersion = packageJson.version
                    echo "version: ${packageVersion}"
                }
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
                    nexusUrl: '54.146.66.219:8081/',
                    groupId: 'com.roboshop',
                    version: "$packageVersion",
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
                script{
                echo "Deployment"
                def params = [
                    string(name: 'version', value: "$packageVersion")
                ]
                build job: "../catalogue-deploy", wait: true, parameters: params
                }
            }
        }
    }
    post{
        always{
            echo 'cleaning up workspace'
            // deleteDir()
        }
    }
    
}