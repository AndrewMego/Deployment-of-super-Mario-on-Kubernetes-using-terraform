pipeline {
    agent any
    stages {
        stage('Git_Project_File') {
              steps {
                // Use Jenkins' built-in git step
                git url: 'https://github.com/AndrewMego/Deployment-of-super-Mario-on-Kubernetes-using-terraform.git', branch: 'main'
            }
        }
          stage('Build_Terra') {
            steps {
                // Add your build steps here, e.g., running Terraform commands
                sh '''
                cd Deployment-of-super-Mario-on-Kubernetes-using-terraform/EKS-TF && terraform init && terraform apply && echo "Done"
                '''
            }
        }
           stage('Build_AWS') {
            steps {
                // Add your build steps here, e.g., running Terraform commands
                sh ''' aws eks update-kubeconfig --name EKS_CLOUD --region ap-south-1 ''' 
            }
        }
        
           stage('Build_Kuber') {
            steps {
                // Add your build steps here, e.g., running Terraform commands
                sh ''' cd .. '''
                sh ''' kubectl apply -f deployment.yaml '''
                sh ''' kubectl apply -f service.yaml '''
                
            }
        }

    }
}
