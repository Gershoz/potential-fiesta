pipeline
{
    agent any
    environment
    {
    REGISTRY_URL = "352708296901.dkr.ecr.eu-central-1.amazonaws.com"
    IMAGE_TAG = "0.0.$BUILD_NUMBER"
    IMAGE_NAME = "gershoz_dev_bot_build"
    }
    stages
    {
        stage('Build')
        {
            steps {
                // TODO dev bot build stage                
                sh '''
                aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin $REGISTRY_URL
                docker build -t $IMAGE_NAME .
                docker tag $IMAGE_NAME $REGISTRY_URL/$IMAGE_NAME:$IMAGE_TAG
                docker push $IMAGE_NAME
                '''
            }
        }
    }
//         stage('Trigger Deploy') {
//             steps {
//                 build job: 'BotDeploy', wait: false, parameters: [
//                     string(name: 'BOT_IMAGE_NAME', value: "<image-name>")
//                 ]
//             }
//         }
//     }
//         docker {
//             // TODO build & push your Jenkins agent image, place the URL here
//             image '<jenkins-agent-image>'
//             args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
}