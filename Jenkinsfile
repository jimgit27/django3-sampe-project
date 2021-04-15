pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/jimgit27/django3-sampe-project.git'

                
            }
        }
        
        stage('Test') {
            steps {
                sh '''
                    python3 -m venv myvenv
                    source myvenv/bin/activate
                    pip install -r requirements.txt
                    cd myproject
                    cp myproject/.env.example myproject/.env
                    ./manage.py test'''
            }
        }

        stage('Deploy w/ ansible'){
            steps {
                sshagent (credentials:["ssh-deployment-1"]){

                    sh '''
                        pwd
                        echo $WORKSPACE
                        ansible-playbook -i ~/workspace/ansible-proj/hosts.yml -l deploymentservers ~/workspace/ansible-proj/playbooks/check.yml
                    '''
                }
            }
        }
    }
}
