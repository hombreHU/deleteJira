pipeline {
  agent any
  stages {
    stage('delete Jira ') {
      steps {
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/jira-service.yaml'
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/jira-pod.yaml'
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/jira-claim.yaml'
      }
    }
    stage('delete PostgreSQL') {
      steps {
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/postgres-service.yaml'
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/postgres-pod.yaml'
        sh '/Data/jenkins/kubectl delete -f /Data/jenkins/postgres-claim.yaml'
      }
    }
    stage('check') {
      steps {
        sh 'until [ `/Data/jenkins/kubectl get pv |  wc -l` -eq 0 ];  do echo "- Still deleting... -"; /Data/jenkins/kubectl get pv ; sleep 15; done'
      }
    }
  }
}