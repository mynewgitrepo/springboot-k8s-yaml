node
{
    stage('checkout')
    {
        git 'https://github.com/mynewgitrepo/springboot-k8s-yaml.git'
    }
    stage('build')
    {
        sh "npm config set optional false"
        sh "npm i"
    }
    stage('Sonaqube-analysis')
    {
        sh "npm run sonar"
    }
    stage('docker-image-build')
    {
        sh "docker build -t springboot-k8s:1.0.0 ."
    }
    stage('docker-image-push')
    {
        sh "docker tag springboot-k8s:1.0.0 pavanktm/springboot-k8s:1.0.0"
        sh "docker login -u pavanktm -p Lion@1234"
        sh "docker push pavanktm/springboot-k8s:1.0.0"
    }
    stage('deploy')
    {
        sh "kubectl apply -f deployment.yaml"
        sh "kubectl apply -f service.yaml"
    }
}
