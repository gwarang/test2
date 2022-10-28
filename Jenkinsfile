pipeline {
  agent any
  stages {
    stage('git clone or git pull') {
      steps {
        git url: 'https://github.com/gwarang/test2.git', branch: 'master'
      }
    }

    stage('docker image builder and push to private registry') {
      steps {
        sh '''
        docker build -t 192.168.8.100:5000/testweb:green .
	docker push 192.168.8.100:5000/testweb:green
	'''
      }
    }

    stage('deployment, svc creation') {
      steps {
        sh '''
	kubectl create deploy testweb --image=192.168.8.100:5000/testweb:green
	kubectl expose deploy testweb --type=LoadBalancer --port=80 --target-port=80 --name=testweb-svc
	'''
      }
    }
  }
}
