---
title: maven转gradle小记
date: 2025-05-13 14:44:30
tags: maven
category: 备案
---
gradle打包jar速度确实比maven快，而且还有可以单独打包里面一个jar，不必先上传父依赖，而会自动生成的特点，确实方便很多。
但用在jenkins打包过程中，我发现它有一个缺点，插件里面无法导出环境变量，毕竟没有pipeline；用老式的拼装式job感觉比pipeline方便很多-我不喜欢写代码。
折腾了好久， exposes出的环境变量，在最后的salt插件==Send a message to Salt API== 中无法获取这些变量；放弃了，等以后有时间再弄。

*This plugin exposes variables found from the project's POM (as of version 2.1):*

*   POM\_VERSION - taken from \<version> in POM

PS:参考url:
<https://plugins.jenkins.io/maven-plugin/>

```shell
//Jenkinsfile (Declarative Pipeline)
import jenkins.model.*
import groovy.json.JsonOutput

pipeline {
    agent {
        label 'ci02'
    }

    tools {
        jdk 'JDK 8'
    }

    parameters {
        booleanParam defaultValue: false, description: '是否需要编译，只发布不需要勾选', name: 'test_DO_BUILD'
        choice choices: ['REL', 'PRO'], description: '环境', name: 'SERVICE_ENV'
        extendedChoice description: '要发布的服务器，多个服务器用逗号分隔', multiSelectDelimiter: ',', name: 'TARGET_NAME', quoteValue: false, saveJSONParameterToFile: false, type: 'PT_CHECKBOX', value: 'java02', visibleItemCount: 2
        gitParameter branchFilter: 'origin/(.*)', defaultValue: 'feat-div', description: '分支', name: 'BRANCH_NAME', type: 'PT_BRANCH',sortMode: 'DESCENDING_SMART',selectedValue: 'DEFAULT'
        text defaultValue: '-Xms512m -Xmx512m -Dservice.env=REL -Djava.io.tmpdir=./temp/', description: '启动时使用的JAVA参数', name: 'JAVA_OPTS'
    }

    stages {
        stage("Git") {
            steps {
                git branch: "${params.BRANCH_NAME}", credentialsId: 'ec3ecaa3-3cdf-4add-b6f5-9d672ba78263', url: 'ssh://git@git.****ol.com:8855/service/isvpay.git'
            }
        }

        stage('Build') {
            when { expression { return params.test_DO_BUILD } }

            steps {
                echo '开始构建..'
                sh '/opt/gradle-7.6.4/bin/gradle  payment:bootJar'
            }
        }

        stage('Deploy') {
            when {
                environment name: 'SERVICE_ENV', value: 'REL'
            }

            environment {
                BUILD_VERSION = """${sh(
                        returnStdout: true,
                        script: '/opt/gradle-7.6.4/bin/gradle payment:properties | grep "^version:"|awk  \'{print $NF}\''
                )}""".trim()

                SALT_ARGS = """deploy.java 'pillar={"project":{"name": "isvpay-payment"},"java":{"java_opts":"${params.test_JAVA_OPTS}", "jar_name":"payment-${BUILD_VERSION}.jar"}}'"""
            }

            steps {
                echo SALT_ARGS
                echo '开始发送制品...'
                sh "/test/scripts/deploy/send_artifacts.sh -p isvpay-payment payment/build/libs/payment-${BUILD_VERSION}.jar conf/payment/application*.yml"
                salt(authtype: 'pam', clientInterface: local(arguments: SALT_ARGS,
                                                            function: 'state.sls',
                                                            jobPollTime: 30,
                                                            target: "${params.TARGET_NAME}",
                                                            targettype: 'list'),
                    credentialsId: '5810dae9-21e3-4d97-a6e4-c729feab40b3',
                    saveFile: true,
                    servername: 'http://salt.dev.testol.com:8001')
                script {
                    env.WORKSPACE = pwd()
                    def output = readFile "${env.WORKSPACE}/saltOutput.json"
                    echo JsonOutput.prettyPrint(output)
                }
            }
        }
    }
}

```

