pipeline{
    agent any
    environment {
      WS = "${WORKSPACE}"
    }
    //定义流水线的加工流程
    stages {
        //流水线的所有阶段
        stage('环境检查'){
            steps {
               sh 'printenv'
               echo "正在检测基本信息"
               sh 'java -version'
               sh 'git --version'
               sh 'docker version'
               sh 'pwd && ls -alh'
               //未来，凡是需要取变量值的时候，都用双引号
               //sh "ssh --help"
            }
        }
        //1、编译 "abc"
        stage('maven编译'){
            //jenkins不配置任何环境的情况下， 仅适用docker 兼容所有场景
            agent {
                docker {
                    image 'maven:3-alpine'
                    // args '-v /var/jenkins_home/appconfig/maven/.m2:/root/.m2'
                 }
            }
            steps {
               //git下载来的代码目录下
               sh 'pwd && ls -alh'
               sh 'mvn -v'
               sh "echo 默认的工作目录：${WS}"
                sh 'cd ${WS} && mvn clean package -s "/var/jenkins_home/appconfig/maven/settings.xml"  -Dmaven.test.skip=true '
            }
        }

        //4、部署
        stage('部署'){
            steps {
                echo "部署..."

            }
        }
    }
}