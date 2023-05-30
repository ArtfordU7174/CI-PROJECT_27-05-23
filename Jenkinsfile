pipeline {
    agent any
    tools{
        maven 'mvn'
        jdk 'JDK8'
    }
    environment {
        SNAP_REPO = 'vpro-snapshots'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin'
        RELEASE_REPO = 'vpro-release'
        CENTRAL_REPO = 'vipro-maven-central'
        NEXUS_IP = '172.31.1.241'
        NEXUS_PORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages{
        stage('BUILD'){
            steps{
                sh 'mvn -s settings.xml install -DskipTests'
            }
            post {
                success {
                    echo 'Archiving Artifacts'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('TEST'){
            steps {
                sh 'mvn -s settings.xml test'
                }
        }
        stage('CHECKSTYLE ANALYSIS'){
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}