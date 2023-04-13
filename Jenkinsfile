pipeline {
    agent any
    environment{
        IMAGE_NAME= '20it065/spring_exam-app:6.5'
    }

    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    echo "building the spring application"
                    sh 'mvn package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "Building The Docker image and push to docker hub..."
                    //gv.buildImage()
                    withCredentials([usernamePassword(credentialsId: '50da56cc-c869-454c-9e27-01f9dc560573', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
                        sh 'docker build -t ${IMAGE_NAME} .'
                        sh 'docker login -u $USERNAME -p $PASSWORD'
                        sh 'docker push ${IMAGE_NAME}'
                    }
                }
            }
        }
    }
}
