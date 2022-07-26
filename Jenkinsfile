pipeline {
    agent any
    
    tools{
        maven 'maven3'
    }
    
    parameters {
        booleanParam(defaultValue: false, description: 'clean wk?', name: 'clean')
        booleanParam(defaultValue: false, description: 'build?', name: 'build')
        booleanParam(defaultValue: false, description: 'test?', name: 'test')
        booleanParam(defaultValue: false, description: 'package?', name: 'package')
        booleanParam(defaultValue: false, description: 'deploy?', name: 'deploy')
        gitParameter(
      branch: '',
      branchFilter: ".*",
      defaultValue: "origin/master",
      description: 'which branch ?',
      name: 'BRANCH_',
      sortMode: 'ASCENDING_SMART',
      tagFilter: "*",
      type: 'PT_BRANCH_TAG',
      useRepository: 'https://github.com/jenkins-docs/simple-java-maven-app.git')
   }
        
    
    stages {
        stage('Clean Workspace'){
            when {
                expression { params.clean }
            }
            steps{
                deleteDir()
            }
        }
        stage('CheckOut') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jenkins-docs/simple-java-maven-app.git']]])
            }
        }
        stage('Build') {
            when {
                expression { params.build }
            }
            steps {
                sh ' mvn compile '
            }
        }
        stage('Test') {
            when {
                expression { params.test }
            }
            steps {
                sh ' mvn test '
            }
        }
        stage('Packaging') {
            when {
                expression { params.package }
            }
            steps {
                sh ' mvn package '
            }
        }
        stage('Deploy') {
            when {
                expression { params.deploy }
            }
            steps {
                sh ' mvn deploy '
            }
        }
    }
}

