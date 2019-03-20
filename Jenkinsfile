node{
  stage('SCM CHeckout'){
    
    git'https://github.com/Alex2626/softwareSeguroPEC4'
  }
  stage('Compile-Package'){
    def mvnHome = tool name: aven-3', type: 'maven'
    sh"${mvnHomeÇ}/bin/mvn package"

}
