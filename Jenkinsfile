pipeline{
    agent {label 'Sprinng-petclinic-proj-node1'}
    options{
        timeout(time: 30, unit: 'MINUTES') // faild the build in 30 min if build not success
    }
    triggers{
        pollSCM('* * * * *') // build code in every minutes when commits happend
    }
     tools {
        jdk 'JDK_17' 
    }

    stages{
        stage('svc'){
            steps {
                git url: 'https://github.com/mk2502dev/spring-petclinic-1.git',
                    branch: 'develop'
            }
        }
        stage('Build and packages'){
            steps {
                sh script: 'mvn package'
            }
        }
        stage('Reporting'){
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-*.jar'
                junit testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }
    }


}