pipeline
{
    agent any
    stages
    {
        stage('Build')
        {
            steps {
                // TODO dev bot build stage                
                sh '''
                aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 352708296901.dkr.ecr.eu-central-1.amazonaws.com
                docker build -t gershoz_dev_bot_build:0.0.$BUILD_NUMBER .
                docker tag gershoz_dev_bot_build:0.0.$BUILD_NUMBER 352708296901.dkr.ecr.eu-central-1.amazonaws.com/gershoz_dev_bot_build:0.0.$BUILD_NUMBER
                docker push 352708296901.dkr.ecr.eu-central-1.amazonaws.com/gershoz_dev_bot_build:0.0.$BUILD_NUMBER
                '''
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'BotDeploy', wait: false, parameters: [
                    string(name: 'BOT_IMAGE_NAME', value: "<image-name>")
                ]
            }
        }
    }
}
//         docker {
//             // TODO build & push your Jenkins agent image, place the URL here
//             image '<jenkins-agent-image>'
//             args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
