pipeline {
  environment {
        DOCKERHUB_CREDENTIALS=credentials('haleema-dockerhub')
    }
  agent none
  stages {
    stage('Login to Dockerhub') {
      agent any
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        } 
    
    stage('On-RPI') {
      agent {label 'linuxslave1'}
          steps {
           sh 'echo "collecting data from sound sensor" '
           git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-RPI-sound-sensor.git'
           //sh 'docker build -t haleema/docker-rpi-sound:latest .'
           //sh 'docker run --privileged -t haleema/docker-rpi-sound'

            sh 'echo "collecting data from flame sensor" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-RPI-flame-sensor.git'
            sh 'docker build -t haleema/docker-rpi-flame:latest .'
            //sh 'docker run --privileged -t haleema/docker-rpi-flame'
            
            sh 'echo "collecting data from DHT11 sensor" '
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-RPI-DHT11-sensor.git'
            sh 'docker build -t haleema/docker-rpi-dht:latest .'
            //sh 'docker run --privileged -t haleema/docker-rpi-dht'

            }
    }
    stage('On-Edge-rec-data') {
      agent any
        steps {
            sh 'echo "edge-rec-3con-data"'
            git branch: 'main', url: 'https://github.com/HaleemaEssa/jenkins-edge-rec.git'
            sh 'docker build -t haleema/docker-edge1:latest .'
            echo "Started stage A"
            //sh 'docker run -v "${PWD}:/data" -t haleema/docker-edge1'
            }
        }
           
    }
}
