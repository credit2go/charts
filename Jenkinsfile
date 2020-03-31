#!/usr/bin/env groovy

def label = "builder-${UUID.randomUUID().toString()}"
podTemplate(label: label, yaml: libraryResource('kubernetes/deploy.yaml')) {
    node(label) {
        container('slave') {
            timeout(activity: true, time: 5) {
                //config git to enable commit and push to github
                gitlabUtil.writeGlobalGITConfigFile()
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
}
