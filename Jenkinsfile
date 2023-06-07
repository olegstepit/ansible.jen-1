#!groovy
//  groovy Jenkinsfile
properties([disableConcurrentBuilds()])\

pipeline  {
        agent { 
           label ''
        }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    stages {
        stage("Git clone") {
            steps {
                sh '''
                cd /home/an/
                git clone https://github.com/Makson8286/ansible.jen         
                '''
            }
        }    
        stage("Build") {
            steps {
                sh '''
                cd /home/an/ansible.jen/Ansible
                docker build -t oleg222/ansible .
                '''
            }
        } 
        stage("Postgres") {
            steps {
                sh '''
                docker run \
                --name ansible \
                -d oleg222/ansible
                '''
            }
        }
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'DockerHub-Credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '''
                    docker login -u $USERNAME -p $PASSWORD
                    '''
                }
            }
        }
        stage("docker push") {
            steps {
                echo " ============== pushing image =================="
                sh '''
                docker push oleg222/ansible
                '''
            }
        }
    }
}
