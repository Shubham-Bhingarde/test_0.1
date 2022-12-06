// Jenkinsfile (Declarative Pipeline) for integration of Dastardly, from Burp Suite.

pipeline {
    agent any
    stages {
        
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                cleanWs()
                sh '''
                    sudo docker run --user $(id -u) -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e DASTARDLY_TARGET_URL=http://www.impladent.co.in/ \
                    -e DASTARDLY_OUTPUT_FILE=${WORKSPACE}/dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }
    }
    post {
        always {
            junit testResults: 'dastardly-report.xml', skipPublishingChecks: true
        }
    }
}
