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
  
  stage('Nexus Deploy') {
    nexusPublisher nexusInstanceId: 'nexuspipeline', nexusRepositoryId: 'thirdparty', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '~/workspace/GameOfLifePipeline_master-YRW7MBWKGVMZJOYMZ7VOH4DPLIT5PDXRNTWQB4WKIVFNSVHN7VBQ/target/spring-boot-sample.jar']], mavenCoordinate: [artifactId: 'spring-boot-sample', groupId: 'nl.revolution', packaging: 'jar', version: '0.0.1-SNAPSHOT']]]
    }
}
