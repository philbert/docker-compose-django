#!/groovy

node('master') {
    // trivial change
    stage "setup environment"
    checkout scm
    env.DOCKER_HOST = "88.80.174.72:2376"
    env.DOCKER_TLS_VERIFY="1"
    env.DOCKER_CERT_PATH="/var/jenkins_home/.docker"
    env.COMPOSE_PROJECT_NAME="tdddjango"
    sh "env"
    sh "docker ps"
    sh "docker-compose ps"
    
    stage "pull images"
    docker.withRegistry("https://quay.io/v1", "quay-credentials") {
        sh "docker-compose pull"
    }
    
    stage "deploy app"
    sh "docker-compose up -d"
    
    stage "run migrations"
    sh "docker exec tdddjango_webapp_1 /usr/local/bin/python manage.py migrate"
}
