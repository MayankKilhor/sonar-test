@Library('jenkins-pipeline-util') _



pipeline {
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
