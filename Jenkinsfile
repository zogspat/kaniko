pipeline {
  agent {
     node {
        label 'java-docker-slave'
        }
  }
  stages {
    stage('Build and push')
    {
      steps
{
        withKubeConfig(credentialsId: 'kubeconfig')
        {
          sh "kubectl apply -f kanikoBuildPod.yaml"
        }
      }
    }
    stage('Deploy app to kubernetes')
    {
      steps
      {
        withKubeConfig(credentialsId: 'kubeconfig')
        {
          sh "kubectl apply -f kubeDepPlusService.yaml"
        }
      }
    }

  }

}
