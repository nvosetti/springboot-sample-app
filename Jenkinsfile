pipeline {
  agent {
    label "linux"
    }
    stages {
        stage('BuildinDevelopment') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n dev'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/codecentric/springboot-sample-app -n dev'
				        sh 'oc expose service springboot-sample-app  -n dev'
            }
        }
        stage('BuildinQA') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n qa'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/codecentric/springboot-sample-app -n qa'
				        sh 'oc expose service springboot-sample-app  -n qa'
            }
        }
        stage('Deploy approval'){
            steps{
			    input message: 'Do you want to proceed to PROD?'
			}
        } 
        stage('BuildinProd') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n prod'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/codecentric/springboot-sample-app -n prod'
				        sh 'oc expose service springboot-sample-app  -n prod'
            }
        }
        
    }
}
