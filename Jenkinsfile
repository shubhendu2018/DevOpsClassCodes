pipeline {
    agent any
    
    tools{
        maven 'mymaven'
    }
    
    stages {
        stage('CloneRepo') {
            steps {
                echo 'This is Stage 1'
                git 'https://github.com/shubhendu2018/DevOpsClassCodes.git'
            }
        }
        stage('Complie Stage') {
            steps {
                echo 'This is Stage 2'
                sh 'mvn compile'
            }
            
        }
        stage('Code review Stage') {
            steps {
                echo 'This is Stage 3'
                sh 'mvn pmd:pmd'
            }
            post{
                success{
                    recordIssues(tools: [pmdParser(pattern: 'target/pmd.xml')])
                }
            }
            
        }
        stage('Code testing Stage') {
            steps {
                echo 'This is Stage 4'
                sh 'mvn test'
            }
            post{
                success{
                    junit 'target/surefire-reports/*.xml'
                }
            }
            
        }
        stage('Code package Stage') {
            steps {
                echo 'This is Stage 5'
                sh 'mvn package'
            }

            
        }
    }
}
