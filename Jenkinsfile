pipeline {
    agent any
    
    environment {
        
        SCANNER_HOME = tool 'sonarqube'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/ajaydabe/10-MicroService-Appliction.git'
            }
        }
        
        stage('SonarQube') {
            steps {
                
                withSonarQubeEnv('sonarqube') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
               
            }
        }
        
        stage('adservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/adservice') {
                                 sh "docker build -t ajaydabe/adservice:latest ."
                                 sh "docker push ajaydabe/adservice:latest"
								                 sh "docker rmi ajaydabe/adservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/cartservice/src/') {
                                 sh "docker build -t ajaydabe/cartservice:latest ."
                                 sh "docker push ajaydabe/cartservice:latest"
								                 sh " docker rmi ajaydabe/cartservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/checkoutservice/') {
                                 sh "docker build -t ajaydabe/checkoutservice:latest ."
                                 sh "docker push ajaydabe/checkoutservice:latest"
								                 sh " docker rmi ajaydabe/checkoutservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/currencyservice/') {
                                 sh "docker build -t ajaydabe/currencyservice:latest ."
                                 sh "docker push ajaydabe/currencyservice:latest"
								                 sh " docker rmi ajaydabe/currencyservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/emailservice/') {
                                 sh "docker build -t ajaydabe/emailservice:latest ."
                                 sh "docker push ajaydabe/emailservice:latest"
								                 sh " docker rmi ajaydabe/emailservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/frontend/') {
                                 sh "docker build -t ajaydabe/frontend:latest ."
                                 sh "docker push ajaydabe/frontend:latest"
								                 sh "docker rmi ajaydabe/frontend:latest"
                        }
                    }
                }
            }
        }
		
		stage('loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/loadgenerator/') {
                                 sh "docker build -t ajaydabe/loadgenerator:latest ."
                                 sh "docker push ajaydabe/loadgenerator:latest"
                								 sh "docker rmi ajaydabe/loadgenerator:latest"
                        }
                    }
                }
            }
        }
		
		stage('paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/paymentservice/') {
                                 sh "docker build -t ajaydabe/paymentservice:latest ."
                                 sh "docker push ajaydabe/paymentservice:latest"
								                 sh "docker rmi ajaydabe/paymentservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/productcatalogservice/') {
                                 sh "docker build -t ajaydabe/productcatalogservice:latest ."
                                 sh "docker push ajaydabe/productcatalogservice:latest"
								                 sh " docker rmi ajaydabe/productcatalogservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('recommendationservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/recommendationservice/') {
                                 sh "docker build -t ajaydabe/recommendationservice:latest ."
                                 sh "docker push ajaydabe/recommendationservice:latest"
								                 sh " docker rmi ajaydabe/recommendationservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('shippingservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-tier/src/shippingservice/') {
                                 sh "docker build -t ajaydabe/shippingservice:latest ."
                                 sh "docker push ajaydabe/shippingservice:latest"
								                 sh " docker rmi ajaydabe/shippingservice:latest"
                        }
                    }
                }
            }
        }
        
        stage('K8-Deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks22', contextName: '', credentialsId: 'k8s', namespace: 'webapp', restrictKubeConfigAccess: false, serverUrl: 'https://71C1BBCA0B37AEE8D313F37F7056C4E4.gr7.us-east-1.eks.amazonaws.com') {
                         sh 'kubectl apply -f deployment-service.yml'
                         sh 'kubectl get pods '
                         sh 'kubectl get svc'
                }
            }
        }
        
    }
}
