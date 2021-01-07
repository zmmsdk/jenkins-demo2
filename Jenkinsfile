// #!groovy
pipeline {
   agent any
       tools {
        nodejs 'NodeJS 15.5.1'
        // gradle "gradle"
    }
    // 指定一个小时的全局执行超时，之后Jenkins将中止Pipeline运行
    // options {
    //     timeout(time: 1, unit: 'HOURS') 
    // }
    // environment { 
    //     CC = 'clang'
    // }
//定期检查开发代码自动触发更新，工作日每晚4点做daily build
    // triggers {
    //     pollSCM('H 4 * * 1-5')
    // }
    stages {
        // stage('Checkout') {
        //     steps {
        //         echo 'Checkout'
        //         checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '500378f5-a6e4-4255-984e-61537fe0e455', url: 'git@gitlab.aniu.so:aniu-yunwei/game-of-life.git']]])
        //     }
        // }        
        // stage('Build') {
        //     steps {
        //         echo 'Building'
        //         // sh 'mvn clean install' # 可以用自己的 mvn clean deploy + 参数替代
        //     }
        // }
          stage('Linting') {
            steps {
               script {
                sh 'npm config set registry https://registry.npm.taobao.org' 
                sh 'npm config get registry' 
                // sh 'cnpm install'

               
                   

                sh 'npm install'
                sh 'npm run build'
               }
            }
        }   
        stage('Test') {
            steps {
                // echo 'env.BRANCH_NAME'
                echo 'Testing'
                // sh 'mvn clean verify sonar:sonar' # 此处可以使用mvn test替代，笔者这步是检测代码的质量同步到自己的代码质量检测平台。
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
                // sh 'mvn clean deploy'  # 此处调用脚本或者ansible、saltstak，部署到远程
            }
        }
    }
}
