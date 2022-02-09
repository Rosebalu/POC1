pipeline{
    agent any
    
    stages{
     stage('SCM'){
         steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '11622c4b-3b28-47d8-9b2d-f234de42d78c', url: 'https://github.com/Rosebalu/POC1.git']]])
         }
     }
     stage('build docker image'){
         steps{
             sh 'docker build -t wordpress .'
         }
     }
     stage('push docker image'){
         steps{
             sh 'docker tag wordpress rosebalu/wordpress:word'
             sh 'docker push rosebalu/wordpress:word'
         }
     }
     stage('deploy image to instance'){
         steps{
             sshagent (credentials: ['ssh']) {
               sh 'ssh ec2-user@172.31.45.130'
               sh 'docker pull rosebalu/wordpress:word'
            }
            }
             
         }
}
         post('trigger the ansible-playbook'){
         success{
             ansiblePlaybook disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts', playbook: 'playbook.yml'
         }
         
     }
}
