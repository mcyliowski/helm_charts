pipeline {
    agent any

    environment {
        HELM_RELEASE = "moja-apka"       // nazwa release w Helm
        HELM_NAMESPACE = "jenkins"            // namespace w Kubernetes
        CHART_PATH = "."                       // ścieżka do chartu w repo
    }

    stages {
        stage('Checkout Helm Charts') {
            steps {
                git branch: 'main', url: 'https://github.com/mcyliowski/helm_charts.git'
            }
        }

        stage('Deploy with Helm') {
            steps {
                sh """
                helm upgrade --install $HELM_RELEASE $CHART_PATH \\
                  --namespace $HELM_NAMESPACE \\
                  --values $CHART_PATH/values.yaml
                """
            }
        }
    }
}
