pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy') {
                    steps {
                       echo "my dir"
                       dir('/home/ubuntu/project/ibm-wave4-workpro')
                         {
                          echo "changed dir"
                          sh 'docker-compose -f docker-compose.yml up --build -d --remove-orphans'
                       }
                    }
        }
    }
}
