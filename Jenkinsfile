pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                url: https://github.com/DECKERED-SHAW/pipeline-project.git
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                ssh -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                ubuntu@<NGINX_PUBLIC_IP> "mkdir -p /tmp/website"

                scp -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                -r * \
                ubuntu@<NGINX_PUBLIC_IP>:/tmp/website/

                ssh -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                ubuntu@<NGINX_PUBLIC_IP> "
                sudo cp -r /tmp/website/* /var/www/html/
                sudo systemctl reload nginx
                "
                '''
            }
        }
    }
}
