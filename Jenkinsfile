node{
    stage("git clone"){
        git credentialsId: 'git_Cred', url: 'https://github.com/selvam0016/mithun_spring-boot-mongo-docker.git'
    }
    stage("maven clean build"){
        def mavenHome = tool name: "mymaven", type: "maven"
        def mavenCMD= "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    stage("docker build"){
        sh "docker build -t devopslearner16/spring-boot-mongo ."
    }
    stage("Docker Push"){
    withCredentials([string(credentialsId: 'Docker_Cred', variable: 'Docker_Cred')]) {
    sh "docker login -u devopslearner16 -p ${Docker_Cred}"
    } 
     sh "docker push devopslearner16/spring-boot-mongo"
      }
    stage("Deploy app in to K8s"){
        kubernetesDeploy(
            configs: 'springBootMongo.yml',
            kubeconfigId: 'Kubernetes_Config',
            enableConfigSubstitution: true
            )
    }
}
