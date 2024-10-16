pipeline {
    agent any

    stages {
        stage('Git_Project_File') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/AndrewMego/Deployment-of-super-Mario-on-Kubernetes-using-terraform.git', branch: 'main'
            }
        }

        stage('Terraform Init and Apply') {
            steps {
                script {
                    sh '''
                    cd Deployment-of-super-Mario-on-Kubernetes-using-terraform/EKS-TF && terraform init && terraform apply && echo "Done"
                       '''
                           // Initialize and apply Terraform using the Terraform plugin
                    //terraformInit(dir: 'Deployment-of-super-Mario-on-Kubernetes-using-terraform/EKS-TF')
                    //terraformApply(dir: 'Deployment-of-super-Mario-on-Kubernetes-using-terraform/EKS-TF', varFile: '')
                }
            }
        }

        stage('Configure AWS EKS') {
            steps {
                // Configure AWS EKS using the AWS CLI
                sh '''
                aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1
                '''
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Deploy application to Kubernetes using kubectl
                dir('Deployment-of-super-Mario-on-Kubernetes-using-terraform/EKS-TF') {
                    sh '''
                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed"
        }
        success {
            echo "Pipeline succeeded"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
