pipeline {
    agent any;
    tools {
        maven "Maven 3.8.6"
    }
    stages {
        stage("Build") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test") {
            steps {
                sh "mvn test"
            }
        }
        stage("Release") {
            steps {
                nexusPublisher nexusInstanceId: 'nexus-st', nexusRepositoryId: 'maven-releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: './target/demo-0.0.1-'+env.BRANCH_NAME+'.jar']], mavenCoordinate: [artifactId: 'demo.jar', groupId: 'com.example.demo', packaging: 'jar', version: env.BRANCH_NAME]]]
            }
        }
    }
}
