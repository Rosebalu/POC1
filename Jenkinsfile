pipeline{
    agent any
    
    stages{
     stage('SCM'){
         steps{
            git branch: 'main', credentialsId: '1d5f0874-7845-4dc8-a2e1-364a5dd3e5cb', url: 'https://github.com/Rosebalu/POC1.git'
         }
     }
     stage('build docker image'){
         steps{
             sh 'docker build -t wordpress .'
         }
     }
     stage('push docker image'){
         steps{
             sh 'docker login -u rosebalu -p Rosebalu@2022'
             sh 'docker tag wordpress rosebalu/wordpress:words'
             sh 'docker push rosebalu/wordpress:words'
         }
     }
     stage('deploy image to instance'){
         steps{
             sshagent(credentials: ['root']){
               sh 'ssh -o StrictHostKeyChecking=no root@15.152.39.227'
               sh 'docker login -u rosebalu -p Rosebalu@2022'
               sh 'docker pull rosebalu/wordpress:words'
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
