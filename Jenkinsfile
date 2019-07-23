#!/usr/bin/env groovy

def label = "builder-${UUID.randomUUID().toString()}"
podTemplate(label: label, yaml: libraryResource('kubernetes/builder.yaml')) {
    node(label) {
        container('slave') {
            //config git to enable commit and push to github
            commonUtil.writeGlobalGITConfigFile()
            //prepare helm before execution
            kubernetesUtil.prepareHelmRepo()
            sh '''cd /charts
                  git pull
                  helm repo index --url https://charts.credit2go.cn/candidates/ candidates
                  helm repo index --url https://charts.credit2go.cn/releases/ releases
                  git add -A *
                  git commit -a -m "sync with local server"
                  git push
            '''
        }
    }
}