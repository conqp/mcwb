pipeline {
  agent any
  stages {
    stage('Run pytest') {
      steps {
        sh 'pip install --upgrade -r requirements.txt'
        sh 'pip install --upgrade pytest'
        sh 'python -m pytest'
      }
    }

    stage('Run SonarQube') {
      steps {
        withSonarQubeEnv(installationName: 'mcwb', credentialsId: '4cdfb484-a052-41be-8739-3e1c232b5f38') {
          sh '/opt/sonar-scanner/bin/sonar-scanner'
        }

      }
    }

    stage('Send Email') {
      steps {
        mail(subject: '[mcwb] build successful', body: 'https://jenkins.richard-neumann.de/blue/organizations/jenkins/mcwb/activity', from: 'jenkins@richard-neumann.de', to: 'mail@richard-neumann.de')
      }
    }

  }
}