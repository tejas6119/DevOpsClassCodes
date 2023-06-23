pipeline {
    agent any
        tools {
            maven 'maven'
        }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'This is stage 1'
                git 'https://github.com/tejas6119/DevOpsClassCodes.git'
            }
        }
        
         stage('Compile Stage') {
            steps {
                echo 'This is stage 2'
                sh 'mvn compile'
            }
        }
        
          stage('Code Review Stage') {
            steps {
                echo 'This is stage 3'
                sh 'mvn pmd:pmd'
            }
            post{
                success{
                    recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')])
                }
            }
        }
        
        stage('Code Test Stage') {
            steps {
                echo 'This is stage 4'
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Package Stage') {
            steps {
                echo 'This is stage 5'
                sh ' mvn package'
            }
        }
    }
}
