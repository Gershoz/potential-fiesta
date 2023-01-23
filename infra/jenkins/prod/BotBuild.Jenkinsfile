pipeline
{
    agent {
        docker {
            // TODO build & push your Jenkins agent image, place the URL here
            image '352708296901.dkr.ecr.eu-central-1.amazonaws.com/gershoz_jenkins_agent:latest'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }    
    environment {
    REGISTRY_URL = "352708296901.dkr.ecr.eu-central-1.amazonaws.com"
    IMAGE_TAG = "0.0.$BUILD_NUMBER"
    IMAGE_NAME = "gershoz_prod_bot"
    }
    stages
    {
        stage('Build')
        {
            steps {
                sh '''
                aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin $REGISTRY_URL
                docker build -t $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG . -f services/bot/Dockerfile
                docker push $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
        }
    }
}
