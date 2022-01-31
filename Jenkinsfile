pipeline{
    agent any
    
    stages('SCM Checkout'){
        git credentialsId: 'fa5d9105-a1d3-4af1-a64d-318621b750cf', url: 'https://github.com/Rosebalu/POC1.git'
    }
     stage('build docker image'){
         sh 'docker build -t wordpress .'
     }
     stage('push docker image'){
         sh 'docker login -u rosebalu -p Cloudifyops@2022'
         sh 'docker push Rosrbalu/wordpressapplication'
     }
     stage('deploy image to instance'){
         def dockerimage: 'docker pull Rosrbalu/wordpress'
         sshagent(['server']) {
             sh 'ssh -o StrictHostKeyChecking=no ec2_user@172.31.13.255 ${dockerimage}'
         }
     }
     
}
