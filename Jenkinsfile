pipeline {
  agent {
    label "Linux"
    }
    stages {
        stage('BuildinDevelopment') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n dev'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/nvosetti/springboot-sample-app  -n dev'
				sh 'oc expose service springboot-sample-app  -n dev'
            }
        }
        stage('TestinginDevelopment') {
            steps {
                sh 'sleep 60'
				sh 'wget -q "http://springboot-sample-app-dev.apps.usadkub01.cotiviti.com" -O /dev/null'
			    sh 'if [ $? == "0" ]; then echo "OK"; else echo "Failed";fi'
            }
        }
        stage('BuildinQA') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n qa'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/nvosetti/springboot-sample-app  -n qa'
				sh 'oc expose service springboot-sample-app  -n qa'
            }
        }
        stage('TestinginQA') {
            steps {
                sh 'sleep 60'
				sh 'wget -q "http://springboot-sample-app-qa.apps.usadkub01.cotiviti.com" -O /dev/null'
			    sh 'if [ $? == "0" ]; then echo "OK"; else echo "Failed";fi'
            }
        }
        stage('DeployProdApproval'){
            steps{
			    input message: 'Do you want to proceed to PROD?'
			}
        } 
        stage('BuildinProd') {
            steps {
                sh 'oc delete all --selector app=springboot-sample-app -n prod'
                sh 'oc new-app codecentric/springboot-maven3-centos~https://github.com/nvosetti/springboot-sample-app  -n prod'
				sh 'oc expose service springboot-sample-app  -n prod'
            }
        }
        stage('TestinginProd') {
            steps {
                sh 'sleep 60'
				sh 'wget -q "http://springboot-sample-app-prod.apps.usadkub01.cotiviti.com" -O /dev/null'
			    sh 'if [ $? == "0" ]; then echo "OK"; else echo "Failed";fi'
            }
        }
        
    }
}
