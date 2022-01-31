node{
     stage('SCM Checkout'){
         git credentialsId: 'b77b2983-3d60-4d23-97b4-d81838dd3b8a', url: 'https://github.com/Rosebalu/POC1.git'
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
