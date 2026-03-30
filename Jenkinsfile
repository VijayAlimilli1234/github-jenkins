pipeline {
    agent any

    environment {
        IMAGE = "vijayalimilli9/site1:v7"
        DOCKER_USER = "vijayalimilli9"
        DOCKER_PASS = "123456789"
    }

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push $IMAGE'
            }
        }

        stage('Deploy with Helm') {
            steps {
                sh '''
                cd /var/lib/jenkins/site3-chart
                sed -i 's/tag:.*/tag: v7/' values.yaml
                helm upgrade site3-release .
                '''
            }
        }
    }
}
