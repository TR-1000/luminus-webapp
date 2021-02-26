def builderImage
def productionImage
def ACCOUNT_REGISTRY_PREFIX
def GIT_COMMIT_HASH

pipeline {
    agent any
    stages {
        stage('Checkout Source Code and Logging Into Registry') {
            steps {
                echo 'Logging Into the Private ECR Registry'
                script {
                    GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
                    ACCOUNT_REGISTRY_PREFIX = "193332868148.dkr.ecr.us-east-2.amazonaws.com"
                    sh """
                    \$(aws ecr get-login --no-include-email --region us-east-2)
                    """
                }
            }
        }

        

        stage('Deploy Container') {
            steps {
                echo 'Restarting Docker'
                script {
                    try {
                        sh 'docker kill $(docker ps -q)'
                    } catch (Exception e) {
                        echo 'No containers are running'
                    } finally {
                        echo 'Starting container'
                        sh 'docker run --rm -d -p 3000:3000 193332868148.dkr.ecr.us-east-2.amazonaws.com/example-webapp:$(git rev-parse HEAD)'
                    }
                }
            }
        }
        
    }
}
