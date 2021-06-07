// pipeline{
//         agent any
//         stages{
//             stage('Make Directory'){
//                 steps{
//                     sh "mkdir ~/jenkins-tutorial-test"
//                 }
//             }
//             stage('Make Files'){
//                 steps{
//                     sh "touch ~/jenkins-tutorial-test/file1 ~/jenkins-tutorial-test/file2"
//                 }
//             }
//         }
// }


pipeline{
        agent any
        stages{
                stage('Clone repo'){
                        steps{
//                                 sh "sudo apt-get update"
//                                 sh "rm -r chaperootodo_client"
                                git branch: 'main', url: 'https://gitlab.com/qacdevops/chaperootodo_client.git'
                        }
                }
                stage('Install docker & docker-compose'){
                        steps{
                                 sh '''sudo apt-get update
                                        sudo apt install -y curl jq
                                        curl https://get.docker.com | sudo bash
                                        version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r \'.tag_name\')
                                        sudo curl -L "https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
                                        sudo chmod +x /usr/local/bin/docker-compose'''
                        }
                }
                stage('Deploy'){
                        steps{
                                sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d"
                        }
                }
        }
}
