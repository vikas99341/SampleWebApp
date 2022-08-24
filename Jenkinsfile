pipeline {
    agent any
    tools {
          maven 'Maven home'
        }

    stages {
        stage('SCM-Checkout') {
            steps {
                git branch: 'main', credentialsId: 'git-credentials', 
                url: 'https://github.com/vikas99341/SampleWebApp.git'
            }
        }
        stage('Maven-Clean-Compile') {
            steps {
				sh "mvn clean compile"
            }
        }
        stage('Maven-Package') {
            steps {
				sh "mvn package"
            }
        }
        stage('Ansible-Deployment') {
            steps {
				ansiblePlaybook become: true, credentialsId: 'ec2-user-ansible', disableHostKeyChecking: true, installation: 'ansible', inventory: 'hosts', playbook: 'install-httpd.yml'
            }
        }
    }
}
