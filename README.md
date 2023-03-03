# nm-api-generator
Automatic generation of API bindings

Deprecated in favor of https://github.com/e-Learning-by-SSE/nm-jenkins-groovy-helper-lib

We recommend generating clients directly in the jenkins pipeline of the associated project by using the helper scripts from the jenkins library. 

This could look like this:

```groovy
stage('Maven') {
    steps {
        withMaven(mavenSettingsConfig: 'mvn-elearn-repo-settings') {
            sh "mvn clean verify spring-boot:build-image -Dspring-boot.build-image.imageName=${env.DOCKER_TARGET}"
        }
        script {
            version = getMvnProjectVersion()
            generateSwaggerClient('target/openapi.json', version, 'net.ssehub', 'nm-facade-service', ['javascript'])
        }
    }
}
```
More examples in the lib-repository.
