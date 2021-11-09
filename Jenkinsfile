pipeline {
  agent 
  {
    label 'master'
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
    // Not working: this next stage executes immediately the shell command returns which is
    // long before the Kaniko build has pushed the image to Docker Hub...
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
