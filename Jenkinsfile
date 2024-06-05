pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials' // Jenkins credentials ID for Docker Hub
        REPOSITORY_BACKEND_MODULE1 = 'syedafatima02/i211213-backend-auth'
        REPOSITORY_BACKEND_MODULE2 = 'syedafatima02/i211213-backend-classrooms'
        REPOSITORY_BACKEND_MODULE3 = 'syedafatima02/i211213-backend-eventbus'
        REPOSITORY_BACKEND_MODULE4 = 'syedafatima02/i211213-backend-post'
        REPOSITORY_FRONTEND = 'syedafatima02/i211213-frontend-client'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/NUCESFAST/scd-final-lab-exam-SyedaFatima002.git'
            }
        }

        stage('Install Dependencies') {
            parallel {
                stage('Install Backend Auth Dependencies') {
                    steps {
                        dir('Auth') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Install Backend Classrooms Dependencies') {
                    steps {
                        dir('Classrooms') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Install Backend Event-bus Dependencies') {
                    steps {
                        dir('event-bus') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Install Backend Post Dependencies') {
                    steps {
                        dir('Post') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Install Frontend Dependencies') {
                    steps {
                        dir('client') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }

        stage('Build Docker Images') {
            parallel {
                stage('Build Backend Auth Module') {
                    steps {
                        script {
                            docker.build("${env.REPOSITORY_BACKEND_MODULE1}", 'Auth')
                        }
                    }
                }
                stage('Build Backend Classrooms Module') {
                    steps {
                        script {
                            docker.build("${env.REPOSITORY_BACKEND_MODULE2}", 'Classrooms')
                        }
                    }
                }
                stage('Build Backend Event-bus Module') {
                    steps {
                        script {
                            docker.build("${env.REPOSITORY_BACKEND_MODULE3}", 'event-bus')
                        }
                    }
                }
                stage('Build Backend Post Module') {
                    steps {
                        script {
                            docker.build("${env.REPOSITORY_BACKEND_MODULE4}", 'Post')
                        }
                    }
                }
                stage('Build Frontend Module') {
                    steps {
                        script {
                            docker.build("${env.REPOSITORY_FRONTEND}", 'client')
                        }
                    }
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', env.DOCKER_CREDENTIALS_ID) {
                        parallel(
                            'Push Backend Auth Module': { docker.image("${env.REPOSITORY_BACKEND_MODULE1}").push() },
                            'Push Backend Classrooms Module': { docker.image("${env.REPOSITORY_BACKEND_MODULE2}").push() },
                            'Push Backend Event-bus Module': { docker.image("${env.REPOSITORY_BACKEND_MODULE3}").push() },
                            'Push Backend Post Module': { docker.image("${env.REPOSITORY_BACKEND_MODULE4}").push() },
                            'Push Frontend Module': { docker.image("${env.REPOSITORY_FRONTEND}").push() }
                        )
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs() // Clean workspace after build
        }
    }
}
