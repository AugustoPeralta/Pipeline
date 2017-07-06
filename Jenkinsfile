node {
  
  stage('Configure') {
    env.PATH = "${tool 'maven 3'}/bin:${env.PATH}"
  }

  stage('Checkout') {
    git 'https://github.com/AugustoPeralta/spring-boot.git'
  }

  stage('Build') {
    sh 'mvn -B -V -U -e clean package'
  }

  stage('Archive') {
    junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
    archive 'target/*.jar'
  }
  
  nexusPublisher nexusInstanceId: 'nexuspipeline', nexusRepositoryId: 'Lab-Repository-Release', packages: [[$class: 'MavenPackage', mavenAssetList: [], mavenCoordinate: [artifactId: 'spring-boot-sample', groupId: 'nl.revolution', packaging: 'jar', version: '0.0.1-SNAPSHOT']]]
   
}
