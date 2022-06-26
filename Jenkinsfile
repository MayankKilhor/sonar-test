@Library('jenkins-pipeline-util') _



pipeline {
    agent {
      docker {
        image 'nexus.cicd.sv2.247-inc.net:5000/247nodejs-build-centos7:16.13.1_npm_v6_jenkins_oss'
        // assume HTTP_PROXY_URL is defined as a jenkins system level env var
        label 'build_sv2'
        args "-e HTTP_PROXY=${env.HTTP_PROXY_URL}"
      }
    }
    stages {
        stage('Install') {
          steps {
            sh 'env'
            script {
              setupStandardNodeBuild(script: this)
            }
          }
        }
        // stage('Validate & Publish Report') {
        //   steps {
        //     script {
        //       nodeValidate(script: this)
        //     }
        //   }
        // }
        stage('Sonar Scan') {
          steps {
            script {
              sonarScan(script: this)
            }
          }
        }
        stage('Quality Gate'){
          steps {
            timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true }
          }
        }
        // stage('Deploy') {
        //   when {
        //     branch 'main'
        //   }
        //   steps {
        //     script {
        //       nodePruneZipDeploy(script: this)
        //     }
        //   }
        // }

    }
}
