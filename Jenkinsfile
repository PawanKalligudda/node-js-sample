pipeline {
    agent any
    stages {
	stage('Clone Repository') {
            steps {
		git 'https://github.com/PawanKalligudda/node-js-sample.git'
	    }
	}
	stage('Build Docker Image') {
	    steps {
		sh 'docker build -t node-js-sample:1.0 .'
	    }
	}
	stage('Push to Docker Hub') {
	    steps {
		sh 'docker tag node-js-sample:1.0 pawankalligudda/node-js-sample:1.0'
		sh 'docker push pawankalligudda/node-js-sample:1.0'
	    }
	}
	stage('Deploy to kubernetes') {
	    steps {
		sh 'kubectl apply -f k8s/deployment.yaml'
	    }
	}
    }
}
