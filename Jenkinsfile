// pipeline {
//     agent any

//     environment {
//         // Define DockerHub credentials ID
//         DOCKER_HUB_CREDENTIALS_ID = 'docker-hub-credentials2'
//         // Define repository on Docker Hub
//         DOCKER_REPO_PREFIX = 'muhammadranaumerofficial754/schoolmanagementsystem'
//     }

//     stages {
//         stage('Checkout Code') {
//             steps {
//                 // Checkout the code from GitHub
//                 git 'https://github.com/NUCESFAST/scd-final-lab-exam-umerfaro.git'
//             }
//         }

//          stage('Build and Push Docker Images') {
//             steps {
//                 script {
//                     // Ensure Docker is available
//                     sh 'docker --version'
//                     // Example Docker command within script block
//                     docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS_ID) {
//                         def services = [
//                             'auth_backend_21i1184',
//                             'classrooms_backend_21i1184',
//                             'client_frontend_21i1184',
//                             'event-bus_backend_21i1184',
//                             'post_backend_21i1184'
//                         ]
//                         services.each {
//                             def app = docker.build("${DOCKER_REPO_PREFIX}/${it}", "./${it}")
//                             app.push('latest')
//                         }
//                     }
//                 }
//             }
//         }

//         stage('Deploy') {
//             steps {
//                 script {
//                     // Use Docker Compose to deploy
//                     bat  'docker-compose up -d'
//                 }
//             }
//         }

//         stage('Validate Deployment') {
//             steps {
//                 script {
//                     // Implement your validation checks here
//                     echo 'Running validation tests...'
//                     // Example: curl to check if services are up and running
//                     bat  'curl -f http://localhost:8412'
//                     bat  'curl -f http://localhost:8413'
//                     bat  'curl -f http://localhost:8411'
//                     bat  'curl -f http://localhost:8414'
//                     bat  'curl -f http://localhost:8415'
//                 }
//             }
//         }
//     }

//     post {
//         always {
//             // Cleanup after pipeline execution
//             bat  'docker-compose down'
//         }
//     }
// }


pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS_ID = 'docker-hub-credentials2'
        DOCKER_REPO_PREFIX = 'muhammadranaumerofficial754/schoolmanagementsystem'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-umerfaro.git'
            }
        }

        stage('Build and Push Docker Images') {
            steps {
                script {
                    // Ensure Docker is available
                    bat 'docker --version'
                    // Example Docker command within script block
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS_ID) {
                        def services = [
                            'auth_backend_21i1184',
                            'classrooms_backend_21i1184',
                            'client_frontend_21i1184',
                            'event-bus_backend_21i1184',
                            'post_backend_21i1184'
                        ]
                        services.each {
                           def app = docker.build("${DOCKER_REPO_PREFIX}/${it}", "./${it}")
                           echo "Pushing ${DOCKER_REPO_PREFIX}/${it}"
                           app.push('latest')
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker-compose up -d'
            }
        }

        stage('Validate Deployment') {
            steps {
                script {
                    echo 'Running validation tests...'
                    bat 'curl -f http://localhost:8412'
                    bat 'curl -f http://localhost:8413'
                    bat 'curl -f http://localhost:8411'
                    bat 'curl -f http://localhost:8414'
                    bat 'curl -f http://localhost:8415'
                }
            }
        }
    }

    post {
        always {
            bat 'docker-compose down'
        }
    }
}

