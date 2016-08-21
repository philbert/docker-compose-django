#!/groovy

node('master') {
    stage "setup environment"
    checkout scm
    env.DOCKER_HOST = "192.121.20.151:2375"
    env.DOCKER_TLS_VERIFY="1"
    env.DOCKER_CERT_PATH="/var/jenkins_home/.docker"
    env.COMPOSE_PROJECT_NAME="tdddjango"
    sh "env"
    sh "docker ps"
    sh "docker-compose ps"
    
    stage "docker compose build"
    sh "docker-compose build"
    
    stage "deploy app"
    sh "docker-compose up -d"
    
    stash "run migrations"
    sh "docker run webapp /usr/local/bin/python manage.py migrate"

}
