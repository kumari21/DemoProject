pipeline{
    agent any
    tools{
        gradle 'Gradle'
    }
    stages{
        stage('build jar'){
            steps{
                echo "Building jar file"
                sh 'gradle clean build'
            }
        }
        stage('build docker image'){
            steps{
                echo "Buildind docker image"
                sh 'docker build -t java-gradle:0.1 .'
            }
        }
        stage('deploy'){
            steps{
                echo "Deploying application"
                sh 'docker rm -f java-gradle-app'
                sh 'docker run --rm -dp 3000:8080 --name java-gradle-app java-gradle:0.1'
                echo "Application is live on <ip-address>:3000"
            }
        }
    }
    post{
        success{
            archiveArtifacts artifacts: 'build/**/*-SNAPSHOT.jar', followSymlinks: false
        }
    }
}
