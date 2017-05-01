pipeline {
  agent any
  stages {
    stage('REPO-DOWNLOAD') {
      steps {
        git(url: 'https://github.com/versionit/mvnrepo.git', branch: 'demo1')
      }
    }
    stage('Compile') {
      steps {
        sh 'mvn clean compile package'
      }
    }
    stage('Deploy-Nexus') {
      steps {
        sh 'mvn deploy'
      }
    }
    stage('Deploy-Tomcat') {
      steps {
        sh '''JNAME=$(echo $JOB_NAME |cut -d / -f2)
sudo su - javaee7 -c "/home/javaee7/deploy-pl.sh $JNAME"'''
      }
    }
  }
}