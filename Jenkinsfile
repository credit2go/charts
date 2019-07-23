#!/usr/bin/env groovy

def label = "builder-${UUID.randomUUID().toString()}"
podTemplate(label: label, yaml: libraryResource('kubernetes/builder.yaml')) {
    node(label) {
        container('slave') {
            //config git to enable commit and push to github
            commonUtil.writeGlobalGITConfigFile()
            //prepare helm before execution
            kubernetesUtil.prepareHelmRepo()
            ws('/charts') {
                //clone into nfs server path
                checkout scm
                sh 'helm repo index --url https://charts.credit2go.cn/candidates/'
                sh 'helm repo index --url https://charts.credit2go.cn/releases/'
                sh 'git add -A *'
                sh 'git commit -a -m "sync with local server"'
                sh 'git push'
            }
        }
    }
}