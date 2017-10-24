import static groovy.json.JsonOutput.*

API_ROOT_URL = 'https://hesperides.mycompany.com'

node {
    withCredentials([[$class: 'UsernamePasswordBinding',
                      credentialsId: 'HesperidesScriptCredentials',
                      variable: 'auth']]) {
        try {
            stage('Test getPlatformInfo') {
                echo prettyPrint(toJson(hesperides.getPlatformInfo(apiRootUrl: API_ROOT_URL,
                                                                   auth: auth,
                                                                   app: 'KTN',
                                                                   platform: 'USN1')))
            }

            stage('Test releaseModule') {
                echo prettyPrint(toJson(hesperides.releaseModule(apiRootUrl: API_ROOT_URL,
                                                                 auth: auth,
                                                                 moduleName: 'demoKatana-war',
                                                                 workingcopyVersion: '1.0.0.0',
                                                                 releaseVersion: '1.0.0.0')))
            }

            stage('Test setPlatformVersion') {
                echo prettyPrint(toJson(hesperides.setPlatformVersion(apiRootUrl: API_ROOT_URL,
                                                                      auth: auth,
                                                                      app:'KTN',
                                                                      platform:'USN1',
                                                                      currentVersion:'1.0.0.0',
                                                                      newVersion:'1.0.0.0')))
                // should do the same, as isWorkingcopy is not enforced by default
                echo prettyPrint(toJson(hesperides.setPlatformVersion(apiRootUrl: API_ROOT_URL,
                                                                      auth: auth,
                                                                      app:'KTN',
                                                                      platform:'USN1',
                                                                      currentVersion:'1.0.0.0',
                                                                      newVersion:'1.0.0.0',
                                                                      isWorkingcopy: true)))
            }

            stage('Test setPlatformModulesVersion') {
                echo prettyPrint(toJson(hesperides.setPlatformModulesVersion(apiRootUrl: API_ROOT_URL,
                                                                             auth: auth,
                                                                             app:'KTN',
                                                                             platform:'USN1',
                                                                             currentVersion:'1.0.0.0',
                                                                             newVersion:'1.0.0.0')))
            }

            stage('Test createInstance') {
                hesperides.createInstance(apiRootUrl: API_ROOT_URL,
                                          app: 'KTN',
                                          auth: auth,
                                          platform: 'USN1',
                                          moduleName: 'demoKatana-war',
                                          instance: 'INSTANCE_TEST')
            }

            stage('Test updateProperties') {
                echo prettyPrint(toJson(hesperides.updateProperties(apiRootUrl: API_ROOT_URL,
                                                                    auth: auth,
                                                                    app: 'KTN',
                                                                    platform: 'USN1',
                                                                    jsonPropertyUpdates: 'http://gitlab.mycompany.com/KTN-USN1.json',
                                                                    commitMsg: 'vsct-hesperides-api tests from Jenkinsfile')))
            }

            stage('Test getModuleVersions') {
                echo prettyPrint(toJson(hesperides.getModuleVersions(apiRootUrl: API_ROOT_URL,
                        auth: auth,
                        moduleName: 'demoKatana-war')))
            }
        } finally {
            stage('Test deleteModule') {
                hesperides.deleteModule(apiRootUrl: API_ROOT_URL,
                                        auth: auth,
                                        moduleName: 'demoKatana-war',
                                        version: '1.0.0.0',
                                        moduleType: 'release')
            }
            stage('Test deleteInstance') {
                hesperides.deleteInstance(apiRootUrl: API_ROOT_URL,
                                          auth: auth,
                                          app: 'KTN',
                                          platform: 'USN1',
                                          moduleName: 'demoKatana-war',
                                          instance: 'INSTANCE_TEST')
            }
        }
    }
}