node {
    stage('Code Checkout') {
        echo 'Code checkout from the git repo'
        git 'https://github.com/Gulajkar-sham23/Gulajkar-sham23.git'
    }

    stage('Building the application') {
        echo 'Moving inside the directory and then building the application'
        sh 'docker build -t sham23docker/my-php-app:1.0 .'
    }

    stage('Pushing docker image') {
        echo 'Pushing docker image to Docker Hub'
        def dockerHubCredentials = 'docker-hub-credentials'
        withCredentials([usernamePassword(credentialsId: dockerHubCredentials, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
            sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
            sh 'docker push sham23docker/my-php-app:1.0'
        }
    }
    
    stage ('Application Deployment'){
        echo 'Deploying the application in the server'
        sh 'docker run -d -p 8081:80 sham23docker/my-php-app:1.0'
    } 
}
