pipeline {
    agent any

    stages {
        // 获取代码
        stage('pull code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'f6a748f8-bbb0-40f5-8f15-6c9467c6e63f', url: 'git@github.com:y1738103684/self-flog-fe.git']]])
            }
        }

        stage('build project') {
            steps {
              sh 'java -version'
              sh 'mvn -v'
              sh 'node -v'
              sh 'npm -v'
            }
        }
    }

    // 发送邮箱
    post {
      success {
        emailext (
                        subject: "【构建成功】:'${JOB_NAME} [${BUILD_NUMBER}]'",
                        body: '${FILE,path="email.html"}',
                        to: 'y19834530446@163.com',
                 )
      }
      failure {
        emailext (
                        subject: "【构建失败】: '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                        body: '${FILE,path="email.html"}',
                        to: 'y19834530446@163.com',
                )
      }
    }

}
