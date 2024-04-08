
### force resolve dependencies
```shell
mvn dependency:resolve -U
```

### purge local repository
```shell
mvn dependency:purge-local-repository -Dinclude:org.slf4j -DresolutionFuzziness=groupId -Dverbose
```
### check dependency tree
```shell
mvn dependency:tree
```
#### download source code
```shell
mvn dependency:sources

mvn dependency:sources -DdownloadSources=true -DdownloadJavadocs=true
```

### for more detail about maven dependency plugin please refer to below link
    https://maven.apache.org/plugins/maven-dependency-plugin/