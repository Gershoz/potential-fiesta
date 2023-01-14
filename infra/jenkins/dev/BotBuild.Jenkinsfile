pipeline
{
    agent 
    {
        docker 
        {
            image '352708296901.dkr.ecr.eu-central-1.amazonaws.com/gershoz_dev_bot_build:latest'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    environment
    {
        REGISTRY_URL = "352708296901.dkr.ecr.eu-central-1.amazonaws.com"
        IMAGE_TAG = "0.0.$BUILD_NUMBER"
        IMAGE_NAME = "gershoz_dev_bot_build"        
        APP_ENV = "prod"
    }
    stages
    {
        stage('Build')
        {
            steps 
            {
                sh '''
                aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin $REGISTRY_URL
                docker build -t $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG . -f services/bot/Dockerfile --label "author=gershoz"
                docker push $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG
                '''
            }
            post 
            {
                always 
                {
                    sh '''
                       docker images | grep "gershoz_dev_bot_build" | awk '{print $1 ":" $2}' | xargs docker rmi
                    '''
                }
            }
        }
        stage('Trigger Post List') 
        {
            steps 
            {
                build job: 'prod/botBuild', wait: false, parameters: 
                [
                    string(name: 'BOT_IMAGE_NAME', value: "${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}")
                ]
            }
        }
    }
}
