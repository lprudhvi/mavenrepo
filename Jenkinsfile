pipeline{
agent {label 'devserver1'}

triggers {
        pollSCM '* * * * *'
    }

stages{

stage('scm'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[credentialsId: '8e9f5687-c989-46d2-ab89-1fdf0cd1c3e1', url: 'https://github.com/lprudhvi/mavenrepo.git']]])
}
}

stage('build'){
steps{
sh 'mvn package'
}
}

stage('sonar'){
steps{
withSonarQubeEnv('sonarqube') {
    sh 'mvn sonar:sonar'
}
}
}

stage('nexus'){
steps{
sh 'mvn deploy'
}
}

stage('tomact'){
steps{
sh 'scp /root/workspace/sample/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war root@54.172.93.35:/var/lib/tomcat/webapps'
}
}

}
}
