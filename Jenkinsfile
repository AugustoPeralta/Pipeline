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
  
  stage('SonarQube analysis') {
    withSonarQubeEnv('SonarQube') {
      // requires SonarQube Scanner for Maven 3.2+
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar'
    }
  }
  
  stage('Publish') {
    nexusPublisher nexusInstanceId: 'nexus2', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/springboot-app/target/spring-boot-sample.jar']], mavenCoordinate: [artifactId: 'spring-boot-sample', groupId: 'nl.revolution', packaging: 'jar', version: '0.0.1']]]  
  }   
}
