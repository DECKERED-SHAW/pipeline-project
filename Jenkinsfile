pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/DECKERED-SHAW/pipeline-project.git'
            }
        }

        stage('Deploy Website') {
            steps {
                sh '''
                ssh -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                ubuntu@13.233.244.252 "mkdir -p /tmp/website"

                scp -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                -r * \
                ubuntu@13.233.244.252:/tmp/website/

                ssh -i /var/lib/jenkins/keypair.pem \
                -o StrictHostKeyChecking=no \
                ubuntu@13.233.244.252 "
                sudo cp -r /tmp/website/* /var/www/html/
                sudo systemctl reload nginx
                "
                '''
            }
        }
    }
}
