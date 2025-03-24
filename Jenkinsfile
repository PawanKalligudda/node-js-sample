pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials')
    }
    stages {
	stage('Clone Repository'){
            steps{
                git branch: 'main', url: 'https://github.com/PawanKalligudda/node-js-sample.git'
            }
        }
	stage('Build Docker Image') {
	    steps {
		sh 'docker build -t node-js-sample:1.0 .'
	    }
	}
	stage('Push to Docker Hub') {
	    steps {
		sh 'docker login -u $DOCKER_HUB_CREDENTIALS_USR -p $DOCKER_HUB_CREDENTIALS_PSW'
		sh 'docker tag node-js-sample:1.0 pawankalligudda/node-js-sample:1.0'
		sh 'docker push pawankalligudda/node-js-sample:1.0'
	    }
	}
	stage('Deploy to kubernetes') {
	    steps {
		sh 'sudo minikube delete'
		sh 'sudo rm -rf ~/.minikube ~/.kube'
		sh 'sudo rm -rf /usr/local/bin/minikube'
		sh 'sudo curl -LO https://storage.googleapis.com/minikube/latest/minikube-linux-amd64'
		sh 'sudo install minikube-linux-amd64 /usr/local/bin/minikube'
		sh 'minikube version'
		sh 'minikube start'    
		sh 'kubectl config get-contexts'
		sh 'kubectl get pods'
		sh 'kubectl get nodes'
		sh 'kubectl apply -f k8s/deployment.yaml'
	    }
	}
    }
}
