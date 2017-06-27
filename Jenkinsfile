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
     nexusArtifactUploader
        artifactId: 'spring-boot-sample',
        file: '~/workspace/GameOfLifePipeline_master-YRW7MBWKGVMZJOYMZ7VOH4DPLIT5PDXRNTWQB4WKIVFNSVHN7VBQ/target/spring-boot-sample.jar',
        groupId: 'nl.revolution',
        type:'jar',
        nexusPassword: 'admin123',
        nexusUrl: 'http://192.168.1.24:30333/nexus',
        nexusUser: 'admin',
        nexusVersion: 'nexus 2.14.4-03',
        protocol: 'http',
        repository: 'maven-snapshots',
        version: '0.0.1-SNAPSHOT' 
    }
}
